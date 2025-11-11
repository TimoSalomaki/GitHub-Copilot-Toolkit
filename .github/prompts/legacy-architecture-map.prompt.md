---
mode: 'agent'
tools: ['search', 'runCommands', 'Azure MCP/search', 'usages', 'think', 'todos']
description: 'Generate or refine a comprehensive architecture map of the legacy codebase'
---

You are analyzing a legacy codebase to create or refine a comprehensive architecture map. Your goal is to systematically explore the codebase and document its structure, components, and relationships.

## Initial Analysis Mode

If no existing architecture map is provided, perform a complete analysis:

1. **Identify Entry Points**: Locate main application entry points (main files, server startup, app initialization)
2. **Map Core Modules**: Identify major modules, packages, or namespaces and their responsibilities
3. **Document Layers**: Identify architectural layers (presentation, business logic, data access, infrastructure)
4. **Find Key Components**: Locate critical components (controllers, services, repositories, utilities)
5. **Trace Data Flow**: Document how data flows through the system
6. **Identify External Dependencies**: Map third-party libraries, frameworks, and external services
7. **Database Connections**: Document database access patterns and connection points
8. **Configuration Systems**: Identify how configuration is managed
9. **Build & Deployment**: Document build systems, deployment configurations

Continue exploring until you have a comprehensive view of the entire architecture. Search broadly, then drill into specifics.

## Refinement Mode

If an existing architecture map is provided in the chat (as a file reference or pasted content):

1. **Gap Analysis**: Review the existing map and identify missing components or modules
2. **Verify Accuracy**: Check if documented components still exist and are accurately described
3. **Find New Patterns**: Look for architectural patterns not previously documented
4. **Deepen Understanding**: Add more detail to high-level descriptions
5. **Update Dependencies**: Verify and update external dependency information
6. **Cross-Reference**: Ensure all referenced components are documented

Work iteratively until all gaps are filled and the map is complete.

## Current File Context

If a specific file is currently open (${file}), use it as a starting point:
- Determine which architectural component this file belongs to
- Trace its dependencies and dependents
- Place it in the broader architectural context

## Output Format

Provide the architecture map as a structured Markdown document with:

- **Executive Summary**: High-level overview of the system architecture
- **System Layers**: Description of each architectural layer
- **Core Modules**: Detailed breakdown of major modules with responsibilities
- **Component Relationships**: How components interact (use Mermaid diagrams)
- **External Dependencies**: Third-party services, libraries, databases
- **Data Flow**: How data moves through the system
- **Configuration & Deployment**: Build and deployment architecture
- **Key Findings**: Important architectural decisions, patterns, or concerns
- **Coverage Notes**: Areas that need further investigation

Use Mermaid diagrams where appropriate to visualize relationships.

## Instructions

- Search systematically through the codebase until you have comprehensive coverage
- Look for README files, documentation, and comments that explain architecture. You MUST consider source code as the source of truth, documentation can be outdated.
- Examine package structures, import statements, and module boundaries
- Identify common patterns (MVC, layered architecture, microservices, etc.)
- If information is unclear, document assumptions and areas needing clarification
- Work until the map is thorough - don't stop prematurely
