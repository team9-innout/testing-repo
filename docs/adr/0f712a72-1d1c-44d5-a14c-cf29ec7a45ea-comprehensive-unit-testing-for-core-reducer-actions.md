The core reducer package contains critical state management logic that handles various actions (duplicate, move, set-ui, replace, insert). These actions form the foundation of the application's state transitions and are used throughout the codebase. Without comprehensive testing, bugs in these core actions could propagate throughout the entire application, leading to unpredictable state management issues. The need for reliable, maintainable state management drove the decision to implement thorough unit testing for each reducer action.

## Policies
- Implement dedicated unit test files for each core reducer action in the packages/core/reducer/actions/__tests__/ directory. Each action (duplicate, move, set-ui, replace, insert) has its own isolated test specification file following the naming convention [action-name].spec.ts. This ensures that every state transformation operation has comprehensive test coverage with clear separation of concerns.

## Instructions
- Positive: High confidence in core state management logic with 91.70% test coverage significance
- Positive: Clear test organization makes it easy to locate and maintain tests for specific actions
- Positive: Isolated test files enable parallel test execution and faster CI/CD pipelines
- Positive: Reduces regression risk when modifying reducer logic
- Positive: Serves as living documentation for expected behavior of each action
- Positive: Facilitates onboarding of new developers by providing clear examples of action behavior
- Negative: Requires ongoing maintenance effort to keep tests synchronized with action implementations
- Negative: Increases initial development time as each action requires corresponding test coverage
- Negative: May lead to test duplication if integration tests also cover similar scenarios