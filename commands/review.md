---
name: review
description: Comprehensive code review with architecture and security focus
---

Perform a thorough code review of the current changes or specified files.

## Review Process

1. **First, understand the context**
   - What problem is being solved?
   - What's the scope of changes?

2. **Check code quality**
   - Logic correctness
   - Error handling
   - Edge cases
   - Test coverage

3. **Assess architecture impact**
   - Does this fit the existing patterns?
   - Are there scaling concerns?
   - Is the abstraction level appropriate?

4. **Security scan**
   - Input validation
   - Authentication/authorization
   - Sensitive data handling
   - Injection vulnerabilities

5. **Provide actionable feedback**
   - Categorize as: blocker, suggestion, nitpick
   - Explain the "why" for each comment
   - Suggest specific fixes

Begin by asking what should be reviewed, or analyze staged/uncommitted changes.
