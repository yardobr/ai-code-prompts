# Testing Strategy

For every new feature or code change, propose and implement comprehensive test coverage before marking work complete.

## Test Coverage Requirements

### Unit Tests
- Test individual functions and methods in isolation
- Cover all code paths including happy path and error conditions
- Mock external dependencies (databases, APIs, file systems)
- Verify edge cases (empty inputs, null values, boundary conditions)

### Integration Tests
- Test interactions between components/modules
- Verify database operations work correctly (if applicable)
- Test API endpoints with various inputs and auth states (if applicable)
- Ensure proper integration with third-party services (if applicable)

### Edge Cases and Error Scenarios
- Test with invalid, malformed, or unexpected inputs
- Verify graceful handling of network failures and timeouts
- Test concurrent access and race conditions where applicable
- Confirm proper behavior when resources are unavailable

## Test Quality Standards

- Tests should be deterministic and not rely on timing or external state
- Use descriptive test names that explain what is being tested
- Keep tests focused - one assertion per logical concept
- Ensure tests are maintainable and easy to understand
- Add tests for bug fixes to prevent regression

## Implementation Approach

When implementing a feature:
1. Propose test cases upfront covering the requirements above
2. Write tests alongside the implementation
3. Run tests and verify they pass before marking work complete
4. Document any test setup requirements or dependencies

Always include testing as part of the implementation, not as an afterthought.
