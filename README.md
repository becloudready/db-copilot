# db-agent

[![Docker Image CI](https://github.com/db-agent/db-agent/actions/workflows/docker-image.yml/badge.svg)](https://github.com/db-agent/db-agent/actions/workflows/docker-image.yml)
[![Checkout the Website](https://img.shields.io/badge/Visit-Our%20Website-brightgreen)](https://www.db-agent.com)
[![Demo Video](https://img.shields.io/badge/Visit-Our%20Demo-red)](https://youtu.be/tt0oTIrY260)





## Demo Video

[Watch the demo video](https://youtu.be/KT84qySZw1I)


## Quickstart - launch the application with defog/llama-3-sqlcoder-8b ( TGI )

- You will need Huggingface token
- Either Intel based laptop or Nvidia GPU

```bash
export HF_TOKEN=<YOUR TOKEN>
docker compose -f docker-compose.demo.yml build
docker compose -f docker-compose.demo.yml up -d
```

## Inference Options

### Local Llama3.2 with Ollama

```
docker run -d --gpus=all -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama

docker exec -it ollama ollama run llama3.2:1b
```

### Huggingface Models ( TGI )

- defog/llama-3-sqlcoder-8b

```
# Deploy with docker on Linux:
docker run --gpus all \
	-v ~/.cache/huggingface:/root/.cache/huggingface \
 	-e HF_TOKEN=$HF_TOKEN \
	-p 8000:80 \
	ghcr.io/huggingface/text-generation-inference:latest \
	--model-id defog/llama-3-sqlcoder-8b
```
- bigscience/bloomz-560m


### Ollama 
```
docker run -d --gpus=all -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
docker exec -it ollama ollama run hf.co/defog/sqlcoder-7b-2

```
### Embedding 

```
# Use a pipeline as a high-level helper
from transformers import pipeline

messages = [
    {"role": "user", "content": "Who are you?"},
]
pipe = pipeline("text-generation", model="defog/llama-3-sqlcoder-8b")
pipe(messages)
```
