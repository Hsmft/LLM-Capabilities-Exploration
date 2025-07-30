# Exploring LLM and VLM Capabilities: A Multi-Task Evaluation

![Language](https://img.shields.io/badge/language-Python-blue.svg)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This project systematically evaluates and compares the capabilities of a text-only Large Language Model (LLM) and a Vision-Language Model (VLM) across five distinct generative AI tasks. The primary methodology is prompt engineering, using the Ollama framework to interact with the models.

---

## 📋 Models & Setup

Two 3-billion-parameter models were selected for this comparative analysis:

| Model Role | Name | Quantization |
| :--- | :--- | :--- |
| **Text-Only LLM** | `llama3.2:3b` | Q8_0 |
| **Vision-Language Model**| `qwen2.5vl:3b` | Q4_K_M |

The project was implemented in Python using a Jupyter Notebook, with key libraries including **Ollama**, **llama-cpp-python** (for perplexity calculation), **Pandas**, and various evaluation libraries like **ROUGE-Score** and **pycocoevalcap**.

---

## 🚀 Tasks and Methodology

The models were prompted to perform five different tasks to test their capabilities in text generation, comprehension, and multimodal reasoning.

1.  **Automatic Story Generation:** Generated 10 diverse short stories by varying genres and decoding temperatures. Performance was measured by calculating the **Perplexity** of the generated text.
2.  **Abstractive Text Summarization:** Each generated story was summarized by its respective model. Performance was evaluated using the **ROUGE-1 F1 Score**.
3.  **Natural Language Inference (NLI):** A three-way classification task (entailment, contradiction, neutral) performed on the SNLI/MultiNLI dataset. Performance was measured by **Classification Accuracy**.
4.  **Image Captioning:** The VLM (`qwen2.5vl:3b`) generated captions for images from the COCO Captions dataset. Performance was evaluated using the **CIDEr** metric against human-written captions.
5.  **Visual Question Answering (VQA):** The VLM answered multiple-choice math questions based on images from the MATH-Vision dataset. Performance was measured by **Exact Match (EM) Accuracy**.

---

## 📊 Evaluation Results & Key Findings

The final performance of the models on each task is summarized below.

| Task | Model | Metric | Score | Avg. Inference Time (s/item) | Reject Rate (%) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Story Gen.** | `llama3.2:3b` | Perplexity | 2.97 | 66.19s | 0.00% |
| | `qwen2.5vl:3b` | Perplexity | **2.62** | 72.44s | 0.00% |
| **Summarization** | `llama3.2:3b` | ROUGE-1 F1| 0.4667 | 40.72s | 0.00% |
| | `qwen2.5vl:3b`| ROUGE-1 F1| **0.5630** | 73.19s | 0.00% |
| **NLI** | `llama3.2:3b` | Accuracy | 56.00% | 16.13s | 0.00% |
| | `qwen2.5vl:3b` | Accuracy | **75.76%** | 32.87s | 1.00% |
| **Image Capt.** | `qwen2.5vl:3b` | CIDEr | 0.1721 | 67.40s | 0.00% |
| **VQA** | `qwen2.5vl:3b` | EM Accuracy| 27.00% | 115.62s | 0.00% |

### Key Findings
* The **`qwen2.5vl:3b` model consistently outperformed `llama3.2:3b`** on all text-based tasks, achieving better perplexity, summarization, and NLI scores.
* On multimodal tasks, the Qwen VLM demonstrated a **foundational capability for visual reasoning**, scoring better than random chance (20%) on the difficult MATH-Vision VQA dataset.
* Careful **prompt engineering** proved highly effective, resulting in a 0% reject rate for the complex VQA task.

---

## 🔧 How to Run

1.  **Clone the repository.**
2.  **Install dependencies** from the `requirements.txt` file.
3.  **Download Models:** Use Ollama to pull the required models (`ollama pull llama3.2:3b` and `ollama pull qwen2.5vl:3b`). You will also need to download the GGUF model files for perplexity calculations and place them in a `models` directory.
4.  **Prepare Datasets:** Download the required datasets and place them in their respective directories (`nli`, `ic`, `vqa`).
5.  **Execute the Analysis:** Open and run the cells in the `main.ipynb` Jupyter Notebook.

---

## 📄 License
This project is licensed under the MIT License.