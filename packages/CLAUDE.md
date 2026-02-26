## ADR 1: Adopt Custom React Hooks for Encapsulating Reusable Component Logic

Context: Establishing custom React hooks as first-class architectural primitives for building the component library.

Policies:
1. Systematically extract reusable component logic into custom React hooks following the 'use-*' naming convention. Each hook encapsulates a specific concern (e.g., use-local-value, use-is-focused, use-parent, use-inject-css, use-preview-mode-hotkeys, use-reset-auto-zoom, use-on-drag-finished, use-deep-field, use-loaded-overrides) and provides a clean, composable API. These hooks are organized within the lib/ directory structure and component-specific lib/ subdirectories, establishing them as first-class architectural primitives for building the component library.