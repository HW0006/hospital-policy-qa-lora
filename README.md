# Hospital Policy QA — LoRA Fine-Tune

A small question-answering assistant for hospital staff, fine-tuned to answer questions about a policy using only the policy text it is given.

- **Base model:** [Qwen2.5-0.5B-Instruct](https://huggingface.co/Qwen/Qwen2.5-0.5B-Instruct), loaded in 4-bit
- **Method:** LoRA adapter on the attention layers (r = 16), trained on a free Colab T4 GPU
- **Task:** given a policy passage and a question, give the short answer from that passage (reading-comprehension QA)
- **What it's for:** a prototype of an internal hospital policy assistant. Staff could ask "What Braden score means a patient is at risk?" and get an answer grounded in the actual policy document, instead of searching through PDFs.

## Data

34 question-answer pairs written from public guidance on six topics:

| Topic | Source | Pairs |
| --- | --- | --- |
| Fall prevention | CDC STEADI, AHRQ Fall TIPS | 8 |
| Central-line infection (CLABSI) prevention | CDC | 6 |
| Hand hygiene | WHO My Five Moments | 5 |
| Sepsis recognition | CDC Get Ahead of Sepsis | 5 |
| SBAR handoff communication | AHRQ / TeamSTEPPS | 5 |
| Pressure-injury prevention | AHRQ toolkit | 5 (held out for testing) |

## How it is tested

The pressure-injury topic is held out completely: the model never sees that passage or its questions during training. The notebook asks the **base model** those 5 questions, fine-tunes on the other 29 pairs, then asks again. It reports exact match and token F1 (the standard reading-comprehension QA metrics) with both sets of answers side by side.

Results are in the last section of the notebook.

## Run it

Open [`hospital_policy_qa_lora.ipynb`](hospital_policy_qa_lora.ipynb) in Google Colab, choose a T4 GPU runtime and run all cells. It takes a few minutes.

## Fine-tuned adapter

[huggingface.co/thumbup/qwen-hospital-policy-qa-lora](https://huggingface.co/thumbup/qwen-hospital-policy-qa-lora). This adapter was trained with an earlier version of the notebook.

## Limits

- 34 examples and a 0.5B model: a proof of concept, not a production assistant.
- 5 test questions from one topic, so one answer can move the score a lot.
- Not for clinical use. A real version would need the hospital's own policies, a much larger evaluation set and staff review against the source document.

Built with help from an AI assistant (Claude).
