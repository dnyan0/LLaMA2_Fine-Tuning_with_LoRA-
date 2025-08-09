# Model Training Report
## Project Title: Fine-Tuning LLaMA2 with PEFT (LoRA)

### Model and Dataset Overview:
- **Base Model:** LLaMA2 (Causal Language Model)
- **PEFT Strategy:** LoRA (Low-Rank Adaptation)
- **Model Wrapper:** PeftModelForCausalLM from Hugging Face + PEFT
- **Train Set Size:** 1024
- **Data Type:** Instruction-style text prompts
- **Tokenization:** Using LLaMA tokenizer with padding & truncation

### Training Configuration:
- **Trainer API:** Hugging Face Trainer
- **Epochs:** 8
- **Batch Size:** 2
- **Gradient Accumulation Steps:** 8
- **Learning Rate:** 2e−5
- **Optimizer:** paged_adamw_32bit
- **Scheduler:** Cosine learning rate scheduler with a warmup ratio of 0.03.
- **Mixed Precision:** Enabled (fp16=True)
- **Evaluation Strategy:** Per epoch
- **Save Strategy:** Per epoch, keeping only the best model based on validation loss.
- **Logging Strategy:** Logging every 25 steps to TensorBoard.
- **Model Saving Path:** ./lora-llama2

### Training & Evaluation Results:
The provided training logs show the validation loss decreasing consistently over 8 epochs, but the training loss is not available in the logs.

| Epoch | Training Loss | Validation Loss |
|-------|---------------|-----------------|
| 1     | No log        | 2.648786        |
| 2     | No log        | 2.647565        |
| 3     | No log        | 2.645788        |
| 4     | No log        | 2.643990        |
| 5     | No log        | 2.642573        |
| 6     | No log        | 2.641841        |
| 7     | No log        | 2.641424        |
| 8     | No log        | 2.640921        |

**Final Training Loss:** No log available.  
**Final Validation Loss:** ≈2.6409 (at epoch 8)

### Observations & Improvements:
- **Consistent Convergence:** The validation loss steadily decreases from epoch 1 to epoch 8, indicating that the model is learning from the dataset and converging well.
- **Learning Rate and Scheduler:** The use of a lower learning rate (2e−5) and a cosine learning rate scheduler is a good practice for stable fine-tuning, preventing the model from overshooting the optimal parameters.
- **No Training Loss:** The provided data lacks training loss metrics, which is crucial for monitoring for overfitting. If the training loss were to drop significantly while the validation loss plateaus or increases, it would be a clear sign of overfitting.
- **Suggested Improvement:** To get a complete picture, the logging should be adjusted to display the training loss. The `logging_strategy` is set to `"steps"`, but the provided table only shows epoch-based metrics. Ensuring the training loss is logged and monitored would provide valuable insights into the model's performance and help confirm whether it is truly converging or starting to overfit.
