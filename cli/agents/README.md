# 🤖 Surgenix Patient Care Agents

This directory contains **GenAI agents** specifically designed for post-surgery patient care and recovery support in the Surgenix healthcare system.

## 🏥 What are Surgenix Agents?

Surgenix agents are intelligent AI assistants that provide specialized healthcare support throughout a patient's recovery journey. Each agent has a specific role and expertise area, working together to deliver comprehensive patient care.

## 👥 Available Patient Care Agents

### 👋 **Welcome Agent (Mila)**

**Directory**: [`welcome_agent/`](welcome_agent/)

**Main File**: `welcome_agent.py`

**Role**: First point of contact and system introduction

**Key Features**:

- Warm patient greetings and introductions
- System orientation and capability explanations
- Onboarding guidance for new patients
- Bridges patients to specialized care agents

**Best For**: Initial patient contact, system introduction, general questions

---

### 📋 **Discharge Summary Agent**

**Directory**: [`discharge_summary/`](discharge_summary/)

**Main File**: `discharge_summary.py`

**Role**: Medical document processing and analysis

**Key Features**:

- Processes discharge summaries and medical documents
- Extracts key medical information
- Provides personalized recovery guidance
- Identifies important care instructions

**Best For**: Document analysis, medical information extraction, personalized care plans

---

### 🏃‍♀️ **Activity Agent**

**Directory**: [`activity_agent/`](activity_agent/)

**Main File**: `activity_agent.py`

**Role**: Recovery exercises and wellness activities

**Key Features**:

- Recommends appropriate recovery exercises
- Suggests wellness activities (music, yoga, walking)
- Provides safety guidelines for activities
- Tracks patient progress and preferences

**Best For**: Exercise recommendations, wellness activities, recovery motivation

## 🚀 Quick Start

### Prerequisites

1. **Environment Setup**:

   ```bash
   # Set required environment variables
   export AGENT_JWT=your_agent_jwt_token
   export OPENAI_API_KEY=your_openai_api_key
   ```

2. **Agent Registration** (if not already done):
   ```bash
   cd ../ # Go back to cli directory
   python cli.py register_agent --name <agent_name> --description <description>
   ```

### Running an Agent

1. **Navigate to the agent directory**:

   ```bash
   cd welcome_agent/
   # or
   cd discharge_summary/
   # or
   cd activity_agent/
   ```

2. **Install dependencies**:

   ```bash
   uv sync
   ```

3. **Run the agent**:
   ```bash
   uv run python welcome_agent.py
   # or
   uv run python discharge_summary.py
   # or
   uv run python activity_agent.py
   ```

### Testing Agents

Each agent can be tested using the GenAI Session Protocol:

```bash
# Example interaction with Welcome Agent
python welcome_agent.py
# Then send messages like: "Hi", "What can you do?", "Who are you?"
```

## 🔄 Patient Care Workflow

### 🎯 **Recommended Patient Journey**

1. **Welcome Agent** → Initial greeting, system introduction
2. **Discharge Summary Agent** → Process medical documents
3. **Activity Agent** → Recovery exercises and activities
4. **Ongoing Care** → Continue with specialized agents as needed

### 🤝 **Agent Collaboration**

- **Welcome Agent** guides patients to upload discharge summaries
- **Discharge Summary Agent** provides medical context for other agents
- **Activity Agent** uses medical information for safe exercise recommendations
- All agents maintain **user memory** for personalized experiences

## 📖 Documentation

Each agent has its own comprehensive README including:

- **Purpose and capabilities**
- **Setup and configuration instructions**
- **Usage examples and interactions**
- **Technical implementation details**
- **Integration guidelines**

## 🔧 Technical Details

### 🛠️ **Framework & Technology**

- **Protocol**: GenAI Session Protocol
- **AI Model**: GPT-4o (OpenAI)
- **Memory**: Integrated user profile storage
- **Dependencies**: Managed with `uv` (see individual `pyproject.toml`)

### 🏗️ **Architecture**

- **Stateful**: Maintains conversation context
- **Memory-enabled**: Remembers user preferences and history
- **Modular**: Each agent focuses on specific healthcare domains
- **Interoperable**: Designed to work together seamlessly

### 🔐 **Security & Privacy**

- **JWT Authentication**: Secure agent registration
- **Environment Variables**: API keys stored securely
- **HIPAA Considerations**: Designed with healthcare privacy in mind

## 🎯 Use Cases

### 🏥 **Healthcare Settings**

- **Post-surgery care** and recovery monitoring
- **Hospital discharge** process automation
- **Telehealth platforms** and remote care
- **Patient portals** and self-service systems

### 👤 **Patient Types**

- **Post-operative patients** (appendectomy, hysterectomy, transplants)
- **Elderly patients** needing guidance and support
- **Non-English speakers** (with translation integration)
- **Patients with accessibility needs** (with audio support)

## 🌟 Benefits

### 💚 **For Patients**

- **24/7 availability** for questions and support
- **Personalized care** based on medical history
- **Step-by-step guidance** through recovery
- **Friendly, supportive** interaction style

### 🏥 **For Healthcare Providers**

- **Reduced manual workload** for routine questions
- **Consistent information delivery**
- **Patient engagement** and compliance tracking
- **Scalable care support**

## 🛠️ Development & Customization

### 🔧 **Adding New Agents**

1. Create new directory under `agents/`
2. Follow the pattern of existing agents
3. Include comprehensive README
4. Use `uv` for dependency management
5. Implement GenAI Session Protocol

### 📝 **Best Practices**

- **Healthcare-focused** language and responses
- **Patient safety** as top priority
- **Clear, simple** communication
- **Empathetic** and supportive tone
- **Integration** with other Surgenix components

Perfect for creating comprehensive, caring patient experiences! 🏥💚
