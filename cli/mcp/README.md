# 🛠️ MCP (Model Context Protocol) Servers

This directory contains **MCP (Model Context Protocol)** server implementations for the Surgenix patient care system.

## 📋 What are MCP Servers?

MCP Servers provide tools and resources that can be used by AI agents through the Model Context Protocol. They extend the capabilities of agents by providing access to external services, APIs, and specialized functionality.

## 🏥 Available MCP Servers

### 🔊 **Text to Audio**

**Directory**: [`text_to_audio/`](text_to_audio/)

**Purpose**: Converts text to speech for patient accessibility and communication needs.

**Main File**: `main.py`

**Features**:

- Text-to-speech conversion
- Audio file generation
- Accessibility support for patients
- Multiple voice options

### 🌐 **Language Translator**

**Directory**: [`language_translator/`](language_translator/)

**Purpose**: Provides multi-language translation services for diverse patient populations.

**Main File**: `language_translator.py`

**Features**:

- Multi-language translation
- Healthcare terminology support
- Patient communication assistance
- Real-time translation capabilities

## 🚀 Quick Start

### Running an MCP Server

1. **Navigate to the desired MCP server directory**:

   ```bash
   cd text_to_audio/
   # or
   cd language_translator/
   ```

2. **Install dependencies**:

   ```bash
   pip install -r requirements.txt
   ```

3. **Run the MCP server**:

   ```bash
   # For text-to-audio
   python main.py

   # For language translator
   python language_translator.py
   ```

### Adding to AgentOS

1. **Go to the GenAI Agent UI**: [http://localhost:3000/](http://localhost:3000/)

2. **Add MCP Server**:

   - Navigate to MCP server configuration
   - Add server URL (e.g., `http://host.docker.internal:8000/mcp`)
   - The system will discover available tools automatically

3. **Configure Access**:
   - Ensure the MCP server supports `streamable-http` protocol
   - Use full URLs for proper discovery

## 📖 Documentation

Each MCP server has its own detailed README with:

- Setup instructions
- API documentation
- Usage examples
- Configuration options
- Integration details

See the individual directories for comprehensive documentation.

## 🔧 Development Notes

### 🎯 **Protocol Requirements**

- MCP servers must support **streamable-http** protocol
- **SSE protocol** is deprecated
- **stdio protocol** support coming soon

### 🏥 **Healthcare Focus**

- Servers are designed for **patient care scenarios**
- Support **accessibility needs** (text-to-speech)
- Enable **multilingual communication**
- Integrate with **Surgenix agent ecosystem**

### 🔗 **Integration Points**

- **Welcome Agent** - Can use text-to-audio for greetings
- **Discharge Summary Agent** - Can use translation for multilingual documents
- **Activity Agent** - Can use audio for exercise instructions

## 🛠️ Troubleshooting

### ❓ MCP Server Not Accessible

✅ **Local Development**: Change URL from `http://localhost:<port>` to `http://host.docker.internal:<port>`

✅ **Full URL Required**: Use complete MCP endpoint URL (e.g., `http://host.docker.internal:8000/mcp`)

✅ **Protocol Support**: Ensure server supports `streamable-http` protocol

For more detailed troubleshooting, see the main [project README](../../README.md) troubleshooting section.

## 🌟 Benefits for Patient Care

- **🔊 Audio Support**: Text-to-speech for patients with reading difficulties
- **🌐 Language Access**: Translation for non-English speaking patients
- **♿ Accessibility**: Enhanced communication options
- **🤖 Agent Integration**: Seamless integration with Surgenix care agents

Perfect for creating inclusive, accessible healthcare experiences! 🏥💚
