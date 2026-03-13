---
title: PostgreSQL MCP Server
author: John Glista
pubDatetime: 2026-03-13T10:00:00Z
featured: false
draft: false
tags:
  - SoftwareEngineering
  - AI
  - Copilot
  - MCP
description:
  Creating a PostgreSQL MCP Server
---

## Creating a PostgreSQL MCP Server

In the pursuit of having LLMs troubleshoot bugs in nonprod and issues in production, I wanted to provide access to our databases.  These days there is code out there for so many MCP servers, but with how easy it is to create one using Copilot, I decided to make my own.  I've also found that sometimes it's faster to just make one yourself than to find the "right" MCP server and vet it yourself.  

### The Process

The process was straightforward.  I created a prompt that outlined the following requirements for this MCP server:

1. It must allow easy switching between each of our environments (dev, qa, load, prod)
2. It must be configurable as read-only/read-write
3. The prod environment must *never* allow read-write mode, even if the config has it turned on (if it gets left on accidentally after being in a lower environment)
4. It must be able to connect to all of the DBs of our microservices and know which service each DB is associated with
5. It must have unit tests for full code coverage

Since I had already written a Kafka MCP server and created a GitHub repo for our team's MCP servers, I planned to build this MCP server here.  That MCP server was written in Go, so Copilot (Claude Sonnet 4.6) observed that pattern and created this PSQL MCP server in Go as well.

### Thanks Copilot

While working with Copilot to ensure that prod will always be read-only from the code, it also suggested creating dedicated users in the DB as read-only users.  While this seems obvious, it's still impressive that it made this suggestion which was outside of the scope of just writing the code.  So I had it write a SQL script for creating these read-only users.

### More to Come

I haven't had a chance yet to put this MCP server to good use, I only gave it a few prompts to have it connect the dots on one order across our multiple DBs, and it already did a great job at that.  The real power will come when I can hook this up with our app logs in AKS or Kibana.  When Copilot can piece together our code, Kafka messages, app logs, and the DBs, it will have everything it needs to fully troubleshoot/fix bugs and prod issues in the environments.