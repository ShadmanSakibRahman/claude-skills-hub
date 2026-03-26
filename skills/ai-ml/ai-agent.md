---
description: Build AI agents with tool use, ReAct pattern, multi-step reasoning, guardrails, and human-in-the-loop
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in building AI agent systems. When creating or improving an AI agent, follow these steps:

1. **Define the agent's purpose and boundaries**:
   - Write a clear system prompt: the agent's role, what it can and cannot do, and how it should reason.
   - Define the domain scope — what tasks the agent handles and when it should refuse or escalate.
   - Set output format expectations for the final response.
   - Specify the LLM model to use and its configuration (temperature, max tokens).

2. **Define tools/functions**:
   - Each tool needs: a descriptive `name`, a clear `description` (the LLM reads this to decide when to use it), and a JSON Schema for `parameters`.
   - Write descriptions from the LLM's perspective: "Search the product catalog by name, category, or price range. Returns matching products with details."
   - Include parameter constraints: required fields, enums for fixed options, min/max for numbers.
   - Keep the tool set focused — 5-15 tools is ideal. Too many tools confuse the model.
   - Categories of tools: data retrieval (search, lookup), data mutation (create, update, delete), computation (calculate, convert), external APIs (email, SMS).

3. **Implement the ReAct pattern** (Reasoning + Acting):
   - Loop: the LLM receives the task and available tools, then outputs either a tool call (Action) or a final answer.
   - After each tool call: execute the tool, format the result, and append it to the conversation as a tool result message.
   - The LLM reviews the result and decides: call another tool, or provide the final answer.
   - Set a maximum iteration limit (e.g., 10 steps) to prevent infinite loops.
   - If the limit is reached, ask the LLM to summarize what it accomplished and what remains.

4. **Handle multi-step reasoning**:
   - Encourage the LLM to plan before acting: "First, I need to... Then I'll... Finally, I'll..."
   - For complex tasks, break them into subtasks and solve sequentially.
   - Allow the agent to backtrack: if a tool returns unexpected results, re-plan.
   - Pass accumulated context between steps so the agent remembers what it has learned.
   - Use structured scratchpad or chain-of-thought prompting to make reasoning explicit.

5. **Manage conversation history**:
   - Store the full message history: system prompt, user messages, assistant messages, tool calls, and tool results.
   - Implement token-aware truncation: summarize older exchanges when approaching context limits.
   - Preserve tool call/result pairs together — never orphan a tool result without its call.
   - For multi-turn agents, maintain a "working memory" of key facts extracted during the conversation.

6. **Add guardrails**:
   - **Input validation**: Check user input for prompt injection attempts, PII, or malicious content before passing to the LLM.
   - **Output validation**: Verify the LLM's tool call parameters are valid before execution. Check the final response for hallucinations, PII leakage, or policy violations.
   - **Tool execution safety**: Validate parameters, use least-privilege permissions, sandbox destructive operations.
   - **Rate limiting**: Limit tool calls per session and per time window.
   - **Content filtering**: Apply content safety filters to both input and output.
   - Log all decisions and tool calls for audit.

7. **Implement human-in-the-loop**:
   - Define which actions require human approval: data deletion, financial transactions, external communications.
   - When approval is needed: pause the agent, present the proposed action with context to the human, wait for approve/reject/modify.
   - Handle the approval response: proceed if approved, adjust if modified, explain to the user if rejected.
   - Set timeouts for pending approvals with appropriate fallback behavior.
   - Log all approval decisions for compliance.

8. **Error handling and recovery**:
   - Tool execution failures: return a clear error message to the LLM so it can try an alternative approach.
   - LLM API failures: implement retries with exponential backoff, fallback to a simpler model if available.
   - Malformed tool calls: return a validation error with guidance on correct usage.
   - Unexpected states: have the agent explain what went wrong and suggest next steps.

9. **Testing and evaluation**:
   - Create test scenarios covering: simple single-tool tasks, multi-step tasks, error recovery, edge cases, and adversarial inputs.
   - Evaluate on: task completion rate, number of steps taken, tool usage accuracy, and response quality.
   - Benchmark against different models to find the best cost/quality trade-off.
   - Monitor production usage: track success rates, common failure patterns, and user feedback.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
