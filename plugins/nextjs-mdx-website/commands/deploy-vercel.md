---
name: deploy-vercel
description: Deploy the Next.js site to Vercel with proper checks and deployment
---

# Deploy to Vercel

Deploys the Next.js website to Vercel after running build checks and linting.

## Usage

/deploy-vercel [environment]

Environments:
- `preview` - Deploy to preview environment (default)
- `production` - Deploy to production

## What This Does

1. **Pre-deployment checks**:
   - Runs `npm run lint` to check for code issues
   - Runs `npm run build` to ensure production build works
   - Checks for TypeScript errors

2. **Deployment**:
   - Uses Vercel CLI or GitHub integration
   - Deploys to specified environment
   - Shows deployment URL when complete

3. **Post-deployment**:
   - Verifies deployment is live
   - Checks for any build warnings
   - Provides deployment URL

## Examples

```
/deploy-vercel preview
```

Deploys to preview environment for testing.

```
/deploy-vercel production
```

Deploys to production (prompts for confirmation).

## Prerequisites

- Vercel CLI installed (`npm i -g vercel`)
- Vercel account linked (`vercel login`)
- Project linked to Vercel (`vercel link`)

## Environment Variables

Ensure these are set in Vercel dashboard:
- `NEXT_PUBLIC_CALENDLY_URL`
- `NEXT_PUBLIC_GA_MEASUREMENT_ID` (optional)

## Vercel Configuration

The deployment respects `vercel.json` settings:
- Security headers
- Redirects
- Custom domain configuration
