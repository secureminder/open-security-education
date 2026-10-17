# AI Security

## Table of Contents

- [Curriculum](#curriculum)
  - [01. Your First Day on an AI Security Engagement](#01-your-first-day-on-an-ai-security-engagement)
  - [02. Map the AI System and Its Data Flows](#02-map-the-ai-system-and-its-data-flows)
  - [03. Test Direct and Indirect Prompt Injection](#03-test-direct-and-indirect-prompt-injection)
  - [04. Test Sensitive Data Leakage and User Access Controls](#04-test-sensitive-data-leakage-and-user-access-controls)
  - [05. Your First RAG and Vector Database Security Assessment](#05-your-first-rag-and-vector-database-security-assessment)
  - [06. Test AI Tools, Agents, and Action Authorization](#06-test-ai-tools-agents-and-action-authorization)
  - [07. Test MCP Servers and Third-Party AI Integrations](#07-test-mcp-servers-and-third-party-ai-integrations)
  - [08. Test Unsafe AI Outputs and Downstream Application Actions](#08-test-unsafe-ai-outputs-and-downstream-application-actions)
  - [09. Test AI APIs, Model Endpoints, Rate Limits, and Cost Abuse](#09-test-ai-apis-model-endpoints-rate-limits-and-cost-abuse)
  - [10. Check Model Files, Training Data, and AI Supply Chain Security](#10-check-model-files-training-data-and-ai-supply-chain-security)
  - [11. Run Automated AI Red Team Tests and Compare Results](#11-run-automated-ai-red-team-tests-and-compare-results)
  - [12. Fix Findings, Add Regression Tests, and Retest the AI System](#12-fix-findings-add-regression-tests-and-retest-the-ai-system)

## Curriculum

### 01. Your First Day on an AI Security Engagement

You’ll take over a real client-style AI security assignment. You’ll find out what the chatbot does, which accounts and files you can use, which actions are off-limits, and how to record what happens when you test it.

Client scenario: Northstar Shop asks SecureMinder to assess its staging customer-support assistant at https://assistant.northstar.example. The assistant answers questions using company help articles, looks up a signed-in customer's test orders, and can prepare a support ticket. The client gives you a written test agreement, two customer accounts (Alice and Bob), a support-agent account, dummy orders, a staging API, and a contact at the engineering team. All addresses and identities are fictional training examples.

### 02. Map the AI System and Its Data Flows

Now that your accounts and tools work, you’ll follow a real customer question from the chat window to the model, the help articles, and the order or ticket service. You’ll use the actual requests and the engineer’s diagrams to find every place where the assistant reads data or is allowed to take an action.

Client scenario: Continue with Northstar Shop's staging assistant and the Alice, Bob, and support-agent accounts from module 01. The engineer provides a sample OpenAPI file, a simple architecture diagram, one test article, and read-only access to selected staging logs.

### 03. Test Direct and Indirect Prompt Injection

With the chatbot's normal behavior recorded, you’ll now check whether it follows instructions that should not control it. First you’ll put a conflicting instruction in Alice's chat message. Then you’ll place one in a harmless returns article and see whether the assistant treats the article as information or as a command.

Client scenario: The Northstar Shop engineer gives you a disposable copy of the returns article and a dedicated document index used only by the staging chatbot. The test instruction asks the assistant to include the exact sentence 'Blue umbrellas are on sale today' in an answer about returns. It must not change orders, send information elsewhere, or create a ticket.

### 04. Test Sensitive Data Leakage and User Access Controls

You’ve checked whether the chatbot follows misleading instructions. Now you’ll check whether Alice can see Bob’s order, whether a support agent can see customer-only notes, and whether passwords or API keys ever appear in answers or logs.

Client scenario: Northstar Shop provides Alice and Bob’s dummy orders 1001 and 1002, a support-agent login, a test-only secret named NORTHSTAR_TEST_KEY, and chat-history records belonging to each account.

### 05. Your First RAG and Vector Database Security Assessment

You’ve found out who should see each record. Next you’ll follow how the assistant searches Northstar’s help articles and make sure the search index does not return private documents or keep old text after it has been removed.

Client scenario: The engineer gives you a staging help-article index with public returns.md, support-only refunds-internal.md, and an Alice-only sample record. Northstar uses a designated embedding model and either pgvector, Pinecone, or another documented index.

### 06. Test AI Tools, Agents, and Action Authorization

The document search is now checked. You’ll move to the assistant’s actions and see what happens when it prepares a ticket, reads an order, or is asked to make a change that the customer has not approved.

Client scenario: Northstar’s staging assistant can call get_order, search_help_articles, draft_ticket, and create_ticket. A training-only cancel_test_order tool is disabled for customers. Alice and Bob have separate dummy orders and ticket queues.

### 07. Test MCP Servers and Third-Party AI Integrations

Now you’ll look at the connectors behind those tools. You’ll check which MCP server supplies each tool, which account it acts as, and whether a customer can make a connector read or change records they do not own.

Client scenario: The engineer provides a staging MCP server that exposes search_help_articles and draft_ticket, plus a separate test ticket service. No production connectors or genuine secrets are used.

### 08. Test Unsafe AI Outputs and Downstream Application Actions

You’ve checked which tools the assistant may use. Next you’ll check what the Northstar website does with the text the model returns, especially when that text is shown as HTML or passed to a ticket or order service.

Client scenario: The engineer gives you a disposable customer-support page, a ticket preview panel, a harmless sample HTML marker, and a test-only tool that rejects invalid order and ticket fields.

### 09. Test AI APIs, Model Endpoints, Rate Limits, and Cost Abuse

You now know how the chatbot handles its replies. Next you’ll check whether the API requires a real login and whether one test user can consume more model calls or tokens than the customer has agreed to allow.

Client scenario: Northstar provides a staging chat API, a low-cost test model deployment, Alice and Bob’s access tokens, per-user request quotas, and a dashboard showing test token usage and spending.

### 10. Check Model Files, Training Data, and AI Supply Chain Security

The API limits are checked. Now you’ll look at the model files, packages, and documents the team uses to build the assistant, so an untrusted download or changed training file does not silently enter the staging system.

Client scenario: Northstar maintains a pinned model deployment, a test-only Hugging Face model repository, a Python requirements file, and a small sample dataset with known record counts. The engineer provides read-only access to the build configuration.

### 11. Run Automated AI Red Team Tests and Compare Results

You’ve completed the manual tests. Now you’ll turn the actual Northstar failures into repeatable checks so the team can catch the same problems when it changes the model, prompts, or search index.

Client scenario: The engineer gives you a staging API token, a fixed model budget, the approved Alice/Bob dummy records, and the safe prompt-injection marker used in module 03.

### 12. Fix Findings, Add Regression Tests, and Retest the AI System

You now have the list of tests that failed. You’ll work through the fixes with Northstar’s developers, rerun the same customer questions, and deliver a report showing what changed and which risks are still open.

Client scenario: Northstar’s developers have queued fixes for a document access filter, an overpowered ticket tool, a chat API quota, and rendering of generated text. You have the earlier test records and access to a new staging release.
