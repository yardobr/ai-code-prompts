# Backwards Compatibility

When making changes to existing code, APIs, or interfaces, always consider backwards compatibility to prevent breaking existing functionality and user workflows.

## Compatibility Assessment

Before implementing changes, evaluate the impact:

### Breaking vs Non-Breaking Changes

**Breaking changes** include:
- Removing or renaming public APIs, functions, or methods
- Changing function signatures (parameters, return types)
- Modifying data structures that are persisted or transmitted
- Changing URL routes or API endpoints
- Altering database schema in incompatible ways
- Removing or renaming configuration options
- Changing CLI command arguments or flags

**Non-breaking changes** include:
- Adding new optional parameters with defaults
- Adding new endpoints or methods
- Extending data structures with optional fields
- Adding new functionality that doesn't affect existing behavior
- Internal refactoring that maintains the same interface

## Guidelines for Changes

### When Making Breaking Changes

If a breaking change is necessary:
1. **Justify**: Clearly explain why the breaking change is required
2. **Deprecate First**: Mark old functionality as deprecated before removing
3. **Provide Migration Path**: Create clear upgrade instructions and examples
4. **Version Appropriately**: Follow semantic versioning (major version bump)
5. **Document**: Clearly note breaking changes in changelog and release notes
6. **Support Period**: Maintain deprecated functionality for reasonable timeframe

### When Maintaining Compatibility

Prefer these approaches:
- Add new parameters as optional with sensible defaults
- Create new methods/endpoints instead of modifying existing ones
- Use feature flags to gradually roll out changes
- Provide adapters or shims for legacy interfaces
- Maintain multiple API versions when necessary

## Migration Strategy

When breaking changes are unavoidable, provide:

1. **Migration Guide**: Step-by-step instructions for upgrading
2. **Code Examples**: Before/after code samples showing the changes
3. **Automated Tools**: Scripts or commands to help with migration when possible
4. **Timeline**: Clear deprecation schedule and support window
5. **Compatibility Layer**: Temporary bridge between old and new versions if feasible

## Database Schema Changes

For database changes:
- Use migrations that work with existing data
- Add new columns as nullable or with defaults
- Create new tables instead of restructuring existing ones when possible
- Provide data migration scripts for structural changes

## Documentation Requirements

When introducing breaking changes:
- Update CHANGELOG with `BREAKING CHANGE:` section
- Update all relevant documentation
- Add migration guide to docs
- Clearly mark deprecated features with removal timeline
- Update version numbers following semantic versioning

Always prioritize backwards compatibility unless there's a compelling reason for a breaking change.
