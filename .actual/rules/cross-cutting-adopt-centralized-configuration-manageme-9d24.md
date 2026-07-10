# Adopt Centralized Configuration Management for Public-Facing Application Entry Points

These rules are ALWAYS ACTIVE for all public-facing application entry points, including framework-specific configuration files such as `_document.tsx`, `layout.tsx`, and `theme.config.tsx` in the docs and demo applications.

### Rules

- **R-CONFIG-001** MUST: Implement centralized runtime configuration management at application entry points using framework-specific configuration files (_document.tsx for Next.js pages, layout.tsx for Next.js app router, theme.config.tsx for documentation theming).
- **R-CONFIG-002** MUST: Establish each public-facing application's configuration sources at the root level through dedicated configuration files that serve as the single source of truth for runtime settings, theming, and layout specifications.
- **R-CONFIG-003** SHOULD: Leverage framework conventions to provide consistent configuration initialization across different application types within the monorepo.
- **R-CONFIG-004** SHOULD: Ensure configuration at entry points is applied before any component rendering to prevent configuration-related runtime errors.
- **R-CONFIG-005** SHOULD: Abstract shared configuration logic into reusable modules to minimize duplication across multiple configuration files.
- **R-CONFIG-006** MAY: Document framework-specific configuration patterns to reduce cognitive load and improve maintainability for developers.

### Verify

```bash
# Verify centralized configuration files exist at application entry points
find . -path './docs' -name '_document.tsx' -o -name 'layout.tsx' -o -name 'theme.config.tsx' | wc -l

# Verify configuration files are at root level of their respective applications
ls -la docs/layout.tsx demo/_document.tsx 2>/dev/null || echo "Entry point files not found"

# Verify no duplicate configuration logic across entry points
grep -r "configuration\|config" docs/layout.tsx demo/_document.tsx | sort | uniq -d
```

**Accept when:**
- All public-facing applications (docs, demo) have dedicated configuration files at their entry points
- Configuration files follow framework conventions (_document.tsx, layout.tsx, theme.config.tsx)
- Configuration is applied before component rendering
- Shared configuration logic is abstracted into reusable modules
- No configuration-related runtime errors occur during application startup

<enforcement>
Claude Code MUST NOT skip or defer verification of centralized configuration management at application entry points.
</enforcement>