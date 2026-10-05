# HCDD 412 Week 7 - Local IaC with Docker Compose

## Overview

This project uses Docker Compose to create a local application environment as code. The setup includes an nginx web server, an Ollama AI service, a private Docker network, and a named volume for the AI model. The same compose.yaml file is used to create both a development environment and a staging environment. The main differences between the two environments are defined in dev.env and staging.env.

## How to Run the Project

Validate the development configuration:

docker compose -p hcdd412-dev --env-file dev.env config

Preview the deployment:

docker compose -p hcdd412-dev --env-file dev.env up -d --dry-run

Deploy the development environment:

docker compose -p hcdd412-dev --env-file dev.env up -d

Deploy the staging environment:

docker compose -p hcdd412-staging --env-file staging.env up -d

Development web server:

http://localhost:8080

Staging web server:

http://localhost:8081

## Drift and Compose Limitations

<<<<<<< HEAD
The drift experiments showed that Docker Compose can detect some changes, but it does not detect every type of drift. When I deleted the development web container, Compose noticed that it was missing and recreated it. However, when I manually changed the memory limit of the running container, Compose did not automatically detect the difference between the live container and the configuration file. The snowflake experiment also showed that a container created manually outside of Compose can continue running without being managed by the Compose project. Path A provides stronger drift detection because cloud IaC tools can compare the declared configuration against the actual environment. This connects to the AWS outage reading because it showed how dependent many applications and services are on shared cloud infrastructure. The outage affected websites, banking services, airlines, social media, and other systems when AWS experienced connectivity and API issues. This shows why keeping infrastructure consistent, documented, and easier to recover is important, especially when many services depend on the same environment.
=======
The drift experiments showed that Docker Compose can detect some changes, but it does not detect every type of drift. When I deleted the development web container, Compose noticed that it was missing and recreated it. However, when I manually changed the memory limit of the running container, Compose did not automatically detect the difference between the live container and the configuration file.

The snowflake experiment also showed that a container created manually outside of Compose can continue running without being managed by the Compose project. Path A provides stronger drift detection because cloud IaC tools can compare the declared configuration against the actual environment.

This connects to the AWS outage reading because it showed how dependent many applications and services are on shared cloud infrastructure. The outage affected websites, banking services, airlines, social media, and other systems when AWS experienced connectivity and API issues. This shows why keeping infrastructure consistent, documented, and easier to recover is important, especially when many services depend on the same environment.
>>>>>>> e062641 (Update README and Compose configuration)

## AI Service Proof of Concept

To verify that the AI service was working correctly, I tested the local Ollama service running in Docker with a simple sentiment analysis request.

**Prompt:**

Classify the sentiment as positive, negative or neutral. Answer with one word. Text: The deployment finished cleanly and the team is thrilled.

**Response:**

Positive

<<<<<<< HEAD
This result matched what I expected because the sentence has a clearly positive tone. It confirms that the service is running, can accept a prompt, and can return a usable result. This service sits behind the inference boundary, the application passes input to the service, the service processes it, and the result is returned to the application. Because the model runs locally, no API keys or other secrets are needed to connect it to the application.

This result matched what I expected because the sentence has a clearly positive tone. It confirms that the service is running, can accept a prompt, and can return a usable result. This service sits behind the inference boundary, the application passes input to the service, the service processes it, and the result is returned to the application. Because the model runs locally, no API keys or other secrets are needed to connect it to the application.
=======
This result matched what I expected because the sentence has a clearly positive tone. It confirms that the service is running, can accept a prompt, and can return a usable result. This service sits behind the inference boundary, the application passes input to the service, the service processes it, and the result is returned to the application. Because the model runs locally, no API keys or other secrets are needed to connect it to the application.
>>>>>>> e062641 (Update README and Compose configuration)
