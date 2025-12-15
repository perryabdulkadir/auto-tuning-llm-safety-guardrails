# Auto-Tuning Safety Guardrails for Black-Box Large Language Models

Code and notebooks for the paper:

> **Auto-Tuning Safety Guardrails for Black-Box Large Language Models**  
> Perry Abdulkadir

This project explores a practical way to configure safety guardrails for black-box LLM deployments by treating **safety configurations as tunable hyperparameters**. Instead of hand-tuning system prompts and content filters, we search over combinations of:

- Modular **jailbreak** and **malware** safety prompts, and  
- A **ModernBERT-based harmfulness classifier** used as a response filter,

and optimize them using both a **grid search** and a **black-box Optuna search**.

The experiments evaluate each configuration on three types of prompts:

1. **Malware prompts** (safety-critical / harmful queries)  
2. **Jailbreak prompts** from `rubend18/ChatGPT-Jailbreak-Prompts`  
3. **Benign user queries** (normal assistant interactions)

Each configuration is scored on:

- `malware_asr` – attack success rate for malware prompts  
- `malware_gen_latency` – end-to-end latency for malware generations  
- `malware_filter_latency` – latency when a malware response is filtered  
- `jailbreak_asr` – jailbreak attack success rate  
- `jailbreak_gen_latency` – latency on jailbreak generations  
- `jailbreak_filter_latency` – latency when jailbreak responses are filtered  
- `benign_harm_rate` – fraction of benign prompts incorrectly flagged as harmful  
- `benign_gen_latency` – latency for safe/benign generations  
- `benign_filter_latency` – latency when a benign response is incorrectly filtered

The key result is that **viewing guardrails as hyperparameters** lets us use standard hyperparameter optimization (HPO) tools to quickly rediscover strong safety configurations with **far fewer evaluations and much less time** than an exhaustive grid search.

## Paper

The full write-up is available in:

- `paper/autotuning_llm_safety_guardrails.pdf`
- arXiv preprint (link and ID forthcoming).
