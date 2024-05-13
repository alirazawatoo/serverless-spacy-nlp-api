# Serverless spaCy NLP API

A Flask API designed for AWS Lambda that downloads spaCy models from S3 at runtime, avoiding the Lambda deployment-package size ceiling.

## Runtime path

```text
HTTP request -> Flask handler -> model manager -> S3 model cache -> spaCy pipeline -> JSON
```

## Local setup

```bash
pipenv install --dev
pipenv shell
pytest
./run_local.sh
```

Configure `S3_BUCKET`, the small/medium model keys, Flask environment, and optional Sentry DSN locally. `zappa_settings.json` and `serverless.yml` are deployment examples and must be reviewed for your own account and buckets.

## Tradeoffs

- Model download and initialization can increase cold-start latency.
- Lambda memory and ephemeral storage constrain model size and concurrency.
- NLP output is model-dependent and should not be treated as authoritative without task-specific evaluation.
