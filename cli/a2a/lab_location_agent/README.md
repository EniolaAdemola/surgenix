# Healthcare Location A2A Agent

This specialized A2A agent helps users find the nearest hospitals, labs, clinics, and emergency care facilities based on their address or location. It provides comprehensive healthcare facility discovery, emergency services location, and appointment scheduling assistance.

## Features

- **Healthcare Facility Location**: Find nearest hospitals, labs, clinics, and urgent care centers
- **Emergency Services**: Locate emergency care facilities with priority-based recommendations
- **Lab Appointment Assistance**: Find labs offering specific tests with appointment availability
- **Distance Calculation**: Accurate distance calculation using Haversine formula
- **Maps Integration**: Generate Google Maps links for directions and location viewing
- **A2A Communication**: Coordinate with other agents for complex healthcare workflows
- **Mock & Real Data**: Supports both mock data for testing and real API integration

## Healthcare Location Functions

### 1. `healthcare_locator`

Find the nearest healthcare facilities based on user's address.

**Parameters:**

- `address` (string): User's address or location description
- `facility_type` (string): Type of facility to search for
  - `"hospital"`: General hospitals
  - `"lab"`: Diagnostic laboratories
  - `"clinic"`: Medical clinics
  - `"urgent_care"`: Urgent care centers
  - `"all"`: All facility types
- `limit` (optional, int): Maximum number of facilities to return (default: 5)
- `radius_km` (optional, float): Search radius in kilometers (default: 10.0)

**Example Usage:**

```json
{
  "address": "123 Main Street, Downtown",
  "facility_type": "lab",
  "limit": 3,
  "radius_km": 5.0
}
```

**Example Response:**

```json
{
  "success": true,
  "facilities": [
    {
      "name": "QuickLab Diagnostics",
      "address": "456 Oak Ave, Midtown",
      "type": "lab",
      "phone": "+1-555-0200",
      "rating": 4.5,
      "distance_km": 2.3,
      "distance_miles": 1.4,
      "maps_url": "https://maps.google.com/?q=40.7589,-73.9851",
      "directions_url": "https://maps.google.com/dir/40.7128,-74.0060/40.7589,-73.9851"
    }
  ],
  "total_found": 1
}
```

### 2. `emergency_locator`

Find emergency healthcare facilities with priority-based recommendations.

**Parameters:**

- `address` (string): User's current address or location
- `emergency_type` (string): Severity of emergency
  - `"critical"`: Life-threatening (hospitals only, larger radius)
  - `"urgent"`: Urgent care needed (hospitals + urgent care)
  - `"non_urgent"`: Non-urgent care (all facility types)

**Example Usage:**

```json
{
  "address": "789 Pine Street",
  "emergency_type": "urgent"
}
```

**Example Response:**

```json
{
  "success": true,
  "emergency_type": "urgent",
  "emergency_number": "911",
  "emergency_facilities": [
    {
      "priority": "HIGH",
      "name": "City General Hospital",
      "type": "hospital",
      "distance_km": 1.8,
      "estimated_travel_time": "4 minutes",
      "call_url": "tel:+15550100",
      "directions_url": "https://maps.google.com/dir/..."
    }
  ],
  "urgent_message": "If this is a life-threatening emergency, call 911 immediately!"
}
```

### 3. `lab_appointment_finder`

Find labs offering specific tests with appointment scheduling information.

**Parameters:**

- `address` (string): User's address
- `test_type` (string): Type of lab test needed
  - `"general"`: General lab work
  - `"blood_work"`: Blood tests
  - `"covid_test"`: COVID-19 testing
  - `"imaging"`: Medical imaging
- `insurance_type` (optional): Insurance provider
- `preferred_time` (optional): Preferred appointment time

**Example Usage:**

```json
{
  "address": "321 Elm Street",
  "test_type": "blood_work",
  "insurance_type": "Blue Cross",
  "preferred_time": "morning"
}
```

**Example Response:**

