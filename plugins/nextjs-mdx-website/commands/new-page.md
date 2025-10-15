---
name: new-page
description: Create a new Next.js App Router page with TypeScript and proper structure
---

# New Page

Creates a new page in the Next.js App Router with TypeScript, metadata, and client/server component structure.

## Usage

/new-page [route-path]

## What This Does

1. Creates directory in `src/app/[route-path]/`
2. Generates `page.tsx` with proper TypeScript types
3. Creates `metadata.ts` for SEO
4. Optionally creates `ClientPage.tsx` for client-side interactivity
5. Sets up proper imports and exports

## Examples

```
/new-page about-us
```

Creates:
```
src/app/about-us/
├── page.tsx
├── metadata.ts
└── ClientPage.tsx (if needed)
```

## Page Structure

### Server Component (page.tsx)
```typescript
import { Metadata } from 'next';
import ClientPage from './ClientPage';

export { metadata } from './metadata';

export default function AboutUsPage() {
  return <ClientPage />;
}
```

### Client Component (ClientPage.tsx)
```typescript
'use client';

export default function AboutUsClientPage() {
  return (
    <div className="container mx-auto">
      {/* Your content */}
    </div>
  );
}
```

### Metadata (metadata.ts)
```typescript
import { Metadata } from 'next';

export const metadata: Metadata = {
  title: 'About Us | Your Site',
  description: 'Learn more about us',
};
```

## Requirements

- Next.js 15 with App Router
- TypeScript
- Project must have `src/app/` directory
