# Chronicle: Agentic Experience Profile (Draft v0.1)

This document defines a draft profile for structuring the actions of autonomous AI agents based on the xAPI specification. The goal is to provide a unified method for recording "what the agent thought, how it acted, and what results it achieved."

## 1. Verb Definitions

We define the primary actions in an agent's workflow using the following Verbs:

| Verb | Meaning | Recording Trigger |
| :--- | :--- | :--- |
| **Delegated** | Task Assignment | When a task is assigned to the agent by a user or another system (e.g., via MCP). |
| **Reasoned** | Reasoning & Inference | When the agent performs internal planning, Chain-of-Thought, or self-criticism. |
| **Invoked** | Tool Execution | When the agent uses a specific "tool," such as an MCP tool, external API, or local command. |
| **Observed** | Environment Observation | When the agent reads tool execution results, logs, or external states. |
| **Refactored** | Correction & Improvement | When the agent modifies its code or approach based on errors or feedback. |
| **Resolved** | Completion | When the assigned mission is successfully completed. |
| **Abandoned** | Termination | When the task is aborted due to errors, retry limits, or unrecoverable issues. |

## 2. Data Structure Example (JSON)

Below is an example of an xAPI statement recorded when an agent attempts to fix code (Refactored) but encounters a syntax error.

```json
{
  "actor": {
    "name": "Antigravity-Agent-01",
    "account": { 
      "homePage": "[https://github.com/antigravity](https://github.com/antigravity)", 
      "name": "agent-uuid-123" 
    }
  },
  "verb": {
    "id": "[https://w3id.org/xapi/chronicle/verbs/refactored](https://w3id.org/xapi/chronicle/verbs/refactored)",
    "display": { "en-US": "refactored", "ja-JP": "修正試行" }
  },
  "object": {
    "id": "[https://w3id.org/xapi/chronicle/activities/code-optimization](https://w3id.org/xapi/chronicle/activities/code-optimization)",
    "definition": {
      "name": { "en-US": "Code Optimization", "ja-JP": "コードの最適化" }
    }
  },
  "result": {
    "success": false,
    "extensions": {
      "[https://w3id.org/xapi/chronicle/ext/error_log](https://w3id.org/xapi/chronicle/ext/error_log)": "SyntaxError: invalid syntax at line 45",
      "[https://w3id.org/xapi/chronicle/ext/attempt_count](https://w3id.org/xapi/chronicle/ext/attempt_count)": 3
    }
  },
  "context": {
    "platform": "MCP-Server-v1.2",
    "extensions": {
      "[https://w3id.org/xapi/chronicle/ext/model](https://w3id.org/xapi/chronicle/ext/model)": "claude-3-5-sonnet"
    }
  }
}
