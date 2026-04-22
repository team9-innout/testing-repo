The codebase needed a consistent approach to organizing unit tests for TypeScript/React components and utilities. As the project grew with multiple packages (core library with components, reducers, and utilities), maintaining test discoverability and ensuring tests remain close to implementation code became critical. The pattern emerged across 4 files in the core package, specifically for testing components (Puck), library utilities (resolve-component-data, migrate), and reducer helpers, indicating a systematic approach to test organization.

## Policies
- Adopt the __tests__ directory convention for co-locating unit tests with source code. Test files are placed in __tests__ subdirectories adjacent to the code they test, using the .spec.tsx extension for React component tests and TypeScript files. This pattern is consistently applied across different architectural layers: UI components (Puck), library utilities (resolve-component-data, migrate), and internal helpers (reducer actions). The convention follows Jest's default test discovery patterns and React Testing Library practices for component testing.

## Instructions
- Improved test discoverability - developers can immediately locate tests related to specific modules without navigating separate directory structures
- Enhanced maintainability - when refactoring or moving code, associated tests are clearly identified and can be moved together
- Reduced cognitive overhead - the __tests__ convention is widely recognized in the JavaScript/TypeScript ecosystem and aligns with Jest defaults
- Better package organization - each package maintains its own test structure, supporting monorepo architecture with independent packages
- Clear separation between test and production code - the __tests__ directory provides visual distinction while maintaining proximity
- Potential for slightly deeper directory nesting compared to flat test structures
- May require additional configuration for build tools to exclude __tests__ directories from production bundles
- Test files are distributed throughout the codebase rather than centralized, which some teams may find less organized