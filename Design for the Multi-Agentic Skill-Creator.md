# Design for the Multi-Agentic Skill-Creator

This document outlines the architecture and design for a new skill, `multi-agent-skill-creator`. This skill will extend the existing `skill-creator` to guide the development of sophisticated, collaborative, enterprise-grade agentic skills, drawing inspiration from the principles of OpenClaw and leveraging modern agent communication protocols.

## 1. Core Principles

The `multi-agent-skill-creator` will be built upon the following core principles derived from the initial research phase:

*   **Action-Oriented Agents**: Skills created should enable agents to perform end-to-end tasks and workflows, moving beyond simple informational responses, as highlighted in the "Actionable Agent" trend report [1].
*   **Pervasive Integration**: The design will encourage building skills that integrate deeply into a user's digital ecosystem (email, calendar, communication platforms), mirroring the OpenClaw philosophy of being an agent that is "Everywhere" [2].
*   **Collaborative by Design**: Skills must be designed for interoperability, with built-in capabilities for discovery, communication, and task negotiation with other agents.
*   **Standardized Communication**: The architecture will be based on the Model Context Protocol (MCP) for tool/data access and the Agent-to-Agent (A2A) protocol for inter-agent collaboration, ensuring a robust and scalable framework [3, 4].
*   **Enterprise-Grade Governance**: A central tenet is to address the challenge of creating a "safe enterprise version of OpenClaw" by embedding security, logging, and governance patterns directly into the skill creation process.
*   **Shared Context**: The design will include a standardized mechanism for agents to maintain and share evolving context, enabling more intelligent and coordinated behavior.

## 2. Skill Architecture: `multi-agent-skill-creator`

The new skill will follow the standard skill anatomy but will be significantly more comprehensive than the original `skill-creator`.

```
/home/ubuntu/skills/multi-agent-skill-creator/
├── SKILL.md
├── scripts/
│   ├── init_multi_agent_skill.py
│   └── validate_multi_agent_skill.py
├── references/
│   ├── 1_foundations.md
│   ├── 2_mcp_integration.md
│   ├── 3_a2a_collaboration.md
│   ├── 4_shared_context.md
│   └── 5_enterprise_governance.md
└── templates/
    ├── agent_manifest.json.tpl
    └── TOOL.md.tpl
```

### 2.1. `SKILL.md` - The Core Workflow

The main `SKILL.md` file will serve as the primary guide for creating a multi-agent skill. It will define a new, more detailed workflow that extends the original `skill-creator` process.

**Key Sections:**

1.  **Introduction**: Briefly explains the purpose of creating multi-agent skills and the core principles.
2.  **Phase 1: Conceptualization & Design**: Guides the developer to think about the agent's role in a multi-agent ecosystem. *What unique capability does this agent provide? How will it interact with others?*
3.  **Phase 2: Initialization**: Instructs the use of the new `init_multi_agent_skill.py` script to scaffold a skill with the necessary multi-agent components.
4.  **Phase 3: Implementation**: This is the main phase, broken down into sub-steps, each pointing to a detailed guide in the `references/` directory:
    *   Defining the Agent's Core Logic (→ `references/1_foundations.md`)
    *   Integrating Tools & Data via MCP (→ `references/2_mcp_integration.md`)
    *   Enabling Collaboration via A2A (→ `references/3_a2a_collaboration.md`)
    *   Managing Shared Context (→ `references/4_shared_context.md`)
    *   Implementing Enterprise Governance (→ `references/5_enterprise_governance.md`)
5.  **Phase 4: Validation & Testing**: Details how to use the `validate_multi_agent_skill.py` script to check for compliance with multi-agent standards.
6.  **Phase 5: Delivery**: Standard skill delivery process.

### 2.2. Bundled Resources

#### Scripts

*   `init_multi_agent_skill.py`: This script will be an enhanced version of the original `init_skill.py`. It will generate a skill directory that includes not only the standard files but also the `agent_manifest.json` and a more detailed `TOOL.md` template, preparing the skill for a multi-agent environment.
*   `validate_multi_agent_skill.py`: A new validation tool that checks for specific multi-agent requirements, such as the presence and validity of the `agent_manifest.json`, proper MCP tool definitions, and declared A2A capabilities.

#### Reference Documents

These detailed guides form the educational core of the skill:

*   `1_foundations.md`: Covers the basics of agentic design, including state management, error handling, and defining a clear purpose (Job to be Done).
*   `2_mcp_integration.md`: Provides a step-by-step guide for making a skill an MCP-compliant tool provider. It will explain how to define tool schemas, handle requests, and return data in the standardized MCP format.
*   `3_a2a_collaboration.md`: Explains the A2A protocol. It will provide patterns for agent discovery, task negotiation (e.g., offer/accept/reject), and asynchronous communication.
*   `4_shared_context.md`: Details the 
proposed mechanism for managing and sharing context between agents. It will advocate for a centralized, file-based approach similar to OpenClaw's `TOOLS.md`, where agents can read and write to a shared knowledge base to maintain state and awareness of the broader system.
*   `5_enterprise_governance.md`: This guide will provide concrete patterns for building enterprise-ready agents. Topics will include structured logging for auditability, role-based access control for tools, error handling with retries, and strategies for human-in-the-loop oversight.

#### Templates

*   `agent_manifest.json.tpl`: A template for the `agent_manifest.json` file. This file will be a standard part of every multi-agent skill, declaring its capabilities, the MCP tools it exposes, and the A2A protocols it supports. This manifest allows for automatic discovery and registration of agents within the ecosystem.
*   `TOOL.md.tpl`: An advanced template for the `TOOL.md` file (inspired by OpenClaw). This file will serve as the skill's internal, persistent memory, storing instance-specific information like API keys, project IDs, and user preferences. The template will provide a structured format for this data.

## 3. References

[1] TrendHunter. (2026, February 18). *Actionable Agent: AI systems that execute tasks end-to-end gain popularity with consumers*. 
[2] ForwardFuture. (n.d.). *OpenClaw: What People Are Actually Doing With It*.
[3] Anthropic. (2024, November 25). *Introducing the Model Context Protocol*. https://www.anthropic.com/news/model-context-protocol
[4] Google Developers. (2025, April 9). *Announcing the Agent2Agent Protocol (A2A)*. https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/
