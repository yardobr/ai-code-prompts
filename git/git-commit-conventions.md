# Git Commit Conventions

Follow these guidelines when creating git commits to maintain a clean, understandable project history.

## Commit Message Structure

Use the Conventional Commits format:

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Type
Choose one of these commit types:
- **feat**: New feature for the user
- **fix**: Bug fix for the user
- **docs**: Documentation changes
- **style**: Code style changes (formatting, missing semi-colons, etc.)
- **refactor**: Code changes that neither fix bugs nor add features
- **perf**: Performance improvements
- **test**: Adding or updating tests
- **build**: Changes to build system or dependencies
- **ci**: Changes to CI configuration files and scripts
- **chore**: Other changes that don't modify src or test files

### Scope (Optional)
The scope specifies what part of the codebase is affected:
- Component name, module name, or feature area
- Examples: `(auth)`, `(api)`, `(ui)`, `(database)`

### Subject
- Use imperative mood ("add" not "added" or "adds")
- Don't capitalize first letter
- No period at the end
- Maximum 50 characters
- Be clear and descriptive

### Body (Optional but Recommended)
- Separate from subject with a blank line
- Explain the "what" and "why", not the "how"
- Wrap at 72 characters
- Use bullet points for multiple changes

### Footer (Optional)
- Reference issue numbers: `Closes #123` or `Fixes #456`
- Note breaking changes: `BREAKING CHANGE: description`

## Atomic Commits

- Each commit should represent one logical change
- Don't mix unrelated changes in a single commit
- Commit working code that doesn't break the build
- Make commits small enough to be easily reviewed and reverted if needed

## Examples

**Good:**
```
feat(auth): add password reset functionality

Implement password reset flow with email verification.
- Add reset token generation and validation
- Create email template for reset link
- Add expiration handling for tokens

Closes #234
```

**Good:**
```
fix(api): handle null response in user endpoint

Prevent crash when external service returns null
```

**Bad:**
```
Updated stuff
```

**Bad:**
```
feat: Added new feature, fixed bugs, updated docs, and refactored code
```

When creating commits, always follow this convention to maintain project history clarity.
