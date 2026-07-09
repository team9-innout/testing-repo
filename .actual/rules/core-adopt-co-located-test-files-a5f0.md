# Adopt Co-located Test Files with __tests__ Directory Pattern for Component and Library Testing

These rules are ALWAYS ACTIVE for all test files in component and library directories across the monorepo.

### Rules

- **R-TEST-001** MUST: Place test files in `__tests__` directories adjacent to the code they test.
- **R-TEST-002** MUST: Use the `.spec.tsx` extension for all test files to indicate TypeScript/TSX test modules.
- **R-TEST-003** MUST: Apply the co-located `__tests__` pattern consistently across component testing (e.g., `components/Puck/__tests__/index.spec.tsx`) and library function testing (e.g., `lib/__tests__/resolve-component-data.spec.tsx`).
- **R-TEST-004** SHOULD: Name test files descriptively to mirror the tested modules (e.g., test file for `migrate.ts` should be `migrate.spec.tsx`).
- **R-TEST-005** SHOULD: Maintain clear separation between production code and test code through dedicated `__tests__` directories.
- **R-TEST-006** MAY: Exclude `__tests__` directories from production builds using standard glob patterns (`**/__tests__/**`).

### Verify

```bash
# Check that all test files follow the __tests__/__*.spec.tsx pattern
find . -path './node_modules' -prune -o -type f -name '*.spec.tsx' -print | grep -E '__tests__/.*\.spec\.tsx$'

# Verify no test files exist outside __tests__ directories
find . -path './node_modules' -prune -o -type f \( -name '*.test.tsx' -o -name '*.test.ts' \) -print | grep -v '__tests__'

# Confirm __tests__ directories are present for major component and lib modules
find ./packages/*/src/components -type d -name '__tests__' | head -5
find ./packages/*/src/lib -type d -name '__tests__' | head -5
```

**Accept when:**
- All test files are located in `__tests__` directories adjacent to their corresponding source code
- All test files use the `.spec.tsx` extension
- Test file names mirror the modules they test
- No test files exist outside `__tests__` directories
- The pattern is applied consistently across all packages in the monorepo

<enforcement>
Claude Code MUST NOT skip or defer verification. Test file organization MUST conform to the co-located `__tests__` pattern with `.spec.tsx` naming before code review approval.
</enforcement>