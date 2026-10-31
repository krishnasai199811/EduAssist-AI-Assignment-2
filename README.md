# EduAssist AI: Systematic Evaluation, Token Economics, and Production Promotion of Academic LLM Prompts

**Student ID:** 2025af05073  
**Course:** Machine Learning Operations (MLOps) — AIMLZG523  
**Target Model:** Gemini 3.5 Flash Lite (`gemini-3.5-flash-lite`)  
**Tracking Server:** MLflow Tracking & Prompt Registry (`eduassist_llmops_assignment`)  

---

## 1. Project Overview
This project systematically evaluates prompt engineering iterations for an academic automated tutoring microservice. The pipeline measures:
* High-resolution inference latency (seconds).
* Input and output token distributions.
* Request-level operational costs in INR (₹6.25/1M input tokens, ₹25.00/1M output tokens).
* Downstream output schema compliance (strict JSON validation).
* Experiment tracking, artifact storage, and production alias promotion via MLflow.

---

## 2. Environment & Prerequisites

* **Python Version:** `Python 3.10` or higher (tested on `3.13.x`)
* **Package Manager:** `pip`
* **API Access:** Google Gemini API Key

### Required Libraries (`requirements.txt`)
```
google-genai>=0.1.1
python-dotenv>=1.0.0
mlflow>=2.15.0
pandas>=2.0.0
numpy>=1.24.0
```

---

## 3. Environment Variable Configuration

Set the `GEMINI_API_KEY` using any of the following methods:

### Method 1: `.env` File
Create a `.env` file in the project root directory:
```bash
echo "GEMINI_API_KEY=your_actual_gemini_api_key_here" > .env
```

### Method 2: Shell Export
```bash
export GEMINI_API_KEY="your_actual_gemini_api_key_here"
```

### Method 3: Interactive Prompt
If no environment variable or `.env` file is present, the notebook will prompt for the API key interactively using masked input.

---

## 4. Installation Commands

1. **(Optional) Set up a virtual environment:**
   ```bash
   python -m venv venv
   source venv/bin/activate       # On Windows: .\venv\Scripts\activate
   ```

2. **Install all dependencies:**
   ```bash
   pip install --upgrade pip
   pip install -r requirements.txt
   ```

---

## 5. Steps to Reproduce the Experiment

1. **Launch Jupyter:**
   ```bash
   jupyter notebook
   ```

2. **Run Evaluation Pipeline:**
   * Open `2025af05073_MLOPS_Assignment2.ipynb`.
   * Click **Kernel** $\rightarrow$ **Restart Kernel and Run All Cells...**.

3. **Execution Summary:**
   * **Cell 0–3:** Installs dependencies, initializes Gemini client, loads parameters from `config.json`, and loads test questions from `academic_data.json`.
   * **Cell 4–7 (Tasks 1 & 2):** Evaluates baseline Prompt v1, computes descriptive latency statistics, calculates token costs, and exports `latency_tokens_cost.csv`.
   * **Cell 8–9 (Task 3):** Evaluates Prompts v2 and v3, logs metrics and prompt template artifacts to MLflow (`eduassist_llmops_assignment`), assigns the `production` alias tag to Prompt v3, and exports `prompt_evaluation_results.csv`.

---

## 6. MLflow UI Command & Verification

1. **Start the MLflow Tracking Server:**
   Run the following command from the root directory where `mlruns` is located:
   ```bash
   mlflow ui --port 5000
   ```

2. **Access MLflow Dashboard:**
   Open `http://localhost:5000` in your web browser.

3. **Verify Deliverable Artifacts:**
   * Select experiment **`eduassist_llmops_assignment`**.
   * Compare metrics across `prompt_v1_evaluation`, `prompt_v2_evaluation`, and `prompt_v3_evaluation`.
   * Inspect `prompt_v3_evaluation` to verify the logged `prompt_v3_template.txt` artifact, the `commit_message` tag, and the `alias: production` tag.

---

## 7. Submission Package Structure

```text
2025af05073_MLOps_Assignment2.zip
├── 2025af05073_MLOPS_Assignment2.ipynb    # Executed notebook with outputs and Markdown analyses
├── 2025af05073_MLOps_Assignment2.pdf      # Final analysis report (500–700 words)
├── README.md                              # Setup, execution, and reproduction guide
├── requirements.txt                       # Python dependencies
├── config.json                            # Model pricing and tracking configuration
├── academic_data.json                     # Evaluation dataset and prompt templates
├── latency_tokens_cost.csv                # Baseline query execution data (Task 1 & 2)
├── prompt_evaluation_results.csv          # Comparative prompt metrics (Task 3)
└── screenshots/                           # MLflow verification screenshots
    ├── 1_experiment_overview.png
    ├── 2_metrics_table.png
    ├── 3_run_comparison.png
    ├── 4_prompt_v3_artifacts_and_commits.png
    └── 5_production_alias.png
```