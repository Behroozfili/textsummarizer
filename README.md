# TextSummarizer

## Overview

TextSummarizer is a complete end-to-end NLP pipeline for abstractive summarization using Hugging Face models. The project includes:

- Data ingestion from a remote summarization dataset archive
- Transformation of raw text and labels for model training
- Model training with `google/pegasus-cnn_dailymail`
- Model evaluation with Rouge metrics
- REST API for training and prediction through FastAPI

## Repository Structure

- `app.py`: FastAPI server exposing `/train` and `/predict`
- `main.py`: Orchestrates pipeline stages (ingestion, transformation, training, evaluation)
- `src/textSummarizer/components`: Stage-specific components
- `src/textSummarizer/pipeline`: Orchestration pipeline classes
- `config/config.yaml`: Path and resource settings
- `params.yaml`: Hyperparameters and experiments
- `requirements.txt`: dependencies
- `Dockerfile`: container image build
- `.github/workflows/ci.yml`: GitHub Actions CI pipeline

## Quick Start

1. Clone the repo

```bash
git clone https://github.com/<your-user>/textsummarizer.git
cd textsummarizer
```

2. Install Python dependencies

```bash
pip install -r requirements.txt
```

3. Run training pipeline

```bash
python main.py
```

4. Start API service

```bash
python app.py
```

Open `http://localhost:8080/docs` for Swagger API docs.

## Prediction API

POST `/predict` with JSON payload

```json
{
  "text": "Your source text here"
}
```

Response: model-generated summary.

## Docker

Build and run with:

```bash
docker build -t textsummarizer .
docker run -p 8080:8080 textsummarizer
```

Verify service at `http://localhost:8080/docs`.

## GitHub Actions CI

- Triggers on push/pull request to `main`
- `flake8` linting
- Docker image build

## Configuration

Update `config/config.yaml` with dataset, tokenizers, and output directories. Model checkpoint and tokenizer settings are under `model_trainer`.

## Notes

- Ensure you have sufficient disk space and GPU/memory for model training.
- Tokenizer and model artifacts are stored in `artifacts/model_trainer`.
