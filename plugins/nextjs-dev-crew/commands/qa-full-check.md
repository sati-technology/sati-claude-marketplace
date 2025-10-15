# Run Full QA Check with Parallel Agents

Executes comprehensive quality assurance using Testing, Code Review, and Security agents in parallel.

## Usage

```
/qa-full-check [scope]
```

## Examples

```bash
/qa-full-check              # Check entire codebase
/qa-full-check src/app/api  # Check API routes only
/qa-full-check components   # Check components only
```

## What It Does

Runs three QA agents simultaneously for maximum speed:

### 1. Testing Agent (Parallel)
- Runs all unit tests
- Runs integration tests
- Runs E2E tests
- Generates coverage report

### 2. Code Review Agent (Parallel)
- Reviews TypeScript quality
- Checks Next.js best practices
- Identifies performance issues
- Suggests refactoring

### 3. Security Agent (Parallel)
- Scans dependencies for vulnerabilities
- Checks for security issues
- Reviews authentication logic
- Validates environment variables

## Execution Flow

```
Start QA Check
│
├─► Testing Agent ──────────► Test Report
├─► Code Review Agent ──────► Quality Report
└─► Security Agent ─────────► Security Report
│
Wait for all three to complete
│
Generate Combined QA Report
```

## Quality Gates

All three checks must pass:

- ✅ **Tests:** All tests passing, coverage > 80%
- ✅ **Code Quality:** No critical issues
- ✅ **Security:** No critical vulnerabilities

## Example Output

```
╭─ QA Check Complete ────────────────────────────╮
│                                                 │
│ ✅ Testing: PASSED                              │
│    - 156 tests passed                          │
│    - Coverage: 87%                             │
│    - 0 failures                                │
│                                                 │
│ ✅ Code Review: PASSED                          │
│    - 3 minor issues found                      │
│    - 0 critical issues                         │
│    - 12 suggestions                            │
│                                                 │
│ ⚠️  Security: WARNING                           │
│    - 2 moderate vulnerabilities                │
│    - 0 critical vulnerabilities                │
│    - Update recommended: next@14.1.0           │
│                                                 │
│ Overall: PASSED WITH WARNINGS                  │
│                                                 │
╰─────────────────────────────────────────────────╯
```

## Time Savings

**Sequential:** ~30 minutes
- Testing: 10 min
- Code Review: 15 min
- Security: 5 min

**Parallel:** ~15 minutes (fastest agent wins!)

## Related Commands

- `/dev-full-feature` - Full development + QA workflow
- `/qa-tests-only` - Run testing agent only
- `/qa-review-only` - Run code review only
- `/qa-security-only` - Run security scan only
