The codebase needed a consistent approach to organizing and structuring test files for components and library functions. As the project grew with multiple packages (core package with components and lib directories), there was a need to establish a clear testing strategy that would:
1. Make tests discoverable and maintainable alongside the code they test
2. Support TypeScript/TSX test files for React component testing
3. Provide clear separation between test code and production code
4. Enable test framework tooling to easily identify and run test suites
5. Scale across a monorepo structure with multiple packages

The pattern emerged across 3 files in the core package, specifically testing component resolution logic, the main Puck component, and migration utilities, indicating a systematic approach to testing infrastructure.

## Policies
- Adopt a co-located __tests__ directory pattern with .spec.tsx naming convention for organizing test files. Test files are placed in __tests__ directories adjacent to the code they test, using descriptive names that mirror the tested modules with a .spec.tsx extension. This pattern is applied consistently across:
- Component testing (e.g., components/Puck/__tests__/index.tsx)
- Library function testing (e.g., lib/__tests__/resolve-component-data.spec.tsx, lib/__tests__/migrate.spec.tsx)

The .spec.tsx extension indicates TypeScript/TSX test files, supporting React component testing with JSX syntax. The __tests__ directory convention is widely recognized by testing frameworks and build tools for automatic test discovery.

## Instructions
- Positive: Tests are co-located with the code they test, making it easy to find and maintain related test files
- Positive: The __tests__ directory pattern is automatically recognized by popular testing frameworks (Jest, Vitest) without additional configuration
- Positive: Clear separation between production code and test code through dedicated __tests__ directories
- Positive: The .spec.tsx extension clearly identifies test files and supports TypeScript with JSX for component testing
- Positive: Scales well in monorepo structures with multiple packages, as each package can maintain its own test organization
- Positive: Enables easy exclusion of test files from production builds through standard glob patterns
- Negative: Creates additional directory nesting which can make file paths longer
- Negative: Requires discipline to maintain consistency - developers must remember to place tests in __tests__ directories
- Negative: May lead to duplication if both __tests__ directories and .test.tsx files coexist without clear guidelines