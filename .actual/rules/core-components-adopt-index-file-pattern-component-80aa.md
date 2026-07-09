# Adopt Index File Pattern for Component Module Exports in UI Framework

These rules are ALWAYS ACTIVE for all component module files in the UI framework, particularly those in the Puck component system including Canvas, Layout, ViewportControls, and other complex components.

### Rules

- **R-COMP-001** MUST: Implement an index.tsx file as the single entry point for each component directory.
- **R-COMP-002** MUST: Re-export the public API from the index file while hiding internal implementation details.
- **R-COMP-003** MUST: Ensure all component imports use the clean path pattern (e.g., 'components/Canvas') rather than direct file paths (e.g., 'components/Canvas/Canvas.tsx').
- **R-COMP-004** SHOULD: Apply the index file pattern consistently across all core components in the Puck component system.
- **R-COMP-005** SHOULD: Avoid circular dependency issues by carefully managing what is exported from index files.
- **R-COMP-006** MAY: Document the public API boundary in comments within the index file to clarify what is intentionally exported versus internal.

### Verify

```bash
# Verify all component directories have an index.tsx file
find src/components -type d -mindepth 1 | while read dir; do
  if [ ! -f "$dir/index.tsx" ]; then
    echo "Missing index.tsx in $dir"
    exit 1
  fi
done

# Verify no direct imports from component implementation files exist
grep -r "from.*components/[^/]*/[^/]*\.tsx" src --include="*.tsx" --include="*.ts" && exit 1 || true

# Verify index files re-export public API
grep -l "export" src/components/*/index.tsx > /dev/null || exit 1
```

**Accept when:**
- Every component directory contains an index.tsx file
- All component imports use the barrel export pattern (clean paths)
- Index files explicitly re-export the public API
- No circular dependencies are introduced by index file exports
- Internal implementation files are not directly imported from outside their component directory

<enforcement>
Claude Code MUST NOT skip or defer verification. All component modules must conform to the index file pattern before code is considered complete.
</enforcement>