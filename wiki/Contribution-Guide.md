# Contribution Guide

Thank you for considering contributing to Commutr! This guide will help you get started.

## Ways to Contribute

You don't need to write code to contribute:

- **Report Bugs**: Found something broken? Let us know
- **Suggest Features**: Have ideas for improvements? Share them
- **Improve Documentation**: Fix typos, clarify explanations, add examples
- **Write Tests**: Help us achieve better test coverage
- **Review Pull Requests**: Provide feedback on others' contributions
- **Answer Questions**: Help other users in Discussions
- **Spread the Word**: Tell others about Commutr

## Before You Start

### Read the Documentation

Familiarize yourself with:
- [Project Vision & Goals](Project-Vision-&-Goals) - Understand our philosophy
- [System Architecture](System-Architecture) - Learn how components work
- [Repository Structure](Repository-Structure) - Know where things are

### Check Existing Work

Before starting:
1. Search [existing issues](https://github.com/YOUR_USERNAME/commutr/issues) to avoid duplicates
2. Check [open pull requests](https://github.com/YOUR_USERNAME/commutr/pulls) for ongoing work
3. Read [discussions](https://github.com/YOUR_USERNAME/commutr/discussions) for context

### Set Up Your Environment

Follow the [Setup & Installation](Setup-&-Installation) guide to get Commutr running locally.

## Reporting Bugs

### Before Reporting

1. **Update to latest version**: Bug might already be fixed
2. **Check existing issues**: Someone may have reported it
3. **Reproduce consistently**: Ensure it's not a one-time glitch

### Creating a Bug Report

Use the bug report template and include:

**Required Information**:
- **Description**: Clear summary of the bug
- **Steps to Reproduce**: Exact steps to trigger the bug
- **Expected Behavior**: What should happen
- **Actual Behavior**: What actually happens
- **Environment**: OS, browser, Node.js version

**Example**:
```markdown
## Description
Route calculation fails when source and destination are the same

## Steps to Reproduce
1. Open Commutr
2. Enter "123 Main St" as both source and destination
3. Click "Find Routes"

## Expected Behavior
Error message: "Source and destination must be different"

## Actual Behavior
Server returns 500 error, no user-friendly message

## Environment
- OS: macOS 13.0
- Browser: Chrome 120
- Node.js: 18.17.0
```

**Helpful Additions**:
- Screenshots or screen recordings
- Browser console errors
- Server logs
- Network request/response data

## Suggesting Features

### Before Suggesting

1. **Check roadmap**: Feature might already be planned
2. **Search discussions**: Idea might have been discussed
3. **Consider scope**: Does it align with project vision?

### Creating a Feature Request

Use the feature request template and include:

**Required Information**:
- **Problem**: What problem does this solve?
- **Proposed Solution**: How should it work?
- **Alternatives**: Other ways to solve the problem
- **Use Cases**: Real-world scenarios where this helps

**Example**:
```markdown
## Problem
Users can't compare multiple routes side-by-side

## Proposed Solution
Add "Compare Routes" button that shows routes in a table:
- Columns: Route, Cost, Time, Accessibility
- Sortable by any column
- Highlight differences

## Alternatives
- Show routes in tabs instead of table
- Add filters to hide/show routes

## Use Cases
- User wants cheapest route but also wants to see fastest
- User comparing accessibility features across routes
- User deciding if extra cost is worth time savings
```

## Contributing Code

### Fork and Clone

```bash
# Fork the repository on GitHub, then:
git clone https://github.com/YOUR_USERNAME/commutr.git
cd commutr
git remote add upstream https://github.com/ORIGINAL_OWNER/commutr.git
```

### Branching Strategy

Create a branch for your work:

```bash
# Feature branch
git checkout -b feature/add-route-comparison

# Bug fix branch
git checkout -b fix/same-location-error

# Documentation branch
git checkout -b docs/improve-setup-guide
```

**Branch naming**:
- `feature/` - New features
- `fix/` - Bug fixes
- `docs/` - Documentation changes
- `test/` - Test additions/improvements
- `refactor/` - Code refactoring

### Making Changes

#### Code Style

We use ESLint and Prettier for consistent code style:

```bash
# Check style
npm run lint

# Auto-fix issues
npm run lint:fix

# Format code
npm run format
```

**Key conventions**:
- Use TypeScript for all new code
- Prefer `const` over `let`, avoid `var`
- Use descriptive variable names
- Add JSDoc comments for public functions
- Keep functions small and focused

**Example**:
```typescript
/**
 * Calculates the total fare for a route including all segments.
 * 
 * @param route - The route to calculate fare for
 * @returns Fare breakdown with total cost
 */
export function calculateRouteFare(route: Route): FareBreakdown {
  const segments = route.segments.map(calculateSegmentFare);
  const totalFare = segments.reduce((sum, seg) => sum + seg.totalSegmentFare, 0);
  
  return {
    segments,
    totalFare,
    currency: 'USD'
  };
}
```

#### Writing Tests

All new features and bug fixes must include tests:

**Unit Tests**:
```typescript
// tests/unit/services/fare-calculator.test.ts
describe('FareCalculator', () => {
  describe('calculateRouteFare', () => {
    it('should calculate total fare for single segment', () => {
      const route = createMockRoute({ segments: [mockSegment] });
      const result = calculateRouteFare(route);
      expect(result.totalFare).toBe(2.50);
    });
    
    it('should include transfer fees', () => {
      const route = createMockRoute({ segments: [mockSegment1, mockSegment2] });
      const result = calculateRouteFare(route);
      expect(result.totalFare).toBe(5.50); // 2.50 + 2.50 + 0.50 transfer
    });
  });
});
```

**Property-Based Tests**:
```typescript
// tests/property/fare-calculation.property.test.ts
import fc from 'fast-check';

describe('FareCalculator Properties', () => {
  it('total fare should equal sum of segment fares', () => {
    fc.assert(
      fc.property(
        fc.array(arbitrarySegment(), { minLength: 1, maxLength: 10 }),
        (segments) => {
          const route = { segments, /* ... */ };
          const breakdown = calculateRouteFare(route);
          const manualSum = segments.reduce((sum, seg) => 
            sum + calculateSegmentFare(seg).totalSegmentFare, 0
          );
          expect(breakdown.totalFare).toBeCloseTo(manualSum, 2);
        }
      )
    );
  });
});
```

**Test Coverage**:
- Aim for 80%+ coverage
- Test happy paths and error cases
- Test edge cases (empty inputs, boundary values)
- Test integration between components

#### Commit Messages

Follow conventional commits format:

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types**:
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `test`: Test additions/changes
- `refactor`: Code refactoring
- `style`: Code style changes (formatting)
- `chore`: Build process, dependencies

**Examples**:
```
feat(route-planner): add route comparison feature

Adds ability to compare multiple routes side-by-side in a table.
Users can sort by cost, time, or accessibility score.

Closes #123
```

```
fix(fare-calculator): handle same source and destination

Returns validation error instead of 500 when source equals destination.

Fixes #456
```

```
docs(setup): clarify PostgreSQL installation steps

Adds specific commands for Ubuntu, macOS, and Windows.
Includes troubleshooting for common PostGIS issues.
```

### Submitting a Pull Request

#### Before Submitting

1. **Update from upstream**:
   ```bash
   git fetch upstream
   git rebase upstream/main
   ```

2. **Run all checks**:
   ```bash
   npm run lint
   npm test
   npm run type-check
   ```

3. **Update documentation** if needed

4. **Test manually** in your local environment

#### Creating the PR

1. Push your branch:
   ```bash
   git push origin feature/add-route-comparison
   ```

2. Open PR on GitHub

3. Fill out the PR template:
   - **Description**: What does this PR do?
   - **Motivation**: Why is this change needed?
   - **Testing**: How was this tested?
   - **Screenshots**: For UI changes
   - **Checklist**: Confirm all items completed

**Example PR Description**:
```markdown
## Description
Adds route comparison feature allowing users to view multiple routes side-by-side.

## Motivation
Users requested ability to compare routes before choosing. Currently they must
view routes one at a time, making comparison difficult.

Closes #123

## Changes
- Added ComparisonTable component
- Added "Compare Routes" button to route list
- Added sorting by cost, time, accessibility
- Updated route state management

## Testing
- Added unit tests for ComparisonTable
- Added integration test for comparison workflow
- Manually tested with 2-5 routes
- Tested sorting functionality
- Verified accessibility with screen reader

## Screenshots
[Include screenshots of the comparison table]

## Checklist
- [x] Tests added and passing
- [x] Documentation updated
- [x] Code follows style guide
- [x] No console errors
- [x] Accessible (keyboard navigation, screen reader)
```

#### Code Review Process

1. **Automated checks run**: Linting, tests, type checking
2. **Maintainer reviews code**: Usually within 2-3 days
3. **Address feedback**: Make requested changes
4. **Re-review**: Maintainer reviews again
5. **Merge**: PR merged when approved

**Responding to Feedback**:
- Be open to suggestions
- Ask questions if unclear
- Make requested changes promptly
- Push new commits (don't force-push during review)
- Thank reviewers for their time

## Code Review Guidelines

### For Contributors

When your PR is reviewed:
- **Don't take it personally**: Reviews improve code quality
- **Ask questions**: If feedback is unclear, ask for clarification
- **Explain decisions**: If you disagree, explain your reasoning
- **Be patient**: Maintainers are volunteers with limited time

### For Reviewers

When reviewing PRs:
- **Be kind and constructive**: Assume good intentions
- **Explain why**: Don't just say "change this", explain the reason
- **Suggest alternatives**: Offer specific improvements
- **Approve small improvements**: Don't block on minor style issues
- **Test the changes**: Pull the branch and test locally

## Documentation Contributions

### Improving Wiki Pages

1. Click "Edit" on any Wiki page
2. Make your changes in Markdown
3. Preview to ensure formatting is correct
4. Save with descriptive commit message

### Adding Code Comments

- Explain **why**, not **what**
- Document assumptions and edge cases
- Add JSDoc for public APIs
- Keep comments up-to-date with code

### Writing Guides

Good documentation:
- Starts with the problem being solved
- Provides step-by-step instructions
- Includes examples and code snippets
- Anticipates common questions
- Uses simple, clear language

## Community Guidelines

### Be Respectful

- Treat everyone with respect
- Welcome newcomers
- Be patient with questions
- Assume good intentions
- No harassment or discrimination

### Be Constructive

- Provide actionable feedback
- Suggest improvements, don't just criticize
- Acknowledge good work
- Help others learn

### Be Collaborative

- Share knowledge freely
- Credit others' contributions
- Work together to solve problems
- Celebrate successes as a team

## Recognition

Contributors are recognized in:
- **README.md**: Listed in Contributors section
- **Release Notes**: Mentioned for significant contributions
- **GitHub**: Contributor badge on profile

## Getting Help

Stuck? Need guidance?

- **GitHub Discussions**: Ask questions, discuss ideas
- **Issue Comments**: Ask for clarification on specific issues
- **Pull Request Comments**: Ask reviewers for help
- **Email**: Contact maintainers directly (if provided)

## First-Time Contributors

New to open source? Start here:

### Good First Issues

Look for issues labeled `good first issue`:
- Well-defined scope
- Clear acceptance criteria
- Guidance provided
- Mentorship available

### Beginner-Friendly Tasks

- Fix typos in documentation
- Improve error messages
- Add missing tests
- Update dependencies
- Improve code comments

### Learning Resources

- [How to Contribute to Open Source](https://opensource.guide/how-to-contribute/)
- [First Contributions](https://github.com/firstcontributions/first-contributions)
- [Git Handbook](https://guides.github.com/introduction/git-handbook/)

## Advanced Topics

### Property-Based Testing

We use fast-check for property-based tests. See [design document](.kiro/specs/commutr/design.md) for correctness properties.

### Database Migrations

```bash
# Create migration
npm run migrate:create -- --name add_column_to_routes

# Edit migration file in src/database/migrations/

# Run migration
npm run migrate

# Rollback if needed
npm run migrate:rollback
```

### Performance Optimization

Before optimizing:
1. Profile to find bottlenecks
2. Measure current performance
3. Make changes
4. Measure again to verify improvement

## Questions?

- Read the [FAQ](FAQ)
- Search [GitHub Discussions](https://github.com/YOUR_USERNAME/commutr/discussions)
- Open a new discussion if your question isn't answered

---

*Thank you for contributing to Commutr! Every contribution, no matter how small, makes a difference.*
