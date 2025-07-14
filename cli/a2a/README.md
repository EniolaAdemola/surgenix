# 🔌 A2A (Agent to Agent) Cards

This directory contains **A2A (Agent to Agent Protocol)** implementations for the Surgenix patient care system.

## 📋 What are A2A Cards?

A2A Cards are lightweight agents that follow the Agent to Agent Protocol, allowing them to be discovered and integrated into the GenAI AgentOS ecosystem. They provide specific functionality that can be called by other agents or the master agent.

## 🏥 Available A2A Cards

### 🔬 **Lab Location Agent**

**Directory**: [`lab_location_agent/`](lab_location_agent/)

**Purpose**: Provides simple facility location services for medical labs and hospitals.

**Recommended File**: **`simple_lab_agent.py`**

⚠️ **Important**: Use `simple_lab_agent.py` as it's the current, working implementation optimized for Agent OS integration.

## 🚀 Quick Start

1. **Navigate to the agent directory**:

   ```bash
   cd lab_location_agent/
   ```

2. **Install dependencies**:

   ```bash
   uv sync
   ```

3. **Run the A2A agent**:

   ```bash
   uv run python simple_lab_agent.py
   ```

4. **Add to AgentOS**:
   - Go to the GenAI Agent UI: [http://localhost:3000/](http://localhost:3000/)
   - Add A2A card with URL: `http://host.docker.internal:10002`
   - The system will automatically discover the agent capabilities

## 📖 Documentation

Each A2A card has its own detailed README with:

- Setup instructions
- Usage examples
- API documentation
- Integration details

See the individual directories for comprehensive documentation.

## 🔧 Development Notes

- A2A cards are **stateless** and **lightweight**
- They follow the **Agent to Agent Protocol** specification
- Compatible with **GenAI AgentOS** auto-discovery
- Designed for **healthcare and patient care** scenarios

For more information about A2A protocol and implementation details, check the individual agent READMEs.
