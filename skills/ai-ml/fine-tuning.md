---
description: Configure model fine-tuning with training data preparation, hyperparameters, monitoring, evaluation, and deployment
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in fine-tuning language models. When setting up or running fine-tuning, follow these steps:

1. **Determine if fine-tuning is necessary**:
   - Fine-tune when: you need consistent output formatting, domain-specific behavior, reduced latency (smaller model matching larger model quality), or cost reduction at scale.
   - Do NOT fine-tune when: prompt engineering or RAG can achieve the same result. Start with few-shot prompting and RAG first — fine-tuning is a last resort.
   - Define success criteria: what metric improvement justifies the cost of fine-tuning?

2. **Prepare training data**:
   - **OpenAI format**: JSONL file with `{"messages": [{"role": "system", "content": "..."}, {"role": "user", "content": "..."}, {"role": "assistant", "content": "..."}]}` per line.
   - **LoRA/QLoRA format**: Depends on the framework. For HuggingFace: dataset with `text` or `instruction`/`input`/`output` columns.
   - Minimum 50-100 examples for OpenAI, 200-1000+ for LoRA/QLoRA depending on task complexity.
   - Ensure diversity: cover all task variations, edge cases, and output formats.
   - Quality over quantity: every example should be a perfect demonstration of desired behavior.
   - Split: 80% training, 20% validation. Never include test data in training.

3. **Data quality checklist**:
   - Verify JSON format: `python -m json.tool < data.jsonl` or validate each line.
   - Check for duplicates and near-duplicates — remove them.
   - Ensure consistent formatting across all examples.
   - Verify assistant responses are high-quality and match your desired output.
   - Check token counts: identify outliers that may need truncation.
   - For OpenAI: run `openai tools fine_tunes.prepare_data` for automated validation.

4. **Configure OpenAI fine-tuning**:
   - Upload training file: `client.files.create(file=open("train.jsonl", "rb"), purpose="fine-tune")`.
   - Create fine-tuning job: `client.fine_tuning.jobs.create(training_file=file_id, model="gpt-4o-mini-2024-07-18", hyperparameters={"n_epochs": 3})`.
   - Hyperparameters: `n_epochs` (1-10, start with 3), `learning_rate_multiplier` (default auto), `batch_size` (default auto).
   - Monitor: `client.fine_tuning.jobs.list_events(fine_tuning_job_id=job_id)`.
   - The fine-tuned model name is returned upon completion.

5. **Configure LoRA/QLoRA fine-tuning** (open-source models):
   - Install: `transformers`, `peft`, `bitsandbytes`, `trl`, `datasets`.
   - Load base model with quantization (QLoRA): `BitsAndBytesConfig(load_in_4bit=True, bnb_4bit_quant_type="nf4", bnb_4bit_compute_dtype=torch.bfloat16)`.
   - Configure LoRA: `LoraConfig(r=16, lora_alpha=32, target_modules=["q_proj", "v_proj", "k_proj", "o_proj"], lora_dropout=0.05, task_type="CAUSAL_LM")`.
   - Set training arguments: `learning_rate=2e-4`, `num_train_epochs=3`, `per_device_train_batch_size=4`, `gradient_accumulation_steps=4`, `warmup_ratio=0.03`, `fp16=True`.
   - Use `SFTTrainer` from `trl` for supervised fine-tuning with proper chat template formatting.
   - Use `peft.prepare_model_for_kbit_training(model)` before adding LoRA adapters.

6. **Monitor training metrics**:
   - Track training loss and validation loss per step/epoch.
   - Watch for overfitting: validation loss increasing while training loss decreases.
   - Stop early if validation loss plateaus for 2+ epochs.
   - Log to Weights & Biases or TensorBoard for visualization.
   - Check gradient norms — spikes indicate training instability.

7. **Evaluate the fine-tuned model**:
   - Run the model on a held-out test set not used during training.
   - Compare against the base model (with equivalent prompting) on the same test set.
   - Measure: task accuracy, output format compliance, response quality (human evaluation), and latency.
   - Check for regression: does the model still handle general tasks outside the fine-tuning domain?
   - Test edge cases and adversarial inputs.

8. **Deploy the fine-tuned model**:
   - **OpenAI**: Use the fine-tuned model ID directly in API calls. No additional deployment needed.
   - **LoRA**: Merge adapters with base model using `model.merge_and_unload()`, then save. Or serve with the adapter separately using vLLM or TGI.
   - **Quantized deployment**: Use GPTQ, AWQ, or GGUF format for efficient serving.
   - Serve with: vLLM (high throughput), TGI (HuggingFace), or Ollama (local).
   - Monitor production performance and retrain periodically as requirements evolve.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
