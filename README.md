# Multi-Agent UPSC Essay Evaluation System

An automated, multi-agent AI framework designed to evaluate essays across multiple core evaluation metrics. Built using **LangGraph** and **LangChain**, the system leverages a local **Ollama (Llama 3.2)** model to execute parallel analytical reviews and aggregate a final assessment.

## 🚀 Features
* **Multi-Dimensional Analysis:** Runs parallel LangGraph worker nodes to evaluate language quality, depth of analysis, and clarity of thought.
* **Structured Output Integration:** Uses Pydantic schemas to enforce exact JSON output formatting (`feedback` text and a numerical `score` out of 10) from local LLMs.
* **Intelligent Aggregation:** Utilizes a supervisor node to calculate average metric scores and compile a unified summary feedback report.

## 🏗️ Architecture Workflow
+-----------+
|   START   |
+-----+-----+
|
+----------+----------+
|                     |
v                     v
+----+---------------+ +---+----------------+
|  evaluate_language | | evaluate_analysis  |  ... (Parallel Nodes)
+----+---------------+ +---+----------------+
|                     |
+----------+----------+
|
v
+----------+----------+
|  final_evaluation   | (Aggregator)
+----------+----------+
|
v
+-----+-----+
|    END    |
+-----------+

## ⚙️ Quick Start

1. **Install Dependencies:**
   ```bash
   pip install langgraph langchain-ollama python-dotenv pydantic
   ```

2. **Pull the Local Model (Ollama):**
   ```bash
   ollama run llama3.2:1b
   ```

3. **Execution Snippet:**
   ```python
   # Initialize state input matching the Graph Schema
   initial_state = {
       'essay': "Your text essay content goes here..."
   }

   # Invoke the multi-agent graph
   final_output = workflow.invoke(initial_state)
   print("Average Score:", final_output['avg_score'])
   print("Overall Feedback:", final_output['overall_feedback'])
   ```