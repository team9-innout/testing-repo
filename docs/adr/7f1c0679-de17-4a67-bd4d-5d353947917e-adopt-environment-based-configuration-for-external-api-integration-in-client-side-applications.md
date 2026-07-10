The codebase contains multiple client-facing applications (documentation site and demo app) that need to integrate with external APIs and services. These applications require secure configuration management for API keys, endpoints, and other sensitive credentials while maintaining separation between different deployment environments (development, staging, production). The pattern emerged across layout and configuration files (_document.tsx, layout.tsx, theme.config.tsx) which are critical entry points for application initialization and external service integration. The challenge is to manage secrets and API configurations securely in client-side applications without exposing sensitive credentials in the codebase or to end users.

## Policies
- Implement environment-based configuration management using environment variables for all external API integrations in public-facing applications. This approach centralizes API configuration in application layout and theme configuration files, using runtime environment variable injection to manage secrets. The pattern ensures that API keys and sensitive configuration are never hardcoded in source code, are environment-specific, and are properly scoped to server-side or build-time contexts where appropriate. Configuration is initialized at the application root level (document/layout components) to ensure consistent availability throughout the component tree.

## Instructions
- Positive: Secrets and API keys are never committed to version control, reducing security risks
- Positive: Environment-specific configurations enable seamless deployment across development, staging, and production environments
- Positive: Centralized configuration in layout/document files provides a single source of truth for external API integration
- Positive: Consistent pattern across multiple applications (docs and demo) improves maintainability and developer understanding
- Positive: Build-time environment variable injection allows for optimization and dead code elimination
- Negative: Requires proper CI/CD pipeline configuration to inject environment variables at build/deploy time
- Negative: Client-side exposure of certain API keys may still be necessary for some services, requiring careful evaluation of which keys can be safely exposed
- Negative: Debugging configuration issues may be more complex as values are not visible in source code
- Negative: Developers need access to environment variable documentation and example configurations to set up local development environments