## Exploring LLM Capabilities: From Storytelling to Visual QA

#### Overview
This repository contains the implementation of a project for the Natural Language Processing course (Spring 2025). The project systematically evaluates the capabilities of Large Language Models (LLMs) across five diverse tasks—from creative text generation to multimodal reasoning—using prompt engineering techniques including Few-Shot Prompting and Chain-of-Thought (CoT) Reasoning.

<code>─</code> (Box Drawing Light Horizontal - U+2500)

#### Models Used
Two quantized models were deployed via Ollama to balance performance and accessibility on consumer hardware:


phi3:3.8b (Text-only|3.8B)


qwen2.5vl:3b (Vision-Language Model(VLM)|3.8B)

<code>─</code> (Box Drawing Light Horizontal - U+2500)

#### Implemented Tasks
##### 3.1 Automatic Story Generation (ASG)
Generated 10 diverse short stories per model with varying genres (horror, sci-fi, romance, mystery, etc.)
Applied Few-Shot Prompting with genre-specific examples to guide narrative style
Controlled diversity via decoding hyperparameters (temperature ∈ [0.7, 1.2], top_p ∈ [0.9, 0.95])
Topics included space exploration, desert islands, time machines, hidden treasures, and zombie apocalypses
##### 3.2 Abstractive Text Summarization (ATS)
Produced one-sentence summaries for all 20 generated stories
Combined Chain-of-Thought reasoning with Few-Shot examples to improve paraphrasing quality
Enforced constraints: summaries must be <50 words, avoid direct copying, and capture core narrative essence
Evaluated using ROUGE-1 F1 against original stories
##### 3.3 Natural Language Inference (NLI)
Classified 100 premise-hypothesis pairs into three relationship types:
entailment: Hypothesis must be true if premise is true
contradiction: Hypothesis must be false if premise is true
neutral: Neither follows nor conflicts
Used deterministic decoding (temperature=0.1) with strict output formatting
Implemented robust parsing to extract single-word labels from model outputs
##### 3.4 Image Captioning (IC)
Generated natural language descriptions for 100 COCO images
Leveraged qwen2.5vl:3b's multimodal capabilities with base64-encoded images
Evaluated against 5 human-written reference captions per image using CIDEr metric
Ensured caption validity through length checks and content filtering
##### 3.5 Visual Question Answering (VQA)
Solved mathematical reasoning problems from MATH-Vision dataset
Each question presented as image + multiple-choice options (A–E)
Designed specialized prompt template to force single-letter answers
Implemented multi-strategy answer extraction (position-based, regex pattern matching)

<code>─</code> (Box Drawing Light Horizontal - U+2500)


#### Project Structure
```
LLm Capabilities/
├── datasets/                   # Truncated datasets (100 items each)
│   ├── nli/nli.csv           # Premise-hypothesis pairs with labels
│   ├── ic/
│   │   ├── ic.csv            # Image metadata + human captions
│   │   └── images/           # COCO images (100)
│   └── vqa/
│       ├── vqa.csv           # Math problems with options/answers
│       └── images/           # Problem diagrams (100)
├── json_outputs/             # Evaluation results and predictions
│   ├── asg_output.json       # Generated stories (with perplexity)
│   ├── ats_output.json       # Summaries (with ROUGE scores)
│   ├── nli_output_phi3.json  # NLI results (phi3)
│   ├── nli_output_qwen.json  # NLI results (qwen)
│   ├── ic_output.json        # Captions + CIDEr scores
│   └── vqa_output_full.json  # VQA predictions + accuracy
├── code.ipynb                # Complete implementation (all 5 tasks + evaluation)
└── README.md                 # This file
```
<code>─</code> (Box Drawing Light Horizontal - U+2500)
#### Setup & Requirements
##### Download required models
```
ollama pull phi3:3.8b
ollama pull qwen2.5vl:3b
```

##### Python 3.12+ with packages:
```
requests>=2.31.0
pandas>=2.0.0
numpy>=1.24.0
rouge>=1.0.1
nltk>=3.8.0
pycocoevalcap>=1.2
llama-cpp-python>=0.2.0
```
<code>─</code> (Box Drawing Light Horizontal - U+2500)

#### References
1.Jurafsky, D., & Martin, J. H. (2025). Speech and Language Processing (3rd ed.).


2.Chen, X., et al. (2015). Microsoft COCO Captions. arXiv:1504.00325.


3.Wang, K., et al. (2024). Measuring Multimodal Mathematical Reasoning with MATH-Vision. arXiv:2402.14804.


4.Bowman, S. R., et al. (2015). A Large Annotated Corpus for Learning Natural Language Inference. EMNLP.


