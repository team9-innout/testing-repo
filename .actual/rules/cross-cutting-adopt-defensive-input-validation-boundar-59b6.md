# Adopt Defensive Input Validation and Boundary Checking for Configuration and Environment Management

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-DEFENSIVE-001** MUST: Validate environment variables and configuration values before use, implementing type guards and runtime checks for dynamic inputs.
- **R-DEFENSIVE-002** MUST: Provide fallback values for missing or invalid configuration to enable safe defaults and graceful degradation.
- **R-DEFENSIVE-003** MUST: Sanitize user inputs in form fields and UI components at system boundaries.
- **R-DEFENSIVE-004** SHOULD: Establish clear contracts at module boundaries where configuration data flows between layers (routes, models, hooks, components).
- **R-DEFENSIVE-005** SHOULD: Apply validation logic consistently across server-side routes, data models, client-side hooks, and UI components.
- **R-DEFENSIVE-006** SHOULD: Provide clear error messages and debugging information when configuration issues occur.
- **R-DEFENSIVE-007** MAY: Implement validation utilities and helper functions to reduce code duplication and maintain consistency.

### Verify

```bash
# Check for environment variable validation at entry points
grep -r "process\.env" --include="*.ts" --include="*.tsx" --include="*.js" --include="*.jsx" | grep -v "||" | grep -v "??" | wc -l

# Verify type guards exist for configuration objects
grep -r "typeof.*===" --include="*.ts" --include="*.tsx" | grep -c "config\|env\|settings"

# Check for fallback values in configuration handling
grep -r "\?\?" --include="*.ts" --include="*.tsx" | grep -c "config\|env"

# Verify input sanitization in form components
grep -r "trim()\|sanitize\|validate" --include="*.tsx" | grep -c "input\|form"
```

**Accept when:**
- All environment variables are accessed with type guards or fallback values
- Configuration boundaries have explicit validation logic
- User inputs in forms are sanitized before processing
- Error messages provide actionable debugging information
- Validation logic is reused across multiple layers rather than duplicated
- Module boundaries clearly document expected configuration shape

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>