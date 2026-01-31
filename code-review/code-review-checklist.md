# Code Review Checklist

When I ask you to do a code review always follow the rules below to verify the implementation fits the our standards.

## Security
- Check for common vulnerabilities (SQL injection, XSS, CSRF, etc.)
- Validate all user inputs and sanitize outputs
- Review authentication and authorization logic
- Verify that functionality follows the roles/permissions system if applicable
- Ensure sensitive data is properly encrypted and not exposed in logs

## Performance
- Identify potential bottlenecks (N+1 queries, inefficient algorithms)
- Check for unnecessary computations or redundant operations
- Verify proper resource cleanup (connections, file handles, memory)
- Consider caching opportunities where appropriate

## Maintainability
- Ensure code follows project conventions and style guidelines
- Check naming of folders, files, and code units - they should follow guidelines and be self-descriptive
- Check for code duplication and extract reusable components
- Verify meaningful variable/function names and clear logic flow
- Confirm proper separation of concerns

## Best Practices
- Validate error handling and edge cases are covered
- Check for proper logging at appropriate levels
- Ensure code is testable and doesn't introduce tight coupling
- Verify that changes don't violate SOLID principles

## Functionality
- Explain what the reviewed code does from a product standpoint
- Describe the user-facing behavior or business value it provides
- Confirm the implementation matches the intended requirements

After completing the review, explicitly state what you checked and any concerns or improvements identified. Only mark work complete after this review is done.
