# PPTAgent with Docker

This guide explains how to run PPTAgent using Docker Compose.

## Prerequisites

- Docker and Docker Compose installed on your system
- An OpenAI API key (required for PPTAgent's LLM functionality)

## Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/icip-cas/PPTAgent.git
   cd PPTAgent
   ```

2. Create a `.env` file with your OpenAI API key:
   ```bash
   cp .env.example .env
   ```
   Then edit the `.env` file and replace `your_openai_api_key_here` with your actual OpenAI API key.

## Running PPTAgent

Start the services:
```bash
docker-compose up -d
```

This will:
- Build the Docker image if it doesn't exist
- Start the PPTAgent container with both frontend and backend services
- Mount the current directory to the container
- Create a persistent volume for generated presentations

## Accessing PPTAgent

- Frontend UI: http://localhost:8088
- Backend API: http://localhost:9297

## Using GPU Support

If you have an NVIDIA GPU and want to use it with PPTAgent, uncomment the GPU-related lines in the `docker-compose.yml` file:

```yaml
deploy:
  resources:
    reservations:
      devices:
        - driver: nvidia
          count: 1
          capabilities: [gpu]
```

Make sure you have NVIDIA Container Toolkit installed on your system.

## Data Persistence

All generated presentations are stored in a Docker volume named `pptagent_data`. This ensures your work is preserved even if you stop or remove the container.

## Stopping PPTAgent

To stop the services:
```bash
docker-compose down
```

To stop and remove volumes:
```bash
docker-compose down -v
```

## Updating PPTAgent

To pull the latest changes from the repository when starting:

1. Edit the `docker-compose.yml` file and change `PULL=False` to `PULL=True`
2. Restart the services:
   ```bash
   docker-compose down
   docker-compose up -d
   ```

## Troubleshooting

- If you encounter permission issues, ensure your user has access to Docker.
- Check the logs for any errors:
  ```bash
  docker-compose logs -f
  ``` 