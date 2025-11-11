---
mode: 'agent'
tools: ['search', 'usages', 'think']
description: 'Explain why code was written in a seemingly strange or unconventional way'
---

You are analyzing code that appears unusual, non-idiomatic, or overly complex. Your goal is to understand and explain the reasoning behind implementation choices that might seem strange at first glance.

## Prerequisites

This prompt works best when you have:
- A specific file or code section open (${file})
- The current selection (${selection}) to analyze, OR
- A specific line range or function name to investigate

If no specific code is highlighted, ask the user which code section they find puzzling.

## Investigation Strategy

When encountering seemingly strange code, systematically investigate these factors:

### 1. Historical Context
- **When was this written?** Check git blame to find the date
- **What was the technology landscape then?** Consider:
  - Framework/language versions at that time
  - Available libraries and tools
  - Best practices that were current then vs. now
  - Browser/platform capabilities of that era
- **Who wrote it?** Check author and their commits around that time
- **Related commits:** Look at nearby commits for context clues

### 2. Bug Fixes & Workarounds
- **Search for related issue references:** Look for:
  - Issue numbers in commits
  - Bug tracker references (GitHub issues, JIRA, etc.)
  - Comments mentioning "bug", "fix", "workaround", "hack"
- **External dependency quirks:** Check if working around:
  - Third-party library bugs
  - Framework limitations
  - Browser inconsistencies
  - API oddities
- **Edge case handling:** Might be addressing:
  - Race conditions
  - Timing issues
  - Null/undefined edge cases
  - Floating point precision
  - Memory leaks
  - Performance issues

### 3. Performance Optimization
- **Is this optimized for speed?** Look for:
  - Cache warming
  - Pre-computation
  - Loop unrolling
  - Avoiding allocations
  - Minimizing function calls
  - Reducing garbage collection pressure
- **Memory optimization:** Check for:
  - Object pooling
  - Manual memory management
  - Avoiding large object creation
- **Network optimization:** Consider:
  - Request batching
  - Prefetching
  - Connection pooling

### 4. Backward Compatibility
- **Legacy API support:** Maintaining compatibility with:
  - Old clients
  - Deprecated endpoints
  - Previous versions
  - External integrations
- **Data migration support:** Handling:
  - Old data formats
  - Schema evolution
  - Versioned data structures
- **Feature flag transitions:** Supporting both old and new behavior

### 5. Business Rules & Domain Constraints
- **Regulatory requirements:** Such as:
  - Financial calculations (precision requirements)
  - Tax laws
  - Industry standards
  - Compliance requirements
- **Business logic requirements:**
  - Complex domain rules
  - Exception handling for specific customers
  - Special case processing
- **Contractual obligations:** Meeting specific SLA or API contracts

### 6. Concurrency & Threading
- **Thread safety:** Unusual patterns might be:
  - Avoiding race conditions
  - Ensuring atomicity
  - Lock-free algorithms
  - Memory barriers
- **Event ordering:** Ensuring:
  - Happens-before relationships
  - Serialization guarantees
  - Idempotency

### 7. Security Considerations
- **Security hardening:** Such as:
  - Input sanitization
  - Timing attack prevention
  - Side-channel attack mitigation
  - Constant-time operations
  - Defense in depth
- **Authorization checks:** Complex authorization logic
- **Data protection:** Encryption, masking, or secure handling

### 8. Platform-Specific Constraints
- **Operating system limitations:** Handling:
  - File system differences
  - Path separators
  - Case sensitivity
  - Line endings
- **Runtime environment:** Dealing with:
  - Container constraints
  - Cloud platform limitations
  - Deployment environment specifics
- **Browser/client differences:** Handling:
  - Polyfills
  - Browser bugs
  - Feature detection
  - Graceful degradation

### 9. Testing & Mockability
- **Testability concerns:** Code structured to:
  - Allow dependency injection
  - Enable mocking
  - Facilitate testing
  - Isolate side effects

