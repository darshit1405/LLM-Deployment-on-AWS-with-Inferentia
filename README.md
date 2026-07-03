# Deploying Cost-Efficient LLM APIs on AWS SageMaker Using Inferentia Accelerators

Deploy and serve LLMs like **LLaMA 3** on **Amazon SageMaker** and expose them through a **serverless API** using **AWS Lambda + API Gateway**. This solution is scalable, cost-effective, and production-ready.

---

## Highlights

-  **Fast Inference**: Deploy optimized Hugging Face models with inferentia
-  **Serverless API**: Lambda-backed API for real-time predictions
-  **Fully Serverless**: No need to manage infrastructure
-  **Production-Ready**: SAM template with IAM, tracing, and logging

---

## AWS Inferentia Advantages
#### AWS Inferentia :

- Custom-built AWS chips optimized for ML inference
- Up to 2.3× higher throughput than comparable GPUs
- Up to 70% lower cost per inference
- Optimized for large language models through the AWS Neuron SDK




## Architecture Overview

```
Client → API Gateway → Lambda → SageMaker (LLM Endpoint)
```

---

## Prerequisites

- AWS CLI + IAM user/role
- AWS SAM CLI
- Python 3.12+
- Hugging Face account & access token

---

## Environment Variables

The Lambda function expects:

 - SAGEMAKER_ENDPOINT: Name of your SageMaker endpoint

## API Endpoint Setup

### Deploy with AWS SAM

```bash
sam build
sam deploy --guided
```

After deployment, you’ll receive an endpoint like:

```
https://{api-id}.execute-api.{region}.amazonaws.com/Prod/predict/
```

---

## Example Request

```bash
curl -X POST https://{api-id}.execute-api.{region}.amazonaws.com/Prod/predict/ \
  -H "Content-Type: application/json" \
  -d '{"input": "What is the capital of France?"}'
```

**Response**:

```json
{
  "response": [
    {
      "generated_text": "The capital of France is Paris."
    }
  ]
}
```
## Cleanup

```bash
sam delete
```