# HCDD 412 Week 7 - Local IaC with Docker Compose

## Overview

This project uses Docker Compose to create a local application environment as code. The setup includes an nginx web server, an Ollama AI service, a private Docker network, and a named volume for the AI model. The same `compose.yaml` file is used to create both a development environment and a staging environment. The main differences between the two are defined in `dev.env` and `staging.env`, which allows the same configuration to be reused without having to create separate Compose files.

## How to Run the Project

First, validate the development configuration:

`docker compose -p hcdd412-dev --env-file dev.env config`

Preview the deployment before applying any changes:

`docker compose -p hcdd412-dev --env-file dev.env up -d --dry-run`

Deploy the development environment:

`docker compose -p hcdd412-dev --env-file dev.env up -d`

Deploy the staging environment:

`docker compose -p hcdd412-staging --env-file staging.env up -d`

Development web server:

http://localhost:8080

Staging web server:

http://localhost:8081

## Drift and Compose Limitations

The experiments showed that Docker Compose can detect some changes, but it does not detect every type of drift. For example, when I deleted the development web container, Compose noticed that it was missing and recreated it. However, when I manually changed the memory limit of the running container, Compose did not automatically detect the difference between the live container and the configuration file. The snowflake experiment showed another limitation. A container created manually outside of Compose can continue running without being managed by the Compose project. This can cause the actual environment to become different from what is documented in the Compose file. Path A provides stronger drift detection because cloud IaC tools such as Bicep or Terraform can compare the declared configuration against the actual cloud environment. So a what-if or plan preview can show planned changes against the live environment, while Docker Compose dry-run does not detect every type of runtime drift.drift. This also connects to the AWS outage reading because it showed how dependent many applications and services are on shared cloud infrastructure. The outage affected websites, banking services, airlines, social media, and other systems when AWS experienced connectivity and API issues. This shows why infrastructure should be consistent, documented, and easier to reproduce or recover when something goes wrong.

## AI Service Proof of Concept

To verify that the AI service was working correctly, I tested the local Ollama service running in Docker with a simple sentiment analysis request.

**Prompt:**

Classify the sentiment as positive, negative or neutral. Answer with one word. Text: The deployment finished cleanly and the team is thrilled.

**Response:**

Positive

The response matched what I expected because the sentence has a clearly positive tone. This confirmed that the local AI service was running correctly, could accept a prompt, and could return a usable response. this service would sit behind the inference boundary. The application would pass input to the AI service, the service would process it, and the result would then be returned to the application. Because the model is running locally, no API keys or other secrets are required to connect to it.
