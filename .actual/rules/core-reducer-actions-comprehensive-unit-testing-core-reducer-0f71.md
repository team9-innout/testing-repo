# Comprehensive Unit Testing for Core Reducer Actions

These rules are ALWAYS ACTIVE for all files in the `packages/core/reducer/actions/` directory and their corresponding test specifications.

### Rules

- **R-CORE-REDUCER-001** MUST: Implement dedicated unit test files for each core reducer action (duplicate, move, set-ui, replace, insert) in the `packages/core/reducer/actions/__tests__/` directory.
- **R-CORE-REDUCER-002** MUST: Follow the naming convention `[action-name].spec.ts` for all reducer action test files.
- **R-CORE-REDUCER-003** MUST: Ensure each action test file provides comprehensive test coverage with clear separation of concerns.
- **R-CORE-REDUCER-004** SHOULD: Maintain test coverage significance at or above 91.70% for core state management logic.
- **R-CORE-REDUCER-005** SHOULD: Use isolated test files to enable parallel test execution and optimize CI/CD pipeline performance.
- **R-CORE-REDUCER-006** SHOULD: Document expected behavior of each action through test cases to serve as living documentation.
- **R-CORE-REDUCER-007** MAY: Coordinate test coverage with integration tests to minimize duplication while maintaining comprehensive validation.

### Verify

```bash
# Verify test files exist for all core reducer actions
test -f packages/core/reducer/actions/__tests__/duplicate.spec.ts && \
test -f packages/core/reducer/actions/__tests__/move.spec.ts && \
test -f packages/core/reducer/actions/__tests__/set-ui.spec.ts && \
test -f packages/core/reducer/actions/__tests__/replace.spec.ts && \
test -f packages/core/reducer/actions/__tests__/insert.spec.ts

# Verify test coverage meets threshold
npm run test:coverage -- packages/core/reducer/actions --coverage-threshold=91.70

# Verify test naming conventions
find packages/core/reducer/actions/__tests__/ -name '*.spec.ts' | grep -E '(duplicate|move|set-ui|replace|insert)\.spec\.ts$'
```

**Accept when:**
- All five core reducer action test files exist with correct naming convention
- Test coverage for core reducer actions meets or exceeds 91.70%
- Each test file contains isolated test cases for its corresponding action
- Tests execute successfully in parallel without conflicts
- Test cases document expected behavior and state transitions

<enforcement>
Claude Code MUST NOT skip or defer verification of test file existence, naming conventions, and coverage thresholds before approving changes to core reducer actions.
</enforcement>