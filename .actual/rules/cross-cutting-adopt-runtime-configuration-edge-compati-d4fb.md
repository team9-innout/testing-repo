# Adopt Runtime Configuration with Edge-Compatible Execution Model

These rules are ALWAYS ACTIVE for all API routes (route.ts files), server components, and client components in Next.js applications that support multiple runtime environments (Node.js and Edge).

### Rules

- **R-RUNTIME-001** MUST: Explicitly declare runtime configuration at the route level using `export const runtime` declarations in API routes to specify execution environment ('edge' or 'nodejs').
- **R-RUNTIME-002** MUST: Separate client-side and server-side execution concerns through explicit file naming conventions (e.g., `client.tsx` for client components) and runtime declarations.
- **R-RUNTIME-003** SHOULD: Implement environment-specific configuration management that adapts to the declared runtime, enabling feature flags and optimizations based on runtime capabilities.
- **R-RUNTIME-004** SHOULD: Establish consistent patterns for handling concurrency models that work across both Edge and Node.js runtimes.
- **R-RUNTIME-005** MAY: Optimize for Edge runtime where applicable to reduce cold start times and improve global distribution, provided Edge runtime limitations (e.g., no native Node.js modules) are respected.

### Verify

```bash
# Check for explicit runtime declarations in API routes
grep -r "export const runtime" src/app/api --include="route.ts" || echo "No runtime declarations found"

# Verify client component naming conventions
find src -name "*.client.tsx" -o -name "*client.tsx" | head -20

# Check for environment-specific configuration patterns
grep -r "process.env.NODE_ENV\|runtime ===" src --include="*.ts" --include="*.tsx" | head -20

# Validate separation of concerns in component structure
find src -type f \( -name "*.tsx" -o -name "*.ts" \) -exec grep -l "'use client'" {} \; | head -20
```

**Accept when:**
- All API routes in `src/app/api` explicitly declare `export const runtime` with either 'edge' or 'nodejs'
- Client components are clearly marked with `'use client'` directive or follow `.client.tsx` naming convention
- Environment-specific logic is isolated and documented with clear runtime requirements
- No runtime mismatches exist between declared runtime and actual module dependencies
- Concurrency patterns are consistent across both runtime environments

<enforcement>
Claude Code MUST NOT skip or defer verification. All runtime declarations must be validated before accepting changes to API routes or components that interact with multiple execution environments.
</enforcement>