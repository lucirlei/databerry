<h1 align="center" style="font-weight: bold">
  <br>
  <a href="https://chaindesk.ai"><img src="apps/dashboard/public/logo.png" alt="Chaindesk" width="42"></a>
  <br>
  Chaindesk
  <br>
    <h3 align="center">The no-code platform for building custom LLM Agents</h3>
  <br>
  
</h1>

<!-- <h4 align="center">The no-code platform for semantic search and retrieval of personal or organizational documents.</h4> -->

<h2 align="center">
<img src="apps/dashboard/public/og-image.jpg" alt="Chaindesk" width="1000" style="max-width: 100%;">
</h2>

**[Chaindesk](https://chaindesk.ai)** provides a user-friendly solution to quickly setup a semantic search system over your personal data without any technical knowledge.

### [📄 Documentation](https://docs.chaindesk.ai/)

### Features

- Load data from anywhere
  - Raw text
  - Web page
  - Files
    - Word
    - Excel
    - Powerpoint
    - PDF
    - Markdown
    - Plain Text
  - Web Site (coming soon)
  - Notion (coming soon)
  - Airtable (coming soon)
- No-code: User-friendly interface to manage your datastores and chat with your data
- Securized API endpoint for querying your data
- Auto sync data sources (coming soon)
- **Auto generates a ChatGPT Plugin** for each datastore

### Semantic Search Specs

- Vector Database: Qdrant
- Embeddings: Openai's text-embedding-ada-002
- Chunk size: 1024 tokens

### Stack

- Next.js
- Joy UI
- LangchainJS
- PostgreSQL
- Prisma
- Qdrant

Inspired by the [ChatGPT Retrieval Plugin](https://github.com/openai/chatgpt-retrieval-plugin).

### Run the project locally

#### Without docker compose

Minimum requirements to run the projects locally

- Node.js v18
- Postgres Database
- Redis
- Qdrant
- GitHub App (NextAuth)
- Email Provider (NextAuth)
- OpenAI API Key
- AWS S3 Credentials

<!-- ```bash
# Create .env.local
cp .env.example .env.local

# Install dependencies
pnpm install

# Generate DB tables
pnpm prisma:migrate:dev

# Run server
pnpm dev

# Run worker process
pnpm worker:datasource-loader

# or pnpm dev:all
``` -->

<!-- #### With docker compose -->

<!-- First `cd .dev/databerry` then populate the config files `app.env` and `docker.env` as needed, then run the compose command: -->

### Run locally (Docker required)

```shell
cp .env.example .env.local
# Add your own OPENAI_API_KEY

pnpm dev

# pupeteer browser local
brew install chromium --no-quarantine

# Dev emails inbox (maildev)
# visit http://localhost:1080
```
### Deployment via Portainer

#### Prerequisites
- An existing PostgreSQL database, Redis instance, and Traefik reverse proxy.
- A Docker network named `traefik_proxy`:

  ```sh
  docker network create traefik_proxy
  ```

#### Environment variables and secrets
1. Copy `.env.example` to `.env.portainer` and adjust values for your environment.
2. Set `DATABASE_URL` and `REDIS_URL` to point to the existing services.
3. Generate strong secrets for `NEXTAUTH_SECRET` and `JWT_SECRET`:

  ```sh
  openssl rand -hex 32
  ```
4. Map any persistent volumes defined in `docker-compose.portainer.yml` (for example `databerry_data:/app/data`).

#### Deploy
1. In Portainer, go to **Stacks → Add stack**.
2. Upload `docker-compose.portainer.yml` as the stack file.
3. Upload `.env.portainer` in the **Environment variables** section.
4. Deploy the stack.

#### Image options
- Build the image directly in Portainer using the Dockerfile.
- Or reference a pre-built image from a container registry in `docker-compose.portainer.yml`.

#### Verification
- Watch container logs and health checks in Portainer.
- Confirm the service is attached to the `traefik_proxy` network and visible in the Traefik dashboard.
- Access the application through the Traefik-managed URL to ensure it is reachable.
