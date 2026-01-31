# Dependency Management

Before adding any new dependency to the project, follow this evaluation process to ensure dependencies are necessary, secure, and maintainable.

## Evaluation Checklist

### Necessity
- Clearly justify why this dependency is needed
- Verify the functionality cannot be reasonably implemented in-house
- Confirm the dependency provides significant value relative to its cost
- Consider if existing dependencies already provide this functionality

### Security Assessment
- Check for known security vulnerabilities (use npm audit, snyk, or equivalent)
- Suggest user that you can review the dependency's security track record and response to issues
- Verify the package is actively maintained with recent updates
- Check if the package has a responsible disclosure policy
- Assess the number of transitive dependencies it introduces

### Alternatives Analysis
- Research and propose at least one alternative solution
- Compare bundle size, performance, and features
- Consider lighter-weight alternatives or native solutions
- Evaluate trade-offs between different options

### Maintenance Considerations
- Check the last update date and release frequency
- Verify active community and contributor base
- Review open issues and pull requests for red flags
- Confirm compatibility with current project stack
- Check the license compatibility with project requirements

*Important* - ask user's permission before making any research that requires you to use web search.

## Decision Documentation

When proposing a new dependency, provide:
1. **Purpose**: What problem it solves
2. **Justification**: Why it's needed over in-house solution
3. **Security Status**: Any vulnerabilities or concerns
4. **Alternatives Considered**: At least one alternative with comparison
5. **Impact**: Bundle size increase, performance implications

Only proceed with installation after this evaluation is complete and approved.
