# Adopt Centralized Test Helper and Mocking Infrastructure for Component Testing

These rules are ALWAYS ACTIVE for all test files in `__tests__` and `__helpers__` directories across core packages including component resolution, UI components, reducer actions, and migration logic.

### Rules

- **R-TEST-001** MUST: Create and maintain centralized test helpers in `__helpers__/index.tsx` for common test setup, teardown, and utility operations.
- **R-TEST-002** MUST: Use the `.spec.tsx` convention for all React component test files with TypeScript.
- **R-TEST-003** MUST: Implement standardized mock implementations for component data resolution and reuse them across test suites.
- **R-TEST-004** SHOULD: Provide shared fixtures and utilities that can be imported across test suites to ensure consistency in testing approach.
- **R-TEST-005** SHOULD: Design test helpers with proper separation of concerns to avoid unnecessary coupling between tests.
- **R-TEST-006** MAY: Extend helper infrastructure as new testing patterns emerge, but avoid over-abstraction that solves too many problems.

### Verify

```bash
# Check for centralized test helpers directory
test -d "__helpers__" || echo "Missing __helpers__ directory"

# Verify test helper exports exist
grep -l "export" "__helpers__/index.tsx" || echo "No exports in test helpers"

# Check for .spec.tsx test files
find . -name "*.spec.tsx" | head -5

# Verify mock implementations are reused
grep -r "from.*__helpers__" __tests__/ | wc -l

# Check for consistent test patterns
grep -r "describe\|it\|test" __tests__/ | head -10
```

**Accept when:**
- `__helpers__/index.tsx` exists and exports reusable test utilities
- All React component tests follow the `.spec.tsx` naming convention
- Mock implementations for component data resolution are centralized and reused
- Test files import helpers from the centralized `__helpers__` directory
- Test setup and teardown operations are consistent across test suites
- Helper functions maintain clear separation of concerns

<enforcement>
Claude Code MUST NOT skip or defer verification. All test files must conform to centralized helper patterns before merge.
</enforcement>