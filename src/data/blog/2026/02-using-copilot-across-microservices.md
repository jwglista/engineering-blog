---
title: Using Copilot to Research Microservices
author: John Glista
pubDatetime: 2026-02-24T23:00:00Z
featured: false
draft: false
tags:
  - SoftwareEngineering
  - AI
  - Copilot
description:
  How I used Copilot to easily trace together calls between microservices
---

Where I work, we have about 5-6 (micro)services that all operate in the backend and tie together.  They ultimately get called by a BFF service that serves an Android app that is used in our stores to fulfill orders.  All of these services are written with Kotlin and Spring Boot.  While a microservices architecture can have many advantages in a purely backend application, there are several challenges when they are serving a front-end:

1. Keeping track of deprecated/unused methods in the backend.  Oftentimes the front end will stop using one of the backend endpoints, but the endpoint will remain in the backend codebase
2. Understanding/remembering all the complex call paths as they originate from the Android app and flow through the BFF layer and then to the other various backend services
3. Coordinating changes to contracts from front-end --> BFF --> backend
4. Creating useful integration test flows for the backend services that accurately replicate the same series of calls that would happen naturally from the front-end

Fortunately, generative AI models can help tremendously with these tasks.  At my company, we currently use GitHub Copilot.  Today I was manually testing a portion of our Android app for a pending production release.  I noticed what was most likely a bug, but wanted to understand the full trace of calls from front-end through the backend services.  Historically to do this, you would need to start by looking in the Android app code, pinpointing the view models that populate the data, find the correct API call to the BFF layer, trace through that code, etc. etc.  It wasn't a difficult task, just tedious.  This is where AI tends to shine IMO, handling these types of tedious tasks.  I simply gave it a prompt and told it which tab in the Android app I was in, reminded it how the services tie together, and told it the details on the bug I was researching.  It gave me back a very clear and descriptive call trace so that I could look at the code myself, and it also continued to help troubleshoot the bug.  I ultimately stopped the agent since I discovered a pending PR that addressed the issue, but the point here is how clearly it was able to spell out the whole call flow in such a short period of time.  This can save a tremendous amount of time for engineers.  The ultimate goal here would be to have a living document that stays updated and spells out all these call flows so that we don't have to prompt AI every time. Perhaps we could have something in our deployment pipelines or pull-request actions that would update such a document using AI.  

I would also like to use this technique to have Copilot find more of the deprecated/unused API endpoints in the backend.  I did this for endpoint yesterday because I had suspected it was no longer in use, but would be interesting to see how thoroughly it could find all such instances.  