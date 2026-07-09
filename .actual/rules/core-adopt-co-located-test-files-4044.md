# Adopt Co-located Test Files with __tests__ Directory Convention

These rules are ALWAYS ACTIVE for all TypeScript/React component and utility files in the codebase that require unit test coverage.

### Rules

- **R-TEST-001** MUST: Place unit tests in `__tests__` subdirectories adjacent to the source code they test.
- **R-TEST-002** MUST: Use the `.spec.tsx` extension for React component tests and `.spec.ts` for TypeScript utility tests.
- **R-TEST-003** MUST: Apply the `__tests__` convention consistently across all architectural layers: UI components, library utilities, and internal helpers.
- **R-TEST-004** SHOULD: Ensure test files follow Jest's default test discovery patterns and React Testing Library practices for component testing.
- **R-TEST-005** SHOULD: Configure build tools to exclude `__tests__` directories from production bundles.
- **R-TEST-006** MAY: Document the `__tests__` convention in package-level README files for new contributors.

### Verify

```bash
# Verify __tests__ directories exist adjacent to source files
find . -type f \( -name '*.tsx' -o -name '*.ts' \) ! -path './node_modules/*' ! -path './__tests__/*' | while read file; do
  dir=$(dirname "$file")
  if [ -f "${dir}/__tests__/$(basename "$file" | sed 's/\.[^.]*$/.spec.&/')" ]; then
    echo "✓ Test found for $file"
  fi
done

# Verify test file naming convention
find . -path '*/__tests__/*.spec.ts*' ! -path './node_modules/*' | head -5

# Verify __tests__ is excluded from build output
grep -r "__tests__" .gitignore tsconfig.json webpack.config.js 2>/dev/null || echo "(verify exclusion in build config)"
```

**Accept when:**
- All testable source files have corresponding test files in adjacent `__tests__` directories
- Test files consistently use `.spec.tsx` or `.spec.ts` naming convention
- Build configuration explicitly excludes `__tests__` directories from production output
- Test discovery works with Jest's default patterns without additional configuration
- Tests are co-located with their source code across all packages in the monorepo

<enforcement>
Claude Code MUST NOT skip or defer verification. When creating or modifying TypeScript/React files, verify that corresponding test files exist in the adjacent `__tests__` directory with proper naming conventions.
</enforcement>