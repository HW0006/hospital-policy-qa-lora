# Hospital Policy QA — LoRA Fine-Tune

This is a small question-answering assistant fine-tuned on hospital policy text. Specifically:

- **Base model:** Qwen2.5-0.5B (a small open LLM)
- **What we trained it to do:** given a policy passage + a question, extract the correct short answer from that passage — same skill as reading-comprehension QA
- **What it's for:** a prototype of an internal hospital "policy assistant" — staff could ask things like "what's our protocol for a fall risk patient?" and get an answer grounded in the actual policy document, instead of searching through PDFs
- **Current scope:** trained on 34 example Q&A pairs across 6 real policy topics (falls, hand hygiene, sepsis, SBAR handoff, CLABSI, pressure injuries) — a working proof of concept, not yet production-scale

## Fine-tuned model

The trained LoRA adapter is published at [huggingface.co/thumbup/qwen-hospital-policy-qa-lora](https://huggingface.co/thumbup/qwen-hospital-policy-qa-lora).

## Notebook

[`finetune_llama3_qa.ipynb`](finetune_llama3_qa.ipynb) contains the full pipeline: dataset construction, 4-bit model loading with a LoRA adapter, training, and inference testing.
