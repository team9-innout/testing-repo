---

## Architecture Decision Records

<adr_governance source="docs/adr/">
ADRs govern validated architectural standards for this project.
Full ADR documents: @docs/adr/
</adr_governance>

<activation>
These directives are ALWAYS ACTIVE. Claude Code MUST apply all rules in this
document to every code generation, modification, and review action within this
project. No exceptions unless explicitly noted per-rule.
</activation>

---

### Verification Protocol

<verification_protocol>
All rules in this document follow the **Verify → Fix → Repeat** loop.
</verification_protocol>

After generating or modifying code for any rule, Claude Code MUST:

1. **RUN** the targeted verification command(s) in the rule's **Verify** block.
2. **CAPTURE** the full command output (stdout + stderr).
3. **EVALUATE** whether the **Accept when** criteria are satisfied.
4. **IF FAILING:** diagnose the root cause, apply a fix, and re-run from step 1.
5. **IF PASSING:** include the passing output as inline evidence before proposing further changes.
6. **MAX ITERATIONS:** 5 attempts per rule. If still failing after 5 attempts, STOP and report the failure with all captured outputs.

<enforcement>
Compliance is not optional. Claude Code must not skip verification steps, assume
correctness, or defer verification to a later task. Evidence of a passing
verification run must accompany every code change that touches a governed area.
</enforcement>

---

## ADR 1: Adopt Custom React Hooks for Encapsulating Reusable Component Logic

Context: Establishing custom React hooks as first-class architectural primitives for building the component library.

Policies:
1. Systematically extract reusable component logic into custom React hooks following the 'use-*' naming convention. Each hook encapsulates a specific concern (e.g., use-local-value, use-is-focused, use-parent, use-inject-css, use-preview-mode-hotkeys, use-reset-auto-zoom, use-on-drag-finished, use-deep-field, use-loaded-overrides) and provides a clean, composable API. These hooks are organized within the lib/ directory structure and component-specific lib/ subdirectories, establishing them as first-class architectural primitives for building the component library.

---

## ADR 2: Adopt Dedicated Test Files for Redux Reducer Actions with Consistent Naming Convention

Policies:
1. Implement individual test files for each reducer action using the `.spec.ts` naming convention within a dedicated `__tests__` directory. Each action (duplicate, move, set-ui, replace, insert) has its own corresponding test file (e.g., `duplicate.spec.ts`, `move.spec.ts`) co-located with the action implementations in `packages/core/reducer/actions/__tests__/`. This establishes a 1:1 mapping between action modules and their test suites, using a consistent file naming pattern that clearly identifies test files.

---

## ADR 3: Adopt Message Queue Boundaries for Component Communication in React UI Framework

Policies:
1. Implement message queue boundaries as the primary inter-component communication pattern for event-driven interactions in the UI framework. This architectural decision establishes a publish-subscribe or event bus pattern that allows components to emit and consume messages without direct dependencies. Components like ExternalInput, drag-and-drop handlers, and Fields use message queues to broadcast state changes, user interactions, and lifecycle events, enabling loose coupling while maintaining predictable data flow.

---

## ADR 4: Adopt Mocking Strategy for State Management Store Testing in CI/CD Pipeline

Policies:
1. Implement a comprehensive mocking strategy for testing Redux/state management store slices. This involves mocking external dependencies, API calls, and inter-slice dependencies to enable isolated unit testing of state management logic. The mocking approach is consistently applied across all store slice tests (nodes, fields, history, permissions), creating a standardized testing pattern that integrates seamlessly with the CI/CD pipeline.

---

## ADR 5: Adopt Co-located Test Files with __tests__ Directory Pattern for Component and Library Testing

Policies:
1. Adopt a co-located __tests__ directory pattern with .spec.tsx naming convention for organizing test files. Test files are placed in __tests__ directories adjacent to the code they test, using descriptive names that mirror the tested modules with a .spec.tsx extension. This pattern is applied consistently across:
- Component testing (e.g., components/Puck/__tests__/index.tsx)
- Library function testing (e.g., lib/__tests__/resolve-component-data.spec.tsx, lib/__tests__/migrate.spec.tsx)

The .spec.tsx extension indicates TypeScript/TSX test files, supporting React component testing with JSX syntax. The __tests__ directory convention is widely recognized by testing frameworks and build tools for automatic test discovery.

---

## ADR 6: Adopt Index File Pattern for Component Module Exports in UI Framework

Policies:
1. Implement the index file (barrel export) pattern for all component modules in the UI framework. Each component directory contains an index.tsx file that serves as the single entry point for that component, re-exporting the public API while hiding internal implementation details. This pattern is consistently applied across core components including Canvas, Layout, and ViewportControls within the Puck component system.

---

## ADR 7: Adopt Co-located Test Files with __tests__ Directory Convention

Policies:
1. Adopt the __tests__ directory convention for co-locating unit tests with source code. Test files are placed in __tests__ subdirectories adjacent to the code they test, using the .spec.tsx extension for React component tests and TypeScript files. This pattern is consistently applied across different architectural layers: UI components (Puck), library utilities (resolve-component-data, migrate), and internal helpers (reducer actions). The convention follows Jest's default test discovery patterns and React Testing Library practices for component testing.

---

## ADR 8: Adopt Snapshot Testing for Core Data Transformation and State Management Logic

Policies:
1. Implement snapshot testing for core data transformation functions and reducer actions. Test files are organized in __tests__ directories co-located with the source code (packages/core/reducer/actions/__tests__/, packages/core/lib/data/__tests__/). Snapshot tests capture the complete output of operations like tree walking, state transformations, and reducer actions, storing them as serialized snapshots that are version-controlled alongside the code. This approach is specifically applied to the testing.snapshot facet within the CI/CD pipeline to ensure output consistency across builds.

---

## ADR 9: Adopt Centralized Test Helper and Mocking Infrastructure for Component Testing

Policies:
1. Implement a centralized test helper and mocking infrastructure using dedicated __helpers__ and __tests__ directories with shared utilities. This includes: (1) Creating reusable test helpers in __helpers__/index.tsx for common test setup and teardown operations, (2) Standardizing mock implementations for component data resolution, (3) Establishing consistent patterns for testing React components with TypeScript (.spec.tsx convention), and (4) Providing shared fixtures and utilities that can be imported across test suites to ensure consistency in testing approach.