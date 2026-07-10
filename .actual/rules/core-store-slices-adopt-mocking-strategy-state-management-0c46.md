# Adopt Mocking Strategy for State Management Store Testing in CI/CD Pipeline

These rules are ALWAYS ACTIVE for all store slice test files (nodes, fields, history, permissions) and state management testing within the CI/CD pipeline.

### Rules

- **R-STORE-001** MUST: Mock all external dependencies, API calls, and inter-slice dependencies in store slice unit tests to enable isolated testing without requiring full integration setup.
- **R-STORE-002** MUST: Apply mocking strategy consistently across all store slice tests (nodes, fields, history, permissions) to create a standardized testing pattern.
- **R-STORE-003** SHOULD: Ensure mocks accurately represent edge cases and error conditions to avoid false confidence in test results.
- **R-STORE-004** SHOULD: Keep mock implementations synchronized with real dependencies to prevent divergence from actual behavior.
- **R-STORE-005** MAY: Use parallel test execution when mocks are properly isolated to reduce CI/CD pipeline duration.

### Verify

```bash
# Check that all store slice test files use mocking strategy
grep -r "jest.mock\|vi.mock" src/store/slices/*.test.ts

# Verify mock consistency across test files
find src/store/slices -name "*.test.ts" -exec grep -l "mock" {} \;

# Confirm no external API calls in store slice tests
grep -r "fetch\|http\|axios" src/store/slices/*.test.ts | grep -v "mock" || echo "No unmocked external calls found"

# Validate test execution time improvement
npm test -- --testPathPattern="store/slices" --verbose
```

**Accept when:**
- All store slice test files (nodes, fields, history, permissions) implement mocking for external dependencies
- Mocking strategy is applied consistently across all store slice tests
- Tests execute without requiring external service setup or network calls
- Test results are deterministic and reproducible in CI/CD pipeline
- Mock implementations document their correspondence to real dependencies
- No integration issues are discovered post-deployment due to mock divergence

<enforcement>
Claude Code MUST NOT skip or defer verification of mocking strategy compliance in store slice tests.
</enforcement>