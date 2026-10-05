# Autonomous IT Support Agent

An AI-powered **Level 1 IT Incident Responder** built with Python and OpenAI tool calling.

The agent acts as a first responder for server incidents. It investigates server health and recent logs, takes automated corrective action when resource usage is critical, and escalates complex issues to a human engineer when required.

## 🎯 Objective

The agent is designed to perform three core tasks:

1. **Investigate** — Check server CPU, memory, and recent logs when an incident is reported.
2. **Act** — Restart the service when CPU or memory usage is above 90%.
3. **Escalate** — Escalate the incident to a human engineer when logs indicate a critical dependency failure or an issue that cannot be resolved automatically.

## 🧠 Agent Workflow

```text
User Reports an Incident
          ↓
     AI Agent
          ↓
   Check Server Health
          ↓
   Fetch Recent Logs
          ↓
   Analyze Findings
       ↙       ↘
Critical       Complex / Dependency
Resource       Failure
  ↓                ↓
Restart          Escalate
Service          to Engineer
       ↘        ↙
        Final Response
```

## 🛠️ Tools Used by the Agent

The agent has access to four tools:

### 1. `get_server_health`

Checks the CPU and memory utilization of a specific server.

```text
CPU Usage
Memory Usage
Server Status
```

### 2. `fetch_recent_logs`

Retrieves recent log entries from a server to help diagnose the incident.

### 3. `restart_service`

Simulates restarting a service when CPU or memory utilization is critical.

Example result:

```json
{
    "server_id": "payment-server-01",
    "status": "success",
    "message": "Service restart command issued successfully."
}
```

### 4. `escalate_to_engineer`

Escalates complex incidents to an on-call engineer.

Example result:

```json
{
    "status": "escalated",
    "ticket_id": "INC-999",
    "assigned_to": "On-Call Engineer"
}
```

## 🔄 Function Calling Architecture

The application uses OpenAI tool/function calling to allow the model to select and execute the appropriate Python functions.

```text
User Issue
    ↓
OpenAI Model
    ↓
Tool Selection
    ↓
Python Function Execution
    ↓
Tool Result
    ↓
OpenAI Model
    ↓
Final Incident Response
```

The agent maintains a tool execution loop and continues investigating until it has enough information to provide a final response.

## 🧪 Test Scenarios

The notebook contains five test scenarios.

### Scenario A — Critical CPU

**Server:** `payment-server-01`

The server reports:

- CPU: **98%**
- Memory: **40%**
- Critical logs indicating a hung process and thread timeout
