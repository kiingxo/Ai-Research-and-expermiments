# Models

Storage and management of model checkpoints, configurations, and metadata.

## Organization

```
models/
├── checkpoints/
│   ├── llama-7b-finetuned-v1/
│   ├── bert-sentiment-classifier/
│   └── gpt2-essay-generator/
│
├── configs/
│   ├── finetuning_config.yaml
│   ├── training_config.yaml
│   └── inference_config.yaml
│
└── README.md
```

## Model Naming Convention

Use descriptive names:
```
{base_model}-{task}-{variant}-{version}

Examples:
- llama-7b-conversational-lora-v1
- bert-base-sentiment-full-v2
- gpt2-summarization-peft-v1
```

## Checkpoint Structure

Each model checkpoint should include:

```
model_name/
├── config.json          # Model configuration
├── pytorch_model.bin    # Model weights (or .safetensors)
├── tokenizer.json       # Tokenizer files
├── tokenizer_config.json
├── special_tokens_map.json
├── training_args.bin    # Training configuration
└── README.md           # Model card
```

## Model Card Template

Create `README.md` for each model:

```markdown
# Model Name

## Description
Brief description of what the model does

## Training Details
- Base model: 
- Dataset:
- Training time:
- Hardware:

## Performance
- Metric: Score
- Benchmark: Result

## Usage
```python
from transformers import AutoTokenizer, AutoModelForCausalLM

model_id = "path/to/model"
tokenizer = AutoTokenizer.from_pretrained(model_id)
model = AutoModelForCausalLM.from_pretrained(model_id)
```

## Limitations
- Known issues
- Domain restrictions
- Bias considerations

## License
Model license information
```

## Storage Guidelines

- **Large files**: Use Git LFS or external storage
- **Organize by project**: Group related models
- **Version clearly**: Use semantic versioning
- **Document training**: Include hyperparameters
- **Track improvements**: Document performance gains

## Checkpoint Management

```python
# Saving checkpoints during training
from transformers import Trainer

trainer = Trainer(
    args=TrainingArguments(
        output_dir="./models/checkpoints/model-v1",
        save_strategy="epoch",
        load_best_model_at_end=True,
    )
)
trainer.train()

# Loading a checkpoint
model = AutoModelForCausalLM.from_pretrained(
    "./models/checkpoints/model-v1/checkpoint-500"
)
```

## Inference Best Practices

- Test models after training
- Document inference time
- Record memory usage
- Create inference scripts
- Version inference code separately

## See Also
- [Training Techniques](../concepts/3-training-techniques/)
- [Frameworks & Tools](../concepts/4-frameworks/)
- [Projects](../projects/)
