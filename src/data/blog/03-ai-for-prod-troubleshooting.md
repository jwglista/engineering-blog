---
title: AI For Prod Troubleshooting
author: John Glista
pubDatetime: 2026-03-08T14:00:00Z
featured: false
draft: false
tags:
  - SoftwareEngineering
  - AI
  - Copilot
  - ProductionSupport
description:
  How can we use AI to help us triage production issues faster?
---

## The Issue

This week I was on call and on Saturday discovered a production issue where several of the orders in our system were stuck in the first microservice within the flow.  This typically happens when we fail to enrich an order with the data it needs (product data and customer information) before sending it to the next service that handles picking operations.  To assist me, I was using an in-house tool built by another engineer using AI that analyzes application logs in Elastic using AI models.  I was then having to manually copy/paste the output from that analysis into Copilot CLI session that was looking at our codebase.  I had it create an integration test to capture what we thought was the issue in prod, and verified that the test failed with existing code, but passed after implementing the code fix.  The fix was to the reprocessing job that would attempt to reprocess the "stuck" orders.

I had faith that the fix would work, and deployed the hotfix to prod.  When the reprocessing job ran, however, the status of the orders remained as "ACCEPTED" (stuck) in the DB of the first service.  After some time, I decided to look at the Kafka topic where we publish the orders from this first service along to the pick service, and found that we had indeed been publishing the events every time the reprocessing job ran, even prior to the hotfix.  This is when I finally decided to look at the logs for the pick service, and found that the consumer had been throwing duplicate key violation errors when trying to insert into the DB.  When this happens, we never publish the READY_TO_PICK events back to the first service, and that DB will show the orders remaining in ACCEPTED status.  

Going back to using the AI log analysis tool, I was able to have it quickly extract all the primary key values from the error messages into a CSV so I could then manually research them in the DB and make the correct adjustments to resolve the issue.

## Lessons Learned

As with any microservices architecture, it's crucial to never get tunnel vision when triaging an issue.  Now with the use of AI, it's tempting to just point it to the first error messages you see and have it research and implement a fix.  

## Opportunities for deeper AI use:

1. Have the log analysis tool be able to tie directly into our codebase for more powerful root cause analysis, and total bug resolution in the code
2. Start using the Kafka MCP server that I created a few weeks ago to help out with issue triage.  This needs more testing/enhancement to make sure it won't use too many tokens when consuming messages
3. Figure out the best way to allow Copilot to query the DBs during issue triage
4. The biggest opportunity of improvement is figuring out how to use Copilot to tie all of this together during production issue analysis.  It should be able to look at the logs of all microservices in our system, all of their DBs, and all of the Kafka topics.  On top of that, if it's able to look at the codebases of all these services, it should then be able to properly determine root cause and suggest a fix.  