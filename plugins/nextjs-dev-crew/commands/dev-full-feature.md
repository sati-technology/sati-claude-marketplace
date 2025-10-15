# Build Full Feature with Parallel Agent Crew

Orchestrates the complete development workflow using specialized agents working in parallel for maximum efficiency.

## Usage

```
/dev-full-feature [feature-description]
```

## Examples

```bash
/dev-full-feature user profile management with avatar upload

/dev-full-feature product catalog with search and filters

/dev-full-feature admin dashboard with analytics
```

## Workflow

This command orchestrates agents in three parallel stages:

### Stage 1: Development Crew (Parallel)

Three agents work simultaneously on different layers:

**1. Database Agent** (Foundation)
- Design Prisma schema
- Create migrations
- Build query functions
- Generate types

**2. Backend Agent** (Server Logic)
- Implement API routes
- Create server actions
- Add authentication
- Server-side validation

**3. Frontend Agent** (UI/UX)
- Build React components
- Create pages
- Client-side forms
- UI interactions

**Coordination:**
- All three agents start immediately
- Share TypeScript interfaces
- Database provides foundation (schema + types)
- Backend consumes database queries
- Frontend consumes backend APIs

### Stage 2: Quality Assurance Crew (Parallel)

After development completes, three QA agents run simultaneously:

**1. Testing Agent**
- Unit tests
- Component tests
- Integration tests
- E2E tests

**2. Code Review Agent**
- TypeScript quality
- Best practices
- Performance review
- Refactoring suggestions

**3. Security Agent**
- Dependency scanning
- Vulnerability check
- Auth review
- Security headers

**Coordination:**
- All three agents work independently
- No dependencies between them
- Each produces separate report

### Stage 3: Deployment Pipeline (Sequential)

After QA passes, deployment runs:

**1. Build Agent**
- Run production build
- Check for errors
- Optimize bundle

**2. Deployment Agent**
- Deploy to staging
- Run smoke tests
- Deploy to production

## Implementation

When you invoke this command, Claude Code will:

1. **Analyze the feature request**
   - Break down requirements
   - Identify database schema needs
   - Plan API endpoints
   - Design UI components

2. **Execute Stage 1 (Development) in Parallel**
   ```
   Invoke in parallel:
   - Database Agent: Design schema for [feature]
   - Backend Agent: Implement API for [feature]
   - Frontend Agent: Build UI for [feature]
   ```

3. **Wait for Stage 1 completion**
   - All three agents must complete
   - Verify integration points
   - Confirm types are shared

4. **Execute Stage 2 (QA) in Parallel**
   ```
   Invoke in parallel:
   - Testing Agent: Write tests for [feature]
   - Code Review Agent: Review code quality
   - Security Agent: Check for vulnerabilities
   ```

5. **Wait for Stage 2 completion**
   - Review all QA reports
   - Address critical issues
   - Confirm quality gates pass

6. **Execute Stage 3 (Deployment) Sequentially**
   ```
   Invoke sequentially:
   - Build Agent: Build production bundle
   - Deployment Agent: Deploy to staging → production
   ```

## Example Execution

**Request:**
```
/dev-full-feature user authentication with email/password and Google OAuth
```

**Stage 1: Development (Parallel)**

Database Agent creates:
```prisma
model User {
  id            String    @id @default(cuid())
  email         String    @unique
  emailVerified DateTime?
  password      String?
  name          String?
  image         String?
  accounts      Account[]
  sessions      Session[]
}

model Account {
  id                String  @id @default(cuid())
  userId            String
  type              String
  provider          String
  providerAccountId String
  // ... OAuth fields
  user              User    @relation(fields: [userId], references: [id])
}
```

Backend Agent creates:
```typescript
// app/api/auth/[...nextauth]/route.ts
// app/api/auth/register/route.ts
// app/actions/auth.ts
```

Frontend Agent creates:
```typescript
// components/auth/LoginForm.tsx
// components/auth/RegisterForm.tsx
// app/login/page.tsx
// app/register/page.tsx
```

**Stage 2: QA (Parallel)**

Testing Agent writes:
```typescript
// __tests__/api/auth.test.ts
// __tests__/components/LoginForm.test.tsx
// e2e/auth.spec.ts
```

Code Review Agent reviews:
```
- Check authentication security
- Review password hashing
- Verify OAuth implementation
- Check error handling
```

Security Agent scans:
```
- Check for auth vulnerabilities
- Review session management
- Check OAuth configuration
- Scan dependencies
```

**Stage 3: Deployment (Sequential)**

Build Agent:
```bash
npm run build
# Checks for build errors
# Optimizes bundle
```

Deployment Agent:
```bash
vercel deploy
# Deploy to staging
# Run smoke tests
vercel --prod
# Deploy to production
```

## Benefits of Parallel Execution

### Traditional Sequential (Slow)
```
Database (10 min) → Backend (15 min) → Frontend (20 min) → Testing (10 min) → Review (5 min) → Security (5 min)
Total: 65 minutes
```

### Parallel Execution (Fast)
```
Stage 1 (Parallel):
  Database, Backend, Frontend all run simultaneously
  Time: ~20 minutes (longest agent)

Stage 2 (Parallel):
  Testing, Review, Security all run simultaneously
  Time: ~10 minutes (longest agent)

Stage 3 (Sequential):
  Build → Deploy
  Time: ~5 minutes

Total: ~35 minutes (46% faster!)
```

## Configuration

### Agent Timeouts
Each agent has a maximum execution time:
- Development agents: 30 minutes
- QA agents: 15 minutes
- Deployment agents: 10 minutes

### Quality Gates
Stage 2 must pass before Stage 3:
- All tests pass (Testing Agent)
- No critical issues (Code Review Agent)
- No critical vulnerabilities (Security Agent)

### Rollback
If deployment fails:
- Automatic rollback to previous version
- Notify team of failure
- Generate incident report

## Tips for Best Results

1. **Be specific in feature description**
   - ✅ "User registration with email verification and profile setup"
   - ❌ "Add users"

2. **Include technical requirements**
   - "Use Prisma for database"
   - "Implement with NextAuth"
   - "Deploy to Vercel"

3. **Mention integration points**
   - "Integrate with existing product catalog"
   - "Use existing auth middleware"

4. **Specify quality requirements**
   - "Include E2E tests"
   - "Ensure 80%+ test coverage"
   - "Follow TypeScript strict mode"

## Troubleshooting

**Issue:** Agents waiting for each other
**Solution:** Check if you've properly separated concerns. Database should work independently, Backend can start immediately, Frontend can mock APIs.

**Issue:** Integration failures
**Solution:** Ensure shared TypeScript types are created early. Database generates types, Backend and Frontend import them.

**Issue:** QA failures block deployment
**Solution:** This is intentional! Fix critical issues before deploying. Use quality gates to maintain code quality.

## Related Commands

- `/dev-frontend-task` - Frontend development only
- `/dev-backend-task` - Backend development only
- `/qa-full-check` - Run QA crew without development
- `/deploy-full-pipeline` - Run deployment only

---

**Note:** This command requires all Development and QA agents to be available. Ensure your Claude Code environment has access to the full agent crew.
