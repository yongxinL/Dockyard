# ⚓ Dockyard

A quiet harbor where HomeLab services arrive, find their place, and don’t get lost again

## What is this?

This is my HomeLab’s **dockyard** — the place where containers pull in, get documented, and stop floating around unnamed and forgotten.

Instead of half-remembered ports, mystery containers, and _“what was this for again?”_, this repo keeps track of everything running in the lab and why it exists.

## Project Structure

```
Dockyard/
├── compose/                 # Service definitions
│   └── example.yml          # Example service configuration
├── scripts/                 # Setup and utility scripts
│   └── setup.sh             # Environment setup script
├── shared/                  # Shared resources
│   └── example/
│       └── Dockerfile       # Base Dockerfile for services
├── .env.example             # Environment variables template
├── docker-compose.yml       # Main Docker Compose configuration
└── README.md                # This file
```

## Prerequisites

- Docker and Docker Compose
- OpenSSL (for secret generation)
- Git

## Setup

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd Dockyard
   ```

2. **Set up environment variables:**
   ```bash
   ./scripts/setup.sh
   ```
   This will create a `.env` file from `.env.example` with generated secrets.

3. **Customize environment variables:**
   Edit the `.env` file to match your environment (timezone, domain, data paths, etc.).

4. **Start the services:**
   ```bash
   docker-compose up -d
   ```

## Usage

- The starter service runs on port 8000 (mapped from container port 9000).
- Add new services by creating new `.yml` files in the `compose/` directory and including them in `docker-compose.yml`.
- Customize service Dockerfiles in the `shared/` directory.

## Contributing

Add new services by following the modular structure: create service configs in `compose/`, Dockerfiles in `shared/`, and update the main `docker-compose.yml` to include them.
