# OS2agora-Infrastructure

This repository contains the infrastructure setup for running and developing the different parts of OS2agora using Docker.

The repository is designed to make it easy to test, run, and debug individual components or the full system during development.

The frontend for employees is located in [OS2agora-Internal-UI](https://github.com/OS2agora/OS2agora-Internal-UI)  
The frontend for the public is located in [OS2agora-Public-UI](https://github.com/OS2agora/OS2agora-Public-UI)
The Api and backend is located in [OS2agora-API](https://github.com/OS2agora/OS2agora-API)

Technical documentation is located in [OS2agora-docs](https://github.com/OS2agora/OS2agora-docs)

## Required Tools

- Docker
- Docker-compose (is included in Docker for Windows)

## Getting Started

To start a given part of the solution, do the following steps:

1. [Build the required Docker Images](#building-docker-images)
2. Add the required secret files in `_config/secrets`
3. Navigate to the relevant [folder](#folders) and run the following command:
  ```
  docker-compose -f docker-compose.yml --env-file .env up -d
  ```

__NOTE:__ You may start the solution as is, but need to have access to an IdP to login as employee or citizen. The backend should further be configured to use that specific IdP.

To stop the solution, use the following command:
```
docker-compose -f docker-compose.yml --env-file .env stop
```

### Configuration

Each part of the solution has a dedicated `.env.<solution>` file, used for configurations - eg. `.env.api`. Configuration details for each core component are documented in that component’s own repository. This repository only provides the infrastructure needed to run those components, not their internal configuration instructions.

When running parts of the solution through an IDE or similar, make sure it has the correct configurations, allowing communication with the parts running in Docker.

### Building Docker Images

To build the required images, follow these steps:

1. Navigate to the relevant repository:
    - [OS2agora-Internal-UI](https://github.com/OS2agora/OS2agora-Internal-UI)
      - _agora-fe\_internal_
    - [OS2agora-Public-UI](https://github.com/OS2agora/OS2agora-Public-UI)
      - _agora-fe\_public_
      - _agora-fe\_public\_nginx_
    - [OS2agora-API](https://github.com/OS2agora/OS2agora-API)
      - _agora-api_
2. From the root, navigate to `/docker`
3. Run the following command:
  ``` bash
    $ docker-compose -f docker-compose.build.yml build
  ```

## Folders
### Base
Docker Compose configurations that start the base services required to run the backend from an IDE.

- __Required secrets:__
  - _db\_name_
  - _db\_username_
  - _db\_password_
  - _db\_root\_password_

### Frontend
Docker Compose configurations that start the necessary services (e.g., database and frontend apps), allowing the backend to be run and debugged from an IDE while still interacting with a functioning frontend.

- __Required Docker Images:__ 
  - _agora-fe\_internal_
  - _agora-fe\_public_
  - _agora-fe\_public\_nginx_
- __Required secrets:__
  - _db\_name_
  - _db\_username_
  - _db\_password_
  - _db\_root\_password_

### Backend
Docker Compose configurations that start the backend dependencies, making it possible to run and debug the frontend against a real backend environment.

- __Required Docker Images:__ 
  - _agora-api_
- __Required secrets:__
  - _db\_name_
  - _db\_username_
  - _db\_password_
  - _db\_root\_password_
  - _ConnectionStrings\_\_DefaultConnection_

### OS2agora
Docker Compose configurations for running the entire solution end-to-end in Docker

- __Required Docker Images:__ 
  - _agora-api_
  - _agora-fe\_internal_
  - _agora-fe\_public_
  - _agora-fe\_public\_nginx_
- __Required secrets:__
  - _db\_name_
  - _db\_username_
  - _db\_password_
  - _db\_root\_password_
  - _ConnectionStrings\_\_DefaultConnection_
