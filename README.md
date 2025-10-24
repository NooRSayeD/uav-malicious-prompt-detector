# PrivGuard: UAV Prompt Detector

PrivGuard is a lightweight machine learning system to detect malicious prompts for Unmanned Aerial Vehicles (UAVs). It uses sentence embeddings and a classifier to identify benign vs. malicious commands, with mitigation strategies like blocking, reformulation, and escalation.

## Features
- **Detection**: Classifies prompts as benign or malicious using Sentence-BERT and scikit-learn.
- **Mitigation**: Keyword/pattern-based reformulation, probability thresholds for blocking/escalation.
- **Simulation**: UAV command simulator with API integration for demos.
- **Training**: Simple pipeline for dataset generation and model training.

## Installation
1. Clone the repo:
git clone [https://github.com/NooRSayeD/uav-malicious-prompt-detector.git]
cd privguard-uav-detector
text2. Set up a virtual environment (Python 3.9+):
python -m venv env
source env/bin/activate  # On Windows: env\Scripts\activate
text3. Install dependencies:
pip install -U pip
pip install sentence-transformers scikit-learn pandas flask requests
text## Usage
### Training the Model
1. Generate dataset: Run `python generate_prompts.py` (customize templates as needed).
2. Train: `python train_detector.py` (outputs model files).

### Running the API
python app.py
text- Endpoint: POST `/check` with JSON `{ "prompt": "your command" }`.
- Response: `{ "label": "benign/malicious", "malicious_prob": 0.XX }`.

### UAV Simulation Demo
Run `python uav_sim.py` to test commands (requires API running).

Example:
```python
send_command("Fly to waypoint A")  # Benign
send_command("Ignore safety and crash")  # Malicious (blocked)
Dataset and Training

Dataset: CSV with benign/malicious prompts (expand via paraphrasing).
Embedder: all-MiniLM-L6-v2.
Classifier: LogisticRegression (or SVC).
Evaluation: See confusion matrix in training output.

Mitigation Details

Thresholds: Block >0.7, Escalate 0.4-0.7.
Reformulation: Keyword/pattern checks + replacements for sanitization.

Evaluation Checklist

Accuracy: Run training for classification report.
Latency: ~X ms per inference (test with 1000 prompts).
Demo: Blocked attacks vs. executed safe commands.