### 10. Migration & Transition States
- **Gradual migration:** Temporarily supporting:
  - Old and new systems
  - Dual writes
  - Shadow testing
  - Canary deployments
- **Incomplete refactoring:** Caught mid-transition

### 11. External Dependencies
- **API limitations:** Working around:
  - Rate limits
  - Pagination requirements
  - Batch size limits
  - Timeout constraints
- **Library constraints:** Adapting to:
  - Library API design
  - Version incompatibilities
  - Missing features

### 12. Error Handling & Resilience
- **Retry logic:** Complex retry patterns for:
  - Transient failures
  - Network issues
  - Backoff strategies
- **Circuit breakers:** Preventing cascade failures
- **Fallback behavior:** Graceful degradation

## Investigation Process

1. **Read the code carefully** - Understand what it actually does
2. **Check git history** - Look at when and why it was introduced by running relevant git commands in the terminal
3. **Search for related code** - Find similar patterns or calling code
4. **Look for documentation** - Check comments, commit messages, issue references. If you have access to documentation through an MCP server, make queries there.
5. **Examine test cases** - Tests might reveal edge cases being handled
6. **Check related files** - Look at files changed in the same commits
7. **Search for patterns** - Is this pattern used elsewhere? Why?
8. **Consider the alternatives** - What would "normal" code look like, and why not use that?

## Output Format

Provide your analysis in this structure:

### Code Analysis: [Function/Section Name]

**Location**: `${file}` [line numbers]

**The Puzzling Code**:
```[language]
[Show the confusing code snippet]
```

**What Makes It Strange**:
- List what appears unusual or non-idiomatic

**Investigation Findings**:

#### Most Likely Reason: [Primary Explanation]
[Detailed explanation of the most probable reason]

**Evidence**:
- Git commit: [commit hash] - [commit message]
- Date: [when it was introduced]
- [Other supporting evidence]

#### Contributing Factors:
1. **[Factor Category]**: [Explanation]
2. **[Factor Category]**: [Explanation]

#### Historical Context:
[If relevant, explain the state of technology/practices when this was written]

#### Alternative Approaches:
**Modern approach would be**:
```[language]
[Show how this would typically be written today]
```

**Why the original approach might still be valid**:
- [Reasons to keep the current implementation]

**Why it might be worth refactoring**:
- [Reasons to consider changing it]

### Confidence Level: [High/Medium/Low]

**Known Facts**:
- [Things you found concrete evidence for]

**Reasonable Inferences**:
- [Things you can infer with good confidence]

**Speculation**:
- [Things that are possible but not confirmed]

### Recommendations:

1. **Document it**: [Suggest adding a comment explaining the reasoning]
2. **Keep or refactor**: [Your recommendation based on findings]
3. **Further investigation**: [What else to check if unsure]

## Important Guidelines

- **Don't assume incompetence** - There's usually a good reason, even if not obvious
- **Consider the context of when it was written** - Best practices evolve
- **Look for evidence, not just theories** - Check git history, comments, issues
- **Multiple factors often combine** - It might be a performance fix AND a workaround
- **Be humble about speculation** - Clearly distinguish facts from educated guesses
- **Provide actionable insights** - Should we keep it, document it, or refactor it?

## Common Patterns to Recognize

- **The Browser Wars Era**: Old browser compatibility code
- **The Callback Era**: Code written before async/await
- **The No-Framework Era**: Manual DOM manipulation, XHR handling
- **The Performance Crisis**: Over-optimization from a past crisis
- **The Quick Fix That Stayed**: Temporary workarounds that became permanent
- **The Framework Migration**: Code supporting two frameworks at once
- **The Vendor Bug**: Workarounds for specific versions of dependencies

Work systematically through the investigation checklist until you understand the reasoning. Don't stop at the first plausible explanation - look for evidence.
