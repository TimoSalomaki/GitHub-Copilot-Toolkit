---
mode: 'agent'
tools: ['runCommands', 'search', 'usages', 'think']
description: 'Trace and analyze dependency chains from the currently active file or refine existing analysis'
---

You are analyzing dependencies in a legacy codebase. Your goal is to trace and document the complete dependency chain for the current file or refine an existing dependency analysis.

## Prerequisites

This prompt requires a file to be active in the editor. The active file is: **${file}**

## Initial Analysis Mode

If no existing dependency analysis is provided, perform a complete dependency chain analysis:

### 1. Outbound Dependencies (What this file depends on)

- **Direct imports/includes**: List all immediate dependencies
- **Transitive dependencies**: Trace dependencies of dependencies (go at least 2-3 levels deep)
- **External packages**: Identify third-party libraries used
- **Framework dependencies**: Note framework-specific dependencies
- **Type dependencies**: Document type/interface dependencies
- **Runtime dependencies**: Identify dynamic imports, reflection, or runtime-loaded dependencies

### 2. Inbound Dependencies (What depends on this file)

- **Direct dependents**: Find all files that import/reference this file
- **Transitive dependents**: Trace dependents of dependents (go at least 2-3 levels deep)
- **Usage patterns**: How is this file typically used by its dependents
- **Public API surface**: What functions/classes are actually used by dependents

### 3. Dependency Analysis

- **Circular dependencies**: Identify any circular dependency patterns
- **Coupling strength**: Assess how tightly coupled this file is to others
- **Dependency depth**: How deep is the dependency tree
- **Critical dependencies**: Identify dependencies that would be difficult to change
- **Unused dependencies**: Find imported but unused dependencies
- **Missing dependencies**: Identify potential missing or implicit dependencies

### 4. Impact Analysis

- **Blast radius**: How many files would be affected by changes to this file
- **Change risk**: Risk level of modifying this file (based on dependent count and usage)
- **Refactoring opportunities**: Suggest ways to reduce coupling or improve structure

Continue tracing dependencies until you have mapped the complete dependency graph around this file.

## Refinement Mode

If an existing dependency analysis is provided (as a file reference or pasted content):

1. **Verify Completeness**: Check if all dependencies were discovered
2. **Find Missing Edges**: Look for dependencies not documented in the existing analysis
3. **Validate Accuracy**: Confirm that documented dependencies still exist
4. **Deepen Analysis**: Add more detail to shallow dependency descriptions
5. **Update Impact Analysis**: Recalculate blast radius and risk assessments
6. **Find New Patterns**: Identify dependency patterns not previously noted

Work iteratively until all gaps are filled.

## Search Strategy

- Start with the active file and search systematically outward
- Use import/require statements to find direct dependencies
- Find dynamic dependencies by searching for runtime loading patterns
- Search for usages of exported functions/classes to find dependents
- Look for configuration files that might inject dependencies
- Check for IoC/DI container configurations
- Examine test files for additional usage patterns
- Continue until the dependency graph is complete

## Output Format

Provide a structured Markdown document with:

### Dependency Tree for `${fileBasename}`

**File Path**: `${file}`

#### Outbound Dependencies
- Level 1 (Direct)
  - List with file paths and what is imported
- Level 2 (Transitive)
  - Continue the tree structure
- External Dependencies
  - Third-party packages

#### Inbound Dependencies (Dependents)
- Level 1 (Direct)
  - List with file paths and how they use this file
- Level 2 (Transitive)
  - Continue the tree structure

#### Dependency Analysis
- **Total Dependencies**: Count
- **Total Dependents**: Count
- **Circular Dependencies**: Yes/No with details
- **Coupling Score**: Assessment (Low/Medium/High)
- **Dependency Depth**: Max depth of dependency tree

#### Impact Analysis
- **Blast Radius**: Number of files potentially affected
- **Change Risk Level**: Low/Medium/High with justification
- **Critical Dependencies**: Dependencies that cannot be easily changed
- **Refactoring Suggestions**: Specific recommendations

#### Dependency Graph
(Provide a Mermaid diagram showing key relationships)

#### Coverage Notes
- Areas that need further investigation
- Assumptions made during analysis
- Dynamic dependencies that may not be fully traceable

## Instructions

- Be thorough - trace dependencies until you have a complete picture
- Don't stop at the first level; go deep into the dependency chain
- Document both direct and indirect dependencies
- Note any unusual dependency patterns or potential issues
- If you encounter dynamic dependencies, document them with caveats
- Consider both compile-time and runtime dependencies
- Look for hidden dependencies (global state, singletons, etc.)
