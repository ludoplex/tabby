```markdown
# tabby Development Patterns

> Auto-generated skill from repository analysis

## Overview
This skill provides an in-depth guide to the development patterns used in the `tabby` TypeScript codebase. It covers coding conventions, file organization, dependency management workflows, and testing patterns. Whether you're contributing new features or maintaining the repository, following these patterns will ensure consistency and reliability.

## Coding Conventions

### File Naming
- Use **camelCase** for file names.
  - Example: `myComponent.ts`, `userProfile.test.ts`

### Import Style
- Use **relative imports** for modules within the project.
  ```typescript
  import { myFunction } from './utils';
  ```

### Export Style
- Use **named exports** rather than default exports.
  ```typescript
  // utils.ts
  export function myFunction() { ... }

  // usage
  import { myFunction } from './utils';
  ```

### Commit Messages
- Follow **conventional commit** format.
- Common prefix: `chore`
  - Example: `chore: update dependencies across packages`

## Workflows

### Dependency Update Across Multiple Packages
**Trigger:** When dependencies need to be updated (e.g., via Dependabot or manually) across multiple packages or directories in the monorepo.
**Command:** `/update-dependencies`

1. **Identify outdated dependencies**  
   Scan all `package.json` files in the repository (including subdirectories) to find outdated npm/yarn dependencies.
2. **Update version numbers**  
   For each outdated dependency, update its version in every relevant `package.json`.
3. **Regenerate lockfiles**  
   For each affected directory, update or regenerate the corresponding `yarn.lock` file to reflect the new dependency versions.
4. **Commit changes**  
   Commit all modified `package.json` and `yarn.lock` files together, using a conventional commit message such as:
   ```
   chore: update dependencies across packages
   ```
5. **Push and review**  
   Push the changes and open a pull request if required.

**Example Directory Structure:**
```
packages/
  core/
    package.json
    yarn.lock
  ui/
    package.json
    yarn.lock
package.json
yarn.lock
```

**Example Command:**
```sh
/update-dependencies
```

## Testing Patterns

- Test files use the pattern: `*.test.*` (e.g., `userService.test.ts`)
- The specific testing framework is not detected, but tests are colocated with source files or in test directories.
- Example test file:
  ```typescript
  // userService.test.ts
  import { getUser } from './userService';

  describe('getUser', () => {
    it('should return user data', () => {
      // test implementation
    });
  });
  ```

## Commands

| Command              | Purpose                                                      |
|----------------------|--------------------------------------------------------------|
| /update-dependencies | Update npm/yarn dependencies across all packages and lockfiles|
```
