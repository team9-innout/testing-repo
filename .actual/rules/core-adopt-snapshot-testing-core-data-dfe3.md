# Adopt Snapshot Testing for Core Data Transformation and State Management Logic

These rules are ALWAYS ACTIVE for all files matching the configured scope: core data transformation functions (walk-tree, walk-app-state), reducer actions, and state management operations that produce structured outputs involving nested data structures, tree traversals, and state mutations.

### Rules

- **R-SNAPSHOT-001** MUST: Implement snapshot testing for core data transformation functions and reducer actions in `__tests__` directories co-located with source code (e.g., `packages/core/reducer/actions/__tests__/`, `packages/core/lib/data/__tests__/`).
- **R-SNAPSHOT-002** MUST: Store snapshots as serialized, version-controlled files alongside test code to capture complete output of operations like tree walking, state transformations, and reducer actions.
- **R-SNAPSHOT-003** MUST: Validate entire output structures in a single test rather than using granular assertions for each property and nested element.
- **R-SNAPSHOT-004** SHOULD: Use snapshot testing specifically for the `testing.snapshot` facet within the CI/CD pipeline to ensure output consistency across builds.
- **R-SNAPSHOT-005** SHOULD: Review snapshot diffs carefully during code review to detect unintended changes to output structure.
- **R-SNAPSHOT-006** MAY: Update snapshots in bulk when intentional changes occur, rather than modifying multiple individual assertions.
- **R-SNAPSHOT-007** SHOULD: Avoid blindly updating snapshots without carefully reviewing changes to prevent masking bugs.

### Verify

```bash
# Verify snapshot test files exist in __tests__ directories
find packages/core -path '*__tests__*' -name '*.test.ts' -o -name '*.spec.ts' | grep -E '(reducer/actions|lib/data)' | head -5

# Verify snapshot files are version-controlled
find packages/core -name '*.snap' | head -5

# Verify snapshot tests target complex data structures
grep -r "expect.*toMatchSnapshot" packages/core --include="*.test.ts" --include="*.spec.ts" | wc -l

# Verify CI/CD pipeline includes snapshot testing facet
grep -r "testing.snapshot" .github/workflows/ .gitlab-ci.yml .circleci/ 2>/dev/null || echo "(CI/CD snapshot facet configuration not found in standard locations)"
```

**Accept when:**
- Snapshot test files exist in `__tests__` directories co-located with core data transformation and reducer action source code
- Snapshot files (`.snap`) are committed to version control alongside test files
- Tests validate complete output structures using `toMatchSnapshot()` or equivalent rather than granular assertions
- Snapshot testing is integrated into the CI/CD pipeline's `testing.snapshot` facet
- Developers review snapshot diffs during code review before approving changes
- Snapshot updates are intentional and documented in commit messages

<enforcement>
Claude Code MUST NOT skip or defer verification. All snapshot tests for core data transformation and state management logic MUST follow these rules to ensure comprehensive output validation and regression prevention.
</enforcement>