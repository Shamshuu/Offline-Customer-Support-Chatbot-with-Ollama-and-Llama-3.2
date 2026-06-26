# Offline Customer Support Chatbot with Ollama & Llama 3.2

An offline, privacy-first customer support chatbot for a fictional e-commerce store, **Chic Boutique**, built using **Ollama** and **Meta's Llama 3.2 (3B)** model. 

This repository evaluates the feasibility of a local language model for automating support interactions and compares **Zero-Shot** versus **One-Shot** prompting methods across 20 realistic customer scenarios.

---

## 🚀 Key Highlights & Benefits
- **Data Privacy (Offline operation)**: Customer queries, order IDs, and account names stay on local hardware, avoiding compliance risks under GDPR, CCPA, and DPDP Acts.
- **Zero API Costs**: Runs entirely locally using consumer hardware, bypassing per-token costs.
- **Lightweight Inference**: Leverages Ollama's local server and Llama 3.2 3B (quantized) for CPU/GPU efficiency.

---

## 🏗️ System Architecture & Data Flow

```
+--------------------------+
|        chatbot.py        |
|   (Your Python Script)   |
+------------+-------------+
             | 1. Format prompt with query
             | 2. Construct JSON payload
             v
+------------+-------------+
|    HTTP POST Request     |
| to http://localhost...   |
+------------+-------------+
             |
             v
+------------+-------------+
|      Ollama Server       |
|    (Running Locally)     |
+------------+-------------+
             | 3. Pass prompt to model
             v
+------------+-------------+
|     Llama 3.2 Model      |
|       (Inference)        |
+------------+-------------+
             | 4. Generate response text
             v
+------------+-------------+
|      Ollama Server       |
+------------+-------------+
             | 5. Package response in JSON
             v
+------------+-------------+
|  HTTP 200 OK Response    |
|   with generated text    |
+------------+-------------+
             | 6. Parse JSON
             | 7. Log response
             v
+--------------------------+
|     eval/results.md      |
|    (Output Log File)     |
+--------------------------+
```

---

## 📁 Repository Structure
```
Offline-Customer-Support-Chatbot-with-Ollama-and-Llama-3.2/
├── prompts/
│   ├── zero_shot_template.txt   # Instructions without examples
│   └── one_shot_template.txt    # Instructions with a return policy example
├── eval/
│   └── results.md               # Detailed query logs and scored outputs
├── chatbot.py                   # Main python orchestrator client
├── setup.md                     # Installation and setup guide
├── report.md                    # In-depth analysis comparing Zero-Shot vs One-Shot
└── README.md                    # Project overview (this file)
```

---

## 🧪 Methodology & Prompting Comparison

We selected **20 user queries** representing typical Ubuntu technical support questions and adapted them into e-commerce customer support questions (e.g. issues with checkout, shipping, returns, order status, discount codes, website navigation, accounts, etc.).

Responses were generated for both methods and graded manually on a 1-5 scale across three criteria:
- **Relevance**: How well the response answers the specific query.
- **Coherence**: Grammar, syntax, and clarity.
- **Helpfulness**: Usefulness and actionability of the instructions.

### Quantitative Summary (Averages)

| Prompting Method | Relevance (1-5) | Coherence (1-5) | Helpfulness (1-5) | Overall Average |
| --- | --- | --- | --- | --- |
| **Zero-Shot** | **5.00** | **4.95** | **4.55** | **4.83 / 5.00** |
| **One-Shot** | 4.95 | 4.80 | 4.25 | 4.67 / 5.00 |

### Key Findings
1. **Zero-Shot Performance**: For a lightweight model like Llama 3.2 3B, **Zero-Shot prompting yields better results** than One-Shot prompting.
2. **Template Leakage in One-Shot**: The 3B model is prone to overfitting to the formatting. It occasionally prints the structural prompt labels (e.g., `Customer Query: "..."`) directly into its response.
3. **Over-Refusal & Logical Contradiction**: One-Shot examples can restrict the model's logic. It refused to answer help-desk tasks when it lacked specific instructions, whereas Zero-Shot successfully simulated helpful step-by-step account settings procedures.

For a detailed analysis, read the full [Evaluation Report](file:///c:/GPP/Week15/Offline-Customer-Support-Chatbot-with-Ollama-and-Llama-3.2/report.md).

---

## 🛠️ Getting Started
Please follow the instructions in [setup.md](file:///c:/GPP/Week15/Offline-Customer-Support-Chatbot-with-Ollama-and-Llama-3.2/setup.md) to install Ollama, pull Llama 3.2, configure your environment, and execute the chatbot.