```json
{
  "success": true,
  "labs": [
    {
      "name": "Central Medical Lab",
      "test_available": true,
      "test_details": {
        "available": true,
        "fasting_required": true,
        "duration": "10 minutes"
      },
      "appointment_availability": {
        "today": ["2:00 PM", "4:30 PM"],
        "tomorrow": ["9:00 AM", "11:30 AM", "3:00 PM"]
      },
      "online_booking": "https://booking.centralmedicallab.com",
      "call_to_book": "tel:+15550400"
    }
  ],
  "booking_tips": [
    "Call ahead to confirm test availability",
    "Ask about fasting requirements",
    "Bring insurance card and ID"
  ]
}
```

## Setup

1. **Install dependencies:**

   ```bash
   cd /path/to/a2a_agent
   uv sync
   ```

2. **Configure environment:**
   The `.env` file should contain your agent JWT token and A2A settings.

3. **Run the A2A agent:**
   ```bash
   uv run python a2a_agent.py
   ```

## Available Functions

### 1. `coordinate_agents`

Main coordination function for A2A operations.

**Parameters:**

- `action` (string): Action to perform
  - `"discover"`: Find available agents
  - `"send_message"`: Send message to specific agent
  - `"broadcast"`: Send message to all known agents
  - `"status"`: Get A2A agent status
- `target_agent_id` (optional): Target agent ID for direct communication
- `message` (optional): Message content to send
- `data` (optional): Additional data payload

**Example Usage:**

```json
{
  "action": "discover"
}
```

```json
{
  "action": "send_message",
  "target_agent_id": "translator_agent_123",
  "message": "Hello from A2A coordinator",
  "data": { "priority": "high" }
}
```

### 2. `translate_via_agent`

Translate text using the language translator agent via A2A communication.

**Parameters:**

- `text` (string): Text to translate
- `target_language` (string): Target language for translation
- `translator_agent_id` (optional): ID of the translator agent

**Example:**

```json
{
  "text": "Hello, how are you?",
  "target_language": "Spanish",
  "translator_agent_id": "translator_agent_123"
}
```

### 3. `generate_audio_via_agent`

Generate audio from text using the text-to-audio agent via A2A communication.

**Parameters:**

- `text` (string): Text to convert to audio
- `voice_id` (optional): Voice ID for audio generation
- `audio_agent_id` (optional): ID of the audio generation agent

**Example:**

```json
{
  "text": "Welcome to the A2A system",
  "voice_id": "21m00Tcm4TlvDq8ikWAM",
  "audio_agent_id": "audio_agent_456"
}
```

### 4. `orchestrate_workflow`

Orchestrate complex workflows involving multiple agents.

**Parameters:**

- `workflow_type` (string): Type of workflow
  - `"translate_and_audio"`: Translate text then generate audio
  - `"multi_translate"`: Translate to multiple languages
  - `"custom"`: Custom workflow
- `input_data` (object): Input data for the workflow
- `agent_mapping` (optional): Mapping of agent types to specific agent IDs

**Example:**

```json
{
  "workflow_type": "translate_and_audio",
  "input_data": {
    "text": "Welcome to our system",
    "target_language": "French",
    "voice_id": "21m00Tcm4TlvDq8ikWAM"
  },
  "agent_mapping": {
    "translator": "translator_agent_123",
    "audio": "audio_agent_456"
  }
}
```

## Workflow Examples

### 1. Basic Agent Discovery

```json
{
  "function": "coordinate_agents",
  "parameters": {
    "action": "discover"
  }
}
```

**Response:**

```json
{
  "discovered_agents": {
    "translator_agent_123": {
      "info": {...},
      "last_contact": "2025-07-13T12:00:00",
      "status": "active"
    }
  },
  "total_agents": 1,
  "discovery_time": "2025-07-13T12:00:00"
}
```

### 2. Translate and Generate Audio Workflow

```json
{
  "function": "orchestrate_workflow",
  "parameters": {
    "workflow_type": "translate_and_audio",
    "input_data": {
      "text": "Hello, welcome to our service!",
      "target_language": "Spanish",
      "voice_id": "21m00Tcm4TlvDq8ikWAM"
    }
  }
}
```

**Response:**

```json
{
  "success": true,
  "workflow_type": "translate_and_audio",
  "steps": {
    "translation": {
      "success": true,
      "original_text": "Hello, welcome to our service!",
      "translation_result": "¡Hola, bienvenido a nuestro servicio!"
    },
    "audio_generation": {
      "success": true,
      "audio_result": "http://localhost:8891/audio/audio_20250713_120000_abc123.mp3"
    }
  },
  "final_output": {
    "original_text": "Hello, welcome to our service!",
    "translated_text": "¡Hola, bienvenido a nuestro servicio!",
    "audio_file": "http://localhost:8891/audio/audio_20250713_120000_abc123.mp3"
  }
}
```

## Communication Protocol

The A2A agent uses the GenAI session protocol for communication:

1. **Discovery**: Agents register themselves when they start
2. **Heartbeat**: Regular status updates to maintain agent registry
3. **Messaging**: JSON-based message format for all communications
4. **Error Handling**: Retry mechanisms and fallback strategies

## Message Format

Standard A2A message format:

```json
{
  "content": "message content",
  "data": {
    "additional": "data"
  },
  "from_agent": "sender_agent_id",
  "timestamp": "2025-07-13T12:00:00",
  "message_id": "unique_message_id",
  "priority": "normal|high|urgent"
}
```

## Error Handling

The A2A system includes comprehensive error handling:

- **Connection Errors**: Automatic retry with exponential backoff
- **Agent Unavailable**: Graceful degradation and error reporting
- **Timeout Handling**: Configurable timeouts for different operations
- **Message Validation**: Input validation and sanitization

## Configuration

### Environment Variables

- `AGENT_JWT`: JWT token for agent authentication
- `A2A_DISCOVERY_ENABLED`: Enable/disable agent discovery
- `A2A_BROADCAST_ENABLED`: Enable/disable broadcast functionality
- `A2A_MAX_RETRIES`: Maximum retry attempts for failed operations
- `A2A_TIMEOUT_SECONDS`: Timeout for agent communications

### Agent Registry

The A2A agent maintains an in-memory registry of active agents:

- **Auto-discovery**: Agents are discovered when they register
- **Health monitoring**: Regular health checks and status updates
- **Cleanup**: Inactive agents are removed from the registry

## Security Considerations

- **Authentication**: All agent communications use JWT tokens
- **Message Validation**: Input validation on all message content
- **Rate Limiting**: Built-in protection against message flooding
- **Access Control**: Agent-level permissions for sensitive operations

## Performance

- **Async Operations**: All communications are asynchronous
- **Connection Pooling**: Efficient connection management
- **Message Queuing**: Built-in message queuing for high throughput
- **Caching**: Agent registry caching for faster lookups

## Troubleshooting

### Common Issues

1. **Agent Not Found**: Check if target agent is registered and active
2. **Communication Timeout**: Verify network connectivity and agent health
3. **Authentication Errors**: Validate JWT tokens and permissions
4. **Message Format Errors**: Ensure proper JSON formatting

### Debug Mode

Enable debug logging by setting the log level to DEBUG in the configuration.

## Integration Examples

### With Frontend

The A2A agent can be integrated with the frontend through the GenAI system:

1. Frontend sends request to GenAI system
2. GenAI system routes request to A2A agent
3. A2A agent coordinates with other agents
4. Results are returned to frontend

### With Other Agents

Example integration with translator and audio agents:

```python
# Discover available agents
discovery_result = await coordinate_agents(action="discover")

# Send translation request
translation_result = await translate_via_agent(
    text="Hello world",
    target_language="Spanish"
)

# Generate audio from translation
audio_result = await generate_audio_via_agent(
    text=translation_result["translated_text"]
)
```

## Future Enhancements

- **Load Balancing**: Distribute requests across multiple agent instances
- **Persistent Registry**: Database-backed agent registry
- **Advanced Workflows**: More complex workflow orchestration patterns
- **Monitoring Dashboard**: Real-time monitoring of agent communications
- **Message Encryption**: End-to-end encryption for sensitive communications
