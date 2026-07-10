# Adopt Component-Based Public API Architecture with Plugin System

These rules are ALWAYS ACTIVE for all files matching the configured scope, including configuration files, core UI components, plugins, API routes, and custom React hooks that form the public API surface.

### Rules

- **R-API-001** MUST: Implement clear separation between public API surface and internal implementation details.
- **R-API-002** MUST: Expose well-defined interfaces through configuration-driven component registration (puck.config.tsx pattern).
- **R-API-003** MUST: Maintain modular core components with stable public interfaces.
- **R-API-004** SHOULD: Provide plugin architecture for extensibility that allows third-party developers to add functionality without modifying core.
- **R-API-005** SHOULD: Implement RESTful API endpoints for external integrations following consistent patterns.
- **R-API-006** SHOULD: Expose custom React hooks as reusable API primitives following React best practices.
- **R-API-007** SHOULD: Support multiple integration points (components, hooks, plugins, REST APIs) for diverse use cases.
- **R-API-008** SHOULD: Treat components, hooks, and plugins as first-class API citizens with consistent documentation.
- **R-API-009** MAY: Extend the API surface only after evaluating impact on stability and backward compatibility.
- **R-API-010** MUST: Document all public API patterns to reduce learning curve for external developers.

### Verify

```bash
# Verify public API surface is clearly documented
grep -r "export" src/ | grep -E "(component|hook|plugin|api)" | wc -l

# Verify configuration-driven registration pattern exists
find . -name "*.config.*" -o -name "*config*" | xargs grep -l "register\|plugin" 2>/dev/null

# Verify plugin system structure
find . -path "*/plugins/*" -type f | head -20

# Verify custom hooks follow naming convention
find . -name "use-*.ts" -o -name "use-*.tsx" | wc -l

# Verify API routes exist and are documented
find . -path "*/api/*" -type f | head -20
```

**Accept when:**
- Public API surface is clearly separated from internal implementation
- Configuration-driven component registration pattern is consistently applied
- Plugin system allows extensibility without core modifications
- Custom hooks follow React conventions and are properly exported
- RESTful API endpoints are documented and follow consistent patterns
- Multiple integration points are available and documented for external consumers
- Backward compatibility considerations are documented for API changes
- All public APIs have corresponding documentation or examples

<enforcement>
Claude Code MUST NOT skip or defer verification. All rules must be checked before approving changes to public API surface, configuration files, plugin implementations, API routes, or custom hooks.
</enforcement>