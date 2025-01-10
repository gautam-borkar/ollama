# ollama

## Running Ollama Locally in 4 Steps

#### 1. Setting Up Ollama

#### 2. Docker

##### Install Ollama without a GPU
If you want to run using your CPU, which is the simplest way to get started, then run this command:

```bash
docker run -d -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
```

This will run a docker container with Ollama, map a volume for the models that we’re going to use and map port (11434) that we can connect to from the front-end.

#### Running Ollama Web-UI
According to the documentation, we will run the Ollama Web-UI docker container to work with our instance of Ollama. There are other ways, like using docker-compose, which you can see in the docs.

```bash
docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v ollama-webui:/app/backend/data --name ollama-webui --restart always ghcr.io/ollama-webui/ollama-webui:main
```

This command will among other things, run the Ollama Web-UI container named “ollama-webui”, map the container port 8080 to the host port 3000 and map a volume to store files persistently.

You can test it by going to http://127.0.0.1:3000/
Create an account (it’s all local) by clicking “sign up” and log in.

## REST API
Ollama has a REST API for running and managing models.

Generate a response
```bash
curl http://localhost:11434/api/generate -d '{
  "model": "llama3.2",
  "prompt":"Why is the sky blue?"
}'
Chat with a model
curl http://localhost:11434/api/chat -d '{
  "model": "llama3.2",
  "messages": [
    { "role": "user", "content": "why is the sky blue?" }
  ]
}'
```