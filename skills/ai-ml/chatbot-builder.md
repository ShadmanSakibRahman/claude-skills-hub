---
description: Build conversational AI chatbots with state management, intent recognition, tool calling, and streaming responses
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in building conversational AI systems. When creating or improving a chatbot, follow these steps:

1. **Define the chatbot's scope and persona**:
   - Write a clear system prompt defining the bot's role, expertise, tone, and boundaries.
   - List the tasks the bot can handle and explicit out-of-scope topics.
   - Define the escalation path: when and how to hand off to a human agent.
   - Set response length guidelines: concise for simple queries, detailed for complex ones.

2. **Implement conversation state management**:
   - Store conversation history as a list of `{role, content}` message objects.
   - Implement a sliding window or token-based truncation to stay within context limits.
   - Strategy: keep the system prompt + last N messages + a summary of earlier messages.
   - Use `tiktoken` (OpenAI) or model-specific tokenizers to count tokens accurately.
   - Store conversation state in a session store (Redis, database) keyed by session ID.
   - Handle conversation reset/new conversation gracefully.

3. **Implement intent recognition** (if not using pure LLM):
   - Define intents: greeting, FAQ, order_status, complaint, etc.
   - For LLM-based: instruct the model to classify intent in a structured output before responding.
   - For hybrid: use a fast classifier (fine-tuned BERT, regex patterns) for routing, then LLM for response generation.
   - Handle multi-intent messages: "Check my order and also update my address."

4. **Entity extraction**:
   - Extract structured data from user messages: dates, names, order numbers, product names.
   - Use the LLM with a structured output format (JSON mode or function calling) to extract entities.
   - Validate extracted entities against your data (e.g., check if order number exists in the database).
   - Ask for confirmation when extracted entities are ambiguous.

5. **Context window management**:
   - Track token usage per message and cumulative for the conversation.
   - When approaching the limit: summarize older messages using a separate LLM call, replacing detailed history with a concise summary.
   - Preserve critical information: user's name, current task, extracted entities.
   - Use a priority system: system prompt > current task context > recent messages > older messages.

6. **Implement tool/function calling**:
   - Define tools with clear names, descriptions, and parameter schemas (JSON Schema).
   - Tools examples: `search_knowledge_base`, `get_order_status`, `create_ticket`, `calculate_price`.
   - Parse the LLM's tool call response, execute the function, and return results to the LLM.
   - Handle tool errors gracefully — return an error message to the LLM so it can inform the user.
   - Implement tool call limits (max 5 per turn) to prevent infinite loops.
   - Log all tool calls for debugging and audit.

7. **Set up streaming responses**:
   - Use the streaming API (`stream=True` for OpenAI, async iterators for Anthropic).
   - Forward chunks to the client via Server-Sent Events (SSE) or WebSocket.
   - Handle tool calls during streaming: buffer until the tool call is complete, execute, then continue streaming.
   - Implement typing indicators while waiting for the first token.
   - Handle stream interruption: allow users to cancel and stop generation.

8. **Fallback handling**:
   - Detect when the bot cannot answer: low confidence, out-of-scope, or repeated misunderstandings.
   - Fallback chain: rephrase understanding -> ask clarifying question -> offer alternatives -> escalate to human.
   - Track consecutive fallbacks — escalate after 2-3 in a row.
   - Log fallback events for later analysis and prompt improvement.

9. **Testing and monitoring**:
   - Create a test suite with representative conversations covering happy paths and edge cases.
   - Monitor in production: response latency, token usage, fallback rate, user satisfaction (thumbs up/down).
   - Log all conversations (with PII handling) for quality review.
   - Set up alerts for high error rates or unusual patterns.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
