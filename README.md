# 🏥 Surgenix - GenAI Agents Infrastructure

**Surgenix** is a comprehensive patient care system built on GenAI agents infrastructure. This repository provides the complete infrastructure for running GenAI agents, including:

- Backend
- Router
- Master Agents
- PostgreSQL Database
- Frontend
- CLI
- Redis
- Celery

## 📎 Repository Link

👉 [Original Repository](https://github.com/genai-works-org/genai-agentos) (Forked from)
👉 [Surgenix Fork](https://github.com/genai-works-org/genai-agentos)

This project is a **fork** of the original GenAI AgentOS repository, enhanced with **Surgenix patient care agents** and specialized healthcare functionality.

## 🏥 Surgenix Agents & Components

All built agents, MCP servers, and A2A cards are located in the **`cli/`** directory with detailed READMEs:

### 🤖 **Patient Care Agents**

- **Welcome Agent (Mila)** - [`cli/agents/welcome_agent/`](cli/agents/welcome_agent/) - Friendly first-contact agent for patient onboarding
- **Discharge Summary Agent** - [`cli/agents/discharge_summary/`](cli/agents/discharge_summary/) - Processes and analyzes medical discharge documents
- **Activity Agent** - [`cli/agents/activity_agent/`](cli/agents/activity_agent/) - Provides recovery exercises and wellness activities

### 🔌 **A2A Cards**

- **Lab Location Agent** - [`cli/a2a/lab_location_agent/`](cli/a2a/lab_location_agent/) - Simple A2A agent for finding medical facilities

### 🛠️ **MCP Servers**

- **Text to Audio** - [`cli/mcp/text_to_audio/`](cli/mcp/text_to_audio/) - Convert text to speech functionality
- **Language Translator** - [`cli/mcp/language_translator/`](cli/mcp/language_translator/) - Multi-language translation support

Each component includes comprehensive documentation, setup instructions, and usage examples. See the individual README files for detailed information.

### 🔧 **Enhanced Master Agent**

- **Updated Master Agent Prompt** - [`updated_master_agent_prompt.md`](updated_master_agent_prompt.md) - Optimized prompt for healthcare scenarios and Surgenix agent integration (see configuration instructions below)

## 🛠️ Readme Files

- [CLI](cli/README.md)
- [Backend](backend/README.md)
- [Master Agents](master-agent/README.md)
- [Router](router/README.md)
- [Frontend](frontend/README.md)

## 📄️ License

- [MIT](LICENSE)

## 🧠 Supported Agent Types

The Surgenix system supports multiple kinds of Agents for comprehensive patient care:

| Agent Type       | Description                                                                                   | Surgenix Examples                                      |
| ---------------- | --------------------------------------------------------------------------------------------- | ------------------------------------------------------ |
| **GenAI Agents** | Connected via [`genai-protocol`](https://pypi.org/project/genai-protocol/) library interface. | Welcome Agent, Discharge Summary Agent, Activity Agent |
| **MCP Servers**  | MCP (Model Context Protocol) servers can be added by pasting their URL in the UI.             | Text-to-Audio, Language Translator                     |
| **A2A Servers**  | A2A (Agent to Agent Protocol) servers can be added by pasting their URL in the UI.            | Lab Location Agent                                     |

### 🏥 **Healthcare-Focused Architecture**

Surgenix agents are specifically designed for **post-surgery patient care and recovery**, providing:

- **Patient onboarding** and system introductions
- **Medical document processing** and analysis
- **Recovery activity** recommendations and guidance
- **Facility location** services for follow-up care

---

## 📦 Prerequisites

Make sure you have the following installed:

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)
- [`make`](https://www.gnu.org/software/make/) (optional)

  - macOS: `brew install make`
  - Linux: `sudo apt-get install make`

## 🚀 Local Setup

1. Clone the repository:

   ```bash
   git clone https://github.com/genai-works-org/genai-agentos.git
   cd genai-agentos/
   ```

2. Create a `.env` file by copying the example (can be empty and customized later):

   ```bash
   cp .env-example .env
   ```

   - A `.env` file **should be present** for configuration.
   - All variables in `.env-example` are commented.
     You can customize any environment setting by **uncommenting** the relevant line and providing a new value.

3. Start Docker desktop and ensure it is running.

4. Start the infrastructure:

   ```bash
   make up
   # or alternatively
   docker compose up
   ```

5. After startup:

   - Frontend UI: [http://localhost:3000/](http://localhost:3000/)
   - Swagger API Docs: [http://localhost:8000/docs#/](http://localhost:8000/docs#/)

## 🔧 Surgenix Master Agent Configuration

### 📝 **Custom Master Agent Prompt**

For optimal Surgenix patient care functionality, use the **enhanced master agent prompt** provided in this repository:

1. **Navigate to the GenAI Agent UI**: [http://localhost:3000/](http://localhost:3000/)

2. **Configure OpenAI Model**:

   - Go to the model configuration section
   - Add your OpenAI API key
   - Select GPT-4o as the model

3. **Replace Master Agent Prompt**:

   - Copy the contents from [`updated_master_agent_prompt.md`](updated_master_agent_prompt.md)
   - Paste this prompt in the **Master Agent Prompt** field in the UI
   - This enhanced prompt is specifically optimized for Surgenix healthcare agents

4. **Save Configuration** to apply the new settings

The updated prompt includes specialized instructions for healthcare scenarios, patient care workflows, and improved integration with Surgenix agents.

## 👾 Supported Providers and Models

- OpenAI: gpt-4o

## 🌐 Ngrok Setup (Optional)

Ngrok can be used to expose the local WebSocket endpoint.

1. Install Ngrok:

   - macOS (Homebrew): `brew install ngrok/ngrok/ngrok`
   - Linux: `sudo snap install ngrok`

2. Authenticate Ngrok:

   - Sign up or log in at [ngrok dashboard](https://dashboard.ngrok.com).
   - Go to the **"Your Authtoken"** section and copy the token.
   - Run the command:

     ```bash
     ngrok config add-authtoken <YOUR_AUTH_TOKEN>
     ```

3. Start a tunnel to local port 8080:

   ```bash
   ngrok http 8080
   ```

4. Copy the generated WebSocket URL and update the `ws_url` field in:

   ```
   genai_session.session.GenAISession
   ```

---

## 🤖 Surgenix Agent Registration Quick Start

For detailed instructions on all agents, see the [CLI README](cli/README.md) and individual agent directories.

```bash
cd cli/

python cli.py signup -u <username> # Register a new user, also available in [UI](http://localhost:3000/)

python cli.py login -u <username> -p <password> # Login to the system, get JWT user token

python cli.py register_agent --name <agent_name> --description <agent_description>

cd agents/

# Run the agent (using uv - recommended)
uv sync  # Install dependencies
uv run python <agent_name>.py

# Or alternatively with python directly
python <agent_name>.py
```

### 🏥 **Pre-built Surgenix Agents Ready to Run:**

- `welcome_agent.py` - Patient greeting and onboarding
- `discharge_summary.py` - Medical document processing
- `activity_agent.py` - Recovery exercise recommendations

## 💎 Environment Variables

| Variable                    | Description                                                          | Example / Default                                                                       |
| --------------------------- | -------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| `FRONTEND_PORT`             | Port to start a frontend                                             | `3000` - default. Can be changed by run in terminal ` source FRONTEND_PORT=<your_port>` |
| `ROUTER_WS_URL`             | WebSocket URL for the `router` container                             | `ws://genai-router:8080/ws` - host is either `localhost` or `router` container name     |
| `SECRET_KEY`                | Secret key for cryptographic operations - JWT/ LLM config encryption | `$(openssl rand -hex 32)`                                                               |
| `POSTGRES_HOST`             | PostgreSQL Host                                                      | `genai-postgres`                                                                        |
| `POSTGRES_USER`             | PostgreSQL Username                                                  | `postgres`                                                                              |
| `POSTGRES_PASSWORD`         | PostgreSQL Password                                                  | `postgres`                                                                              |
| `POSTGRES_DB`               | PostgreSQL Database Name                                             | `postgres`                                                                              |
| `POSTGRES_PORT`             | PostgreSQL Port                                                      | `5432`                                                                                  |
| `DEBUG`                     | Enable/disable debug mode - Server/ ORM logging                      | `True` / `False`                                                                        |
| `MASTER_AGENT_API_KEY`      | API key for the Master Agent - internal identifier                   | `e1adc3d8-fca1-40b2-b90a-7b48290f2d6a::master_server_ml`                                |
| `MASTER_BE_API_KEY`         | API key for the Master Backend - internal identifier                 | `7a3fd399-3e48-46a0-ab7c-0eaf38020283::master_server_be`                                |
| `BACKEND_CORS_ORIGINS`      | Allowed CORS origins for the `backend`                               | `["*"]`, `["http://localhost"]`                                                         |
| `DEFAULT_FILES_FOLDER_NAME` | Default folder for file storage - Docker file volume path            | `/files`                                                                                |
| `CLI_BACKEND_ORIGIN_URL`    | `backend` URL for CLI access                                         | `http://localhost:8000`                                                                 |

## 🛠️ Troubleshooting

### ❓ MCP server or A2A card URL could not be accessed by the genai-backend

✅ If your MCP server or A2A card is hosted on your local machine, make sure to change the host name from `http://localhost:<your_port>` to `http://host.docker.internal:<your_port>` and try again.

🔎 **Also make sure to pass the full url of your MCP server or A2A card, such as - `http://host.docker.internal:8000/mcp` for MCP or `http://host.docker.internal:10002` for A2A**

⚠️ No need to specify `/.well-known/agent.json` for your A2A card as `genai-backend` will do it for you!

### ❓ My MCP server with valid host cannot be accessed by the genai-backend

✅ Make sure your MCP server supports `streamable-http` protocol and is remotely accessible.Also make sure that you're specifiying full URL of your server, like - `http://host.docker.internal:8000/mcp`

⚠️ Side note: `sse` protocol is officially deprecated by MCP protocol devs, `stdio` protocol is not supported yet, but stay tuned for future announcements!
