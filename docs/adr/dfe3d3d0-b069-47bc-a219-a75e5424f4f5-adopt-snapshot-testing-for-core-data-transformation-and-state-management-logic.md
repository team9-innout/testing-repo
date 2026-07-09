The codebase contains complex data transformation logic (walk-tree, walk-app-state) and state management operations (reducer actions like remove) that produce structured outputs. These operations involve nested data structures, tree traversals, and state mutations that are difficult to verify with granular assertions. The team needed a testing approach that could comprehensively validate the entire output structure while remaining maintainable as the codebase evolves. Traditional assertion-based testing would require numerous individual assertions for each property and nested element, making tests brittle and verbose.

## Policies
- Implement snapshot testing for core data transformation functions and reducer actions. Test files are organized in __tests__ directories co-located with the source code (packages/core/reducer/actions/__tests__/, packages/core/lib/data/__tests__/). Snapshot tests capture the complete output of operations like tree walking, state transformations, and reducer actions, storing them as serialized snapshots that are version-controlled alongside the code. This approach is specifically applied to the testing.snapshot facet within the CI/CD pipeline to ensure output consistency across builds.

## Instructions
- Comprehensive test coverage: Entire output structures are validated in a single test, catching unexpected changes in any part of the data structure
- Improved developer experience: Tests are easier to write and maintain compared to verbose assertion chains for complex nested objects
- Clear change detection: Snapshot diffs provide immediate visibility into how code changes affect outputs, making code reviews more effective
- Regression prevention: Any unintended changes to output structure are immediately caught by snapshot mismatches in CI/CD pipeline
- Reduced test maintenance: When intentional changes occur, snapshots can be updated in bulk rather than modifying multiple assertions
- Trade-off - Less explicit: Snapshots are less self-documenting than explicit assertions, requiring developers to review snapshot files to understand expected behavior
- Trade-off - Potential for lazy updates: Developers might blindly update snapshots without carefully reviewing changes, potentially masking bugs
- Trade-off - Merge conflicts: Snapshot files can create merge conflicts when multiple developers modify the same tested functionality
- Trade-off - Storage overhead: Snapshot files add to repository size, especially for large or numerous outputs