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

## ADR 4: Adopt Environment-Based Configuration for External API Integration in Client-Side Applications

Policies:
1. Implement environment-based configuration management using environment variables for all external API integrations in public-facing applications. This approach centralizes API configuration in application layout and theme configuration files, using runtime environment variable injection to manage secrets. The pattern ensures that API keys and sensitive configuration are never hardcoded in source code, are environment-specific, and are properly scoped to server-side or build-time contexts where appropriate. Configuration is initialized at the application root level (document/layout components) to ensure consistent availability throughout the component tree.

---

## ADR 5: Adopt Centralized Configuration Management for Public-Facing Application Entry Points

Policies:
1. Implement centralized runtime configuration management at application entry points using framework-specific configuration files. Each public-facing application establishes its configuration sources at the root level through dedicated configuration files that serve as the single source of truth for runtime settings, theming, and layout specifications. This approach leverages framework conventions (_document.tsx, layout.tsx, theme.config.tsx) to provide consistent configuration initialization across different application types within the monorepo.