# Api in Express with Jenkins configuration

A minimal Node.js/Express web application with a Jenkins CI/CD pipeline for automated build and deployment.

## Overview

This project demonstrates how to integrate a simple Express.js application with a Jenkins pipeline. The pipeline automatically checks out the code, installs dependencies, starts the server, and verifies the endpoint is responding.

## Requirements

- Node.js >= 18
- Jenkins with the NodeJS plugin configured (tool name: `NODE25`)

## Project Structure

```
.
├── app.js          # Express application
├── Jenkinsfile     # Jenkins pipeline definition
└── package-lock.json
```

## Application

The app runs on port `3000` and exposes a single endpoint:

| Method | Path     | Response       |
|--------|----------|----------------|
| GET    | `/hello` | `Hello world`  |

### Running Locally

```bash
npm install
node app.js
```

Then test it:

```bash
curl http://localhost:3000/hello
```

## Jenkins Pipeline

The `Jenkinsfile` defines a declarative pipeline with the following stages:

1. **Checkout Code** — Clones the repository from SCM.
2. **Install Dependencies** — Initializes the project and installs Express.
3. **Run App** — Starts the app in the background and verifies it responds via `curl`.

### Pipeline Parameters

| Parameter     | Description                              |
|---------------|------------------------------------------|
| `CUSTOM_PORT` | Port used by `curl` to verify the app (default behavior uses `3000` in the app) |

### Post Actions

The pipeline always prints a cleanup message after execution, regardless of success or failure.

## Dependencies

| Package   | Version  |
|-----------|----------|
| express   | ^5.2.1   |
