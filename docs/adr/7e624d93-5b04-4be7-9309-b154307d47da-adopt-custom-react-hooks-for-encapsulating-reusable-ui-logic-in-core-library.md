The core package requires a scalable approach to manage complex UI state, side effects, and component behaviors across multiple features including AutoField components, drag-and-drop functionality, preview modes, and canvas rendering. Without a consistent pattern for encapsulating and reusing logic, the codebase would face duplication, tight coupling between components, and difficulty in testing and maintaining stateful behaviors. The team needed a standardized way to share logic across components while maintaining separation of concerns and testability.

## Policies
- Implement a custom React hooks architecture as the primary pattern for encapsulating and sharing reusable UI logic throughout the core library. This includes creating specialized hooks for specific concerns such as use-local-value, use-is-focused, use-deep-field, use-parent, use-loaded-overrides, use-preview-mode-hotkeys, use-inject-css, use-reset-auto-zoom, and use-on-drag-finished. Each hook is isolated in its own module within the lib directory or component-specific lib subdirectories, following a clear naming convention (use-*) and single-responsibility principle. The hooks encapsulate state management, side effects, context consumption, and complex behavioral logic, exposing clean interfaces to consuming components.

## Instructions
- Positive: Promotes code reusability across components, reducing duplication and maintenance burden
- Positive: Enables better separation of concerns by isolating stateful logic from presentational components
- Positive: Improves testability as hooks can be tested independently from component rendering
- Positive: Provides a consistent, predictable pattern that developers can follow when adding new features
- Positive: Facilitates composition of complex behaviors by combining multiple hooks
- Positive: Aligns with React best practices and modern React development patterns
- Negative: Increases the number of files and modules in the codebase, potentially adding navigation overhead
- Negative: Requires developers to understand React hooks lifecycle and rules of hooks
- Negative: May lead to over-abstraction if hooks are created prematurely before patterns are fully understood
- Negative: Can create indirect dependencies between components through shared hook implementations