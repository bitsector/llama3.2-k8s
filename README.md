
# Llama 3.2 on Google Kubernetes Engine (GKE)
This project demonstrates how to deploy and interact with a containerized Llama 3.2 Large Language Model (LLM) on Google Kubernetes Engine (GKE). It provides a simple way to set up your own AI service that can generate text, answer questions, and perform various language tasks.
Key Features
Deploy Llama 3.2 LLM on GKE
Expose the service to the internet
Interact with the model using HTTP requests
The project includes step-by-step instructions for deployment and usage, making it easy to run your own LLM service on Kubernetes infrastructure.

Have a k8s cluster ready - it should probably have 8vCPU, 16GB RAM, 100GB Disk.

# Deploy the service
kubectl apply -f deployment.yaml

# Get the external IP of the service
kubectl get service llama-service --output=jsonpath='{.status.loadBalancer.ingress[0].ip}:{.spec.ports[0].port}'

# Make a curl call to the service
curl http://EXTERNAL_IP:80/api/generate \
  -H "Content-Type: application/json" \
  -d '{
    "model": "llama2",
    "prompt": "Why is the sky blue?"
  }'

# Sample response
{
  "model":"llama2",
  "created_at":"2024-12-28T09:47:34.049121327Z",
  "response":"The",
  "done":false
}
{
  "model":"llama2",
  "created_at":"2024-12-28T09:47:35.894942437Z",
  "response":" sky",
  "done":false
}
{
  "model":"llama2",
  "created_at":"2024-12-28T09:47:37.733627698Z",
  "response":" appears",
  "done":false
}
...
