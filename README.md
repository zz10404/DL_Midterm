# DL_Midterm

Because of large model sizes and Colab notebook rendering issues, the project is stored in Google Drive and linked below.



## Structure

```
DL_Midterm
│
├── Version2 
│   ├── Version2_1
│   ├── Version2_2
│   ├── Version2_3
│   └── Version2_4
│
└── Version3 
    ├── Version3_1
    ├── Version3_2
    ├── Version3_3
    ├── Version3_4
    ├── Version3_6
    └── Version3_final 
        │
        ├── Midterm_version3_final.ipynb
        ├── loss_history.csv      
        ├── submission.csv        
        └── llama3_8b_math_verifier_checkpoint_version3_final
```

## Version 1
- run starter notebook

## Version 2
**increase dataset:**

- training data = 20000
- validation data = 2000

**increase lora rank:**

- r = 16
- lora_alpha = 32
- lora_dropout = 0

**trainer setup:**

- per_device_train_batch_size = 2
- gradient_accumulation_steps = 4
- warmup_steps = 50
- max_steps = 500
- learning_rate = 2e-4
- lr_scheduler_type = "linear"
---
- **try different prompt word template**

### Version 2_1

```
training_prompt = """You are an expert mathematician and you are tasked with verifying the correctness of solutions to math problems.

Your task: Carefully analyze the given solution and determine if it is correct.

Verification steps:
1. Check if the mathematical operations are correct
2. Verify the logical reasoning is sound
3. Confirm the final answer matches the solution steps

Respond with ONLY one word:
- 'True' if the solution is completely correct
- 'False' if there are any errors

Question:
{}

Solution:
{}

Your verdict:
{}"""
```

### Version 2_2

```
training_prompt_v2 = """[INSTRUCTION]
You are a mathematics verification system. Your ONLY task is to output True or False.

[INPUT]
Question: {}
Solution: {}

[RULES]
- Output "True" if the solution is mathematically correct
- Output "False" if there are any errors
- Do NOT provide explanations

[OUTPUT]
{}"""
```

### Version 2_3

```
training_prompt_v3 = """Task: Verify this mathematical solution step-by-step.

Question: {}

Solution to verify:
{}

Verification process:
1. Read the question
2. Check each calculation step
3. Verify the logic flow
4. Confirm the final answer

Decision: Is this solution correct?
Output only: True or False
Decision: {}"""
```

### Version 2_4

- **Select training_prompt of version 2_1**

---

- **Generate balanced datasets**

  - Shuffle the entire dataset, divide the data into categories, and draw equal amounts of samples from both categories.

  - Then, draw an equal number of validation samples from the remaining samples.

  - dataset:

    train_samples_per_class = 10000

    val_samples_per_class = 500

- **per_device_train_batch_size = 2 -> 4**

## Version 3

- **Version 2_4 learning_rate = 2e-4**
- **try different learning_rate**

---

### Version 3_1

- learning_rate = 1e-4

### Version 3_2

- learning_rate = 3e-4

### Version 3_3

- **select learning_rate = 2e-4**

---

- **try lr_scheduler_type = "cosine"**

### Version 3_4

- **still select lr_scheduler_type = "linear"**

---

**change lora:**

- r = 32
- lora_alpha = 64
- lora_dropout = 0.05

### Version 3_6

**increase dataset:**

- train_samples_per_class = 30000
- val_samples_per_class = 500

**lora:**

- r = 32
- lora_alpha = 64
- lora_dropout = 0.05

**trainer setup:**

- per_device_train_batch_size = 4

- gradient_accumulation_steps = 4

- num_train_epochs = 1

- warmup_steps = 150

- learning_rate = 2e-4

  lr_scheduler_type = "linear"

- EarlyStoppingCallback(early_stopping_patience=3, early_stopping_threshold=5e-4)

- logging_steps = 100,

  eval_strategy = "steps"

  eval_steps = 100

  save_strategy = "steps"

  save_steps = 100

  save_total_limit = 2

### Version 3_final

**increase dataset:**

- train_samples_per_class = 50000
- val_samples_per_class = 1000
