# Adopt Environment-Based Configuration for External API Integration in Client-Side Applications

These rules are ALWAYS ACTIVE for all client-side application files that integrate with external APIs, including layout components (_document.tsx, layout.tsx), theme configuration files (theme.config.tsx), and any other entry points for application initialization and external service integration.

### Rules

- **R-EX-001** MUST: Never hardcode API keys, secrets, or sensitive credentials in source code.
- **R-EX-002** MUST: Use environment variables for all external API integrations in public-facing applications.
- **R-EX-003** MUST: Initialize API configuration at the application root level (document/layout components) to ensure consistent availability throughout the component tree.
- **R-EX-004** MUST: Ensure secrets and API keys are never committed to version control.
- **R-EX-005** SHOULD: Centralize API configuration in layout and theme configuration files as a single source of truth for external API integration.
- **R-EX-006** SHOULD: Use build-time environment variable injection to enable optimization and dead code elimination.
- **R-EX-007** SHOULD: Maintain environment-specific configurations (development, staging, production) to enable seamless deployment across environments.
- **R-EX-008** MAY: Expose certain API keys on the client side only after careful evaluation of security implications and service requirements.

### Verify

```bash
# Check for hardcoded API keys or secrets in source files
grep -r "api[_-]?key\s*=\s*['\"]" --include="*.tsx" --include="*.ts" --include="*.jsx" --include="*.js" .

# Verify environment variables are used in layout/document/theme config files
grep -l "process.env" _document.tsx layout.tsx theme.config.tsx 2>/dev/null || echo "Warning: environment variables not found in config files"

# Check that .env files are in .gitignore
grep -E "^\.env" .gitignore || echo "Warning: .env files may not be properly ignored"

# Verify no secrets in git history (sample check)
git log -p --all -S "api_key" --oneline | head -5 || echo "No hardcoded secrets found in recent history"
```

**Accept when:**
- No API keys or secrets are hardcoded in source files
- Environment variables are used in all layout, document, and theme configuration files
- .env files and sensitive configuration files are properly listed in .gitignore
- API configuration is initialized at the application root level
- Environment-specific configurations are maintained for different deployment environments
- Build-time environment variable injection is configured in CI/CD pipeline
- Documentation exists for required environment variables and example configurations

<enforcement>
Claude Code MUST NOT skip or defer verification. All rules must be checked before approving changes to client-side application configuration files.
</enforcement>