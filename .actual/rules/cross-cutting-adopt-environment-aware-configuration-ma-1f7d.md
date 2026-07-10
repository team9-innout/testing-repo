# Adopt Environment-Aware Configuration Management Across Application Layers

These rules are ALWAYS ACTIVE for all files matching the configured scope, including server-side routes (Remix), data models, UI components, and custom hooks across both application and library layers.

### Rules

- **R-ENV-001** MUST: Implement a centralized configuration pattern accessible across all architectural layers (server routes, models, client components, hooks).
- **R-ENV-002** MUST: Provide consistent access to environment variables and runtime configuration without coupling components to specific environment detection mechanisms.
- **R-ENV-003** SHOULD: Use dependency injection or context-based approaches to make configuration mockable and testable across different component types.
- **R-ENV-004** SHOULD: Document the configuration structure and what settings are available to prevent implicit dependencies.
- **R-ENV-005** MAY: Implement feature flags and environment-specific behavior through the centralized configuration pattern rather than hardcoding values.
- **R-ENV-006** MUST: Avoid configuration bloat by establishing clear governance on what should be configured versus hardcoded.

### Verify

```bash
# Check for centralized configuration module/pattern
grep -r "config\|Config\|configuration" --include="*.ts" --include="*.tsx" --include="*.js" --include="*.jsx" | grep -E "(export|import).*config" | head -20

# Verify configuration is not hardcoded in multiple places
grep -r "process\.env" --include="*.ts" --include="*.tsx" --include="*.js" --include="*.jsx" | wc -l

# Check for consistent pattern usage across layers
grep -r "useConfig\|getConfig\|ConfigContext" --include="*.ts" --include="*.tsx" --include="*.js" --include="*.jsx" | wc -l

# Verify test files can mock configuration
grep -r "mock.*config\|jest\.mock.*config" --include="*.test.ts" --include="*.test.tsx" --include="*.spec.ts" --include="*.spec.tsx" | wc -l
```

**Accept when:**
- A centralized configuration module or pattern exists and is imported consistently across server routes, models, components, and hooks
- Environment variables are accessed through the centralized pattern rather than scattered `process.env` calls
- Configuration can be mocked or injected in test files without modifying component code
- Configuration structure is documented and governance rules are established for what gets configured
- Feature flags and environment-specific behavior are implemented through the configuration pattern

<enforcement>
Claude Code MUST NOT skip or defer verification. All rules must be checked before accepting changes to files in scope.
</enforcement>