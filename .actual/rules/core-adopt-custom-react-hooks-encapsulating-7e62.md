# Adopt Custom React Hooks for Encapsulating Reusable UI Logic in Core Library

These rules are ALWAYS ACTIVE for all React components and utility modules in the core library that manage UI state, side effects, or component behaviors.

### Rules

- **R-HOOKS-001** MUST: Implement custom React hooks as the primary pattern for encapsulating and sharing reusable UI logic throughout the core library.
- **R-HOOKS-002** MUST: Name all custom hooks following the `use-*` convention (e.g., `use-local-value`, `use-is-focused`, `use-deep-field`).
- **R-HOOKS-003** MUST: Isolate each hook in its own module within the `lib` directory or component-specific `lib` subdirectories.
- **R-HOOKS-004** MUST: Apply the single-responsibility principle to each hook, ensuring it encapsulates one specific concern (state management, side effects, context consumption, or behavioral logic).
- **R-HOOKS-005** SHOULD: Expose clean, minimal interfaces from hooks to consuming components, avoiding unnecessary complexity or over-abstraction.
- **R-HOOKS-006** SHOULD: Test hooks independently from component rendering using React Testing Library's `renderHook` or equivalent utilities.
- **R-HOOKS-007** MAY: Compose multiple hooks together to build complex behaviors, provided each hook maintains its single responsibility.

### Verify

```bash
# Check for custom hooks following use-* naming convention
find src -name 'use-*.ts' -o -name 'use-*.tsx' | wc -l

# Verify hooks are isolated in lib directories
find src -path '*/lib/use-*.ts' -o -path '*/lib/use-*.tsx' | head -20

# Check for hook test files
find src -name '*.test.ts' -o -name '*.test.tsx' | xargs grep -l 'renderHook' | wc -l

# Verify no direct state management in presentational components
grep -r 'useState\|useReducer\|useEffect' src/components --include='*.tsx' | grep -v 'lib/' | wc -l
```

**Accept when:**
- All reusable UI logic is encapsulated in custom hooks following the `use-*` naming convention
- Each hook is isolated in its own module within a `lib` directory
- Hooks are tested independently and pass all test suites
- Presentational components delegate stateful logic to custom hooks
- New features follow the established hook pattern for consistency

<enforcement>
Claude Code MUST NOT skip or defer verification. All custom hooks must adhere to naming conventions, isolation requirements, and single-responsibility principle before code is considered compliant.
</enforcement>