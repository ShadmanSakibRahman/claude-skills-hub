---
description: Set up LangChain/LlamaIndex pipelines with chains, agents, memory, retrievers, output parsers, and streaming
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in building LLM application pipelines with LangChain and LlamaIndex. When setting up or modifying these pipelines, follow these steps:

1. **Choose the framework and version**:
   - **LangChain**: Use `langchain` (core), `langchain-openai`, `langchain-anthropic`, `langchain-community` (integrations). Use LCEL (LangChain Expression Language) with the `|` pipe operator — avoid legacy `LLMChain` and `SequentialChain`.
   - **LlamaIndex**: Use `llama-index-core` and provider-specific packages. Use the query engine and chat engine abstractions.
   - Install only the packages you need — avoid installing the monolithic `langchain` package with all extras.

2. **Set up the LLM connection**:
   - LangChain: `ChatOpenAI(model="gpt-4o", temperature=0)` or `ChatAnthropic(model="claude-sonnet-4-20250514")`.
   - LlamaIndex: `OpenAI(model="gpt-4o")` or set `Settings.llm`.
   - Store API keys in environment variables — never hardcode them. Use `python-dotenv` to load from `.env`.
   - Configure timeouts, retries, and rate limiting for production use.

3. **Build chains with LCEL**:
   - Basic chain: `prompt | llm | output_parser`.
   - Create prompts with `ChatPromptTemplate.from_messages([("system", "..."), ("human", "{input}")])`.
   - Chain operations: `RunnablePassthrough` for passing data through, `RunnableParallel` for parallel execution, `RunnableLambda` for custom functions.
   - Example: `chain = {"context": retriever, "question": RunnablePassthrough()} | prompt | llm | StrOutputParser()`.
   - Use `.invoke()` for single calls, `.batch()` for multiple inputs, `.stream()` for streaming.

4. **Implement agents**:
   - Define tools using `@tool` decorator or `StructuredTool.from_function()`.
   - Each tool needs a clear docstring — the agent uses this to decide when to call it.
   - Create the agent: `create_tool_calling_agent(llm, tools, prompt)` with `AgentExecutor`.
   - Set `max_iterations` (default 15) and `handle_parsing_errors=True`.
   - For LlamaIndex: use `ReActAgent.from_tools(tools, llm=llm)` or `OpenAIAgent`.

5. **Configure memory**:
   - **ConversationBufferMemory**: Stores full history. Simple but grows unbounded.
   - **ConversationBufferWindowMemory**: Keeps last k exchanges. Set `k=10` as a starting point.
   - **ConversationSummaryMemory**: Summarizes older messages. Best for long conversations.
   - **ConversationTokenBufferMemory**: Keeps messages up to a token limit. Most predictable.
   - Add to chain: include `MessagesPlaceholder("chat_history")` in the prompt and pass history on each call.
   - For production: persist memory to a database (Redis, PostgreSQL) keyed by session ID.

6. **Set up retrievers**:
   - Vector store retriever: `vectorstore.as_retriever(search_type="similarity", search_kwargs={"k": 5})`.
   - Multi-query retriever: generates multiple query variations for better recall.
   - Contextual compression retriever: re-ranks and filters results.
   - Ensemble retriever: combines multiple retrievers (e.g., vector + BM25) with weighted fusion.
   - For LlamaIndex: `VectorStoreIndex.from_documents(docs).as_retriever(similarity_top_k=5)`.

7. **Configure output parsers**:
   - `StrOutputParser()`: Returns raw string output. Use for simple text responses.
   - `JsonOutputParser(pydantic_object=MyModel)`: Parses into a Pydantic model. Injects format instructions into the prompt.
   - `PydanticOutputParser`: Similar but with more validation options.
   - `CommaSeparatedListOutputParser`: For list outputs.
   - Always add `parser.get_format_instructions()` to the prompt so the LLM knows the expected format.
   - Handle parsing failures: wrap with `OutputFixingParser` or `RetryOutputParser`.

8. **Implement callbacks and tracing**:
   - Use LangSmith for tracing: set `LANGCHAIN_TRACING_V2=true` and `LANGCHAIN_API_KEY`.
   - Custom callbacks: extend `BaseCallbackHandler` to log events, measure latency, or send metrics.
   - Key events: `on_llm_start`, `on_llm_end`, `on_tool_start`, `on_tool_end`, `on_chain_error`.
   - Add cost tracking: log token usage per call and compute costs.

9. **Implement streaming**:
   - Use `.stream()` for LCEL chains: `for chunk in chain.stream({"input": "..."}): print(chunk)`.
   - For async: `async for chunk in chain.astream({"input": "..."}): ...`.
   - With agents: use `.stream_events()` or `astream_events()` for granular streaming of intermediate steps.
   - Forward streaming to HTTP clients via Server-Sent Events (SSE).

10. **Error handling and production readiness**:
    - Wrap LLM calls with try/except for API errors, rate limits, and timeouts.
    - Implement fallback chains: `chain.with_fallbacks([fallback_chain])`.
    - Add retry logic: `chain.with_retry(stop_after_attempt=3)`.
    - Cache LLM responses: `set_llm_cache(SQLiteCache(database_path=".langchain.db"))` for development.
    - Test chains with unit tests: mock LLM responses using `FakeLLM` or `FakeChatModel`.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
