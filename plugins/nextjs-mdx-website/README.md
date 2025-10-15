# Next.js MDX Website Plugin

A comprehensive Claude Code plugin for developing modern Next.js 15 websites with TypeScript, MDX blog functionality, Tailwind CSS, Framer Motion, and Vercel deployment automation.

## Overview

This plugin provides specialized agents and commands for building production-ready Next.js websites with:

- **Next.js 15** with App Router and server/client components
- **TypeScript 5** for type safety
- **MDX** for powerful blog content with React components
- **Tailwind CSS 3.4** for utility-first styling
- **Framer Motion** for smooth animations
- **Vercel** deployment with optimization
- **PWA** support with offline capabilities

Perfect for marketing sites, blogs, documentation, portfolios, and content-driven applications.

## What's Included

### 🤖 Specialized Agents

#### MDX Content Agent (`mdx-content-agent`)
Expert in creating and editing MDX blog posts with proper frontmatter, SEO optimization, and React component integration.

**Use for:**
- Creating blog posts with complete frontmatter
- SEO optimization (titles, descriptions, Open Graph)
- Integrating React components in MDX
- Code syntax highlighting configuration
- Content structure and readability

**Tools:** Read, Write, Edit, Glob, Grep, TodoWrite

#### Next.js Page Agent (`nextjs-page-agent`)
Specializes in building Next.js 15 App Router pages with TypeScript, server/client components, and metadata configuration.

**Use for:**
- Creating App Router pages with TypeScript
- Server and client component patterns
- Metadata and SEO configuration
- Dynamic and static routes
- Layout and template files

**Tools:** Read, Write, Edit, Glob, Grep, TodoWrite

#### Vercel Deployment Agent (`vercel-deployment-agent`)
Expert in Vercel deployment configuration, environment setup, build optimization, and production deployments.

**Use for:**
- Vercel deployment configuration
- Build optimization and troubleshooting
- Environment variable management
- Security headers and redirects
- Performance monitoring

**Tools:** Read, Write, Edit, Bash, Grep, TodoWrite, GitHub Actions workflow tools

#### Component & Styling Agent (`component-styling-agent`)
Specializes in creating React components with Tailwind CSS, Framer Motion animations, and TypeScript.

**Use for:**
- React component development
- Tailwind CSS utility-first styling
- Framer Motion animations
- Responsive design patterns
- Dark mode implementation
- Accessibility features

**Tools:** Read, Write, Edit, Glob, Grep, TodoWrite

### ⚡ Slash Commands

#### `/new-blog-post [title]`
Creates a new MDX blog post with proper frontmatter and structure.

**Example:**
```
/new-blog-post How to Deploy Next.js to Vercel
```

Creates: `content/blog/how-to-deploy-nextjs-to-vercel.mdx`

#### `/new-page [route-path]`
Creates a new Next.js App Router page with TypeScript, metadata, and client/server component structure.

**Example:**
```
/new-page about-us
```

Creates:
```
src/app/about-us/
├── page.tsx
├── metadata.ts
└── ClientPage.tsx
```

#### `/deploy-vercel [environment]`
Deploys the Next.js site to Vercel after running build checks and linting.

**Examples:**
```
/deploy-vercel preview    # Deploy to preview
/deploy-vercel production # Deploy to production
```

## Installation

### Prerequisites

- Node.js 18+ and npm
- Git
- Docker Desktop with MCP Toolkit enabled (see [Docker MCP Guide](../../docs/DOCKER-MCP-GUIDE.md))
- Claude Code

### Setup Steps

1. **Clone or link this plugin** to your Claude Code plugins directory:

```bash
# Option 1: Clone the marketplace repo
git clone https://github.com/sati-technology/sati-claude-marketplace.git

# Option 2: Copy just this plugin
cp -r path/to/plugins/nextjs-mdx-website ~/.claude-code/plugins/
```

2. **Enable the plugin** in Claude Code:

The plugin will be automatically detected from the `.claude-plugin/plugin.json` file.

3. **Install project dependencies**:

```bash
npm install
```

4. **Set up Vercel** (optional, for deployment):

```bash
# Install Vercel CLI
npm i -g vercel

# Login to Vercel
vercel login

# Link your project
vercel link
```

## Usage

### Creating a New Blog Post

**Using the command:**
```
/new-blog-post Building Modern Web Apps with Next.js
```

**Using the agent directly:**
Ask Claude Code to:
> "Create a blog post about building modern web apps with Next.js, covering App Router, server components, and deployment"

The MDX Content Agent will create a complete blog post with:
- SEO-optimized frontmatter
- Proper heading structure
- Code examples with syntax highlighting
- Reading time estimation
- Category and tags

### Creating a New Page

**Using the command:**
```
/new-page services
```

**Using the agent directly:**
Ask Claude Code to:
> "Create a services page that showcases our offerings with TypeScript and proper metadata"

The Next.js Page Agent will create:
- `src/app/services/page.tsx` - Server component
- `src/app/services/metadata.ts` - SEO metadata
- `src/app/services/ClientPage.tsx` - Client component (if interactivity needed)

### Building Components

Ask Claude Code to:
> "Create a hero section component with Framer Motion animations and Tailwind styling"

The Component & Styling Agent will build:
- TypeScript component with proper types
- Tailwind CSS utility classes
- Framer Motion animations
- Responsive design
- Dark mode support
- Accessibility features

### Deploying to Vercel

**Using the command:**
```
/deploy-vercel preview
```

**Using the agent directly:**
Ask Claude Code to:
> "Deploy the site to Vercel production with security headers configured"

The Vercel Deployment Agent will:
1. Run pre-deployment checks (lint, type-check, build)
2. Configure `vercel.json` with security headers
3. Set up environment variables
4. Deploy to specified environment
5. Verify deployment and provide URL

## Project Structure

This plugin expects (and helps create) the following structure:

```
your-nextjs-project/
├── src/
│   ├── app/                  # Next.js App Router
│   │   ├── layout.tsx        # Root layout
│   │   ├── page.tsx          # Home page
│   │   ├── blog/
│   │   │   ├── page.tsx      # Blog list
│   │   │   └── [slug]/
│   │   │       └── page.tsx  # Blog post page
│   │   └── [your-pages]/
│   ├── components/           # React components
│   │   ├── ui/              # Reusable UI components
│   │   └── mdx/             # MDX components
│   └── lib/                 # Utilities
├── content/
│   └── blog/                # MDX blog posts
├── public/                  # Static assets
├── next.config.ts           # Next.js config
├── tailwind.config.ts       # Tailwind config
├── vercel.json             # Vercel config
└── package.json
```

## Configuration

### Tailwind CSS

Ensure your `tailwind.config.ts` includes:

```typescript
import type { Config } from 'tailwindcss';

const config: Config = {
  content: [
    './src/**/*.{js,ts,jsx,tsx,mdx}',
    './content/**/*.{md,mdx}',
  ],
  darkMode: 'class',
  theme: {
    extend: {
      // Your customizations
    },
  },
  plugins: [
    require('@tailwindcss/typography'),
  ],
};

export default config;
```

### MDX Configuration

Install required packages:

```bash
npm install next-mdx-remote gray-matter
```

### Environment Variables

Required for production:

```bash
# .env.local
NEXT_PUBLIC_SITE_URL=https://yoursite.com
NEXT_PUBLIC_GA_MEASUREMENT_ID=G-XXXXXXXXXX
NEXT_PUBLIC_CALENDLY_URL=https://calendly.com/yourname
```

## Examples

### Complete Blog Post Workflow

1. **Create post:**
```
/new-blog-post Modern Authentication Patterns
```

2. **Ask agent to enhance:**
> "Add code examples for OAuth implementation and JWT handling"

3. **Optimize for SEO:**
> "Optimize this blog post for SEO targeting 'authentication best practices'"

4. **Deploy:**
```
/deploy-vercel preview
```

### Building a Landing Page

Ask Claude Code:
> "Create a landing page at /landing with a hero section, features grid, and CTA section. Use Framer Motion for scroll animations and Tailwind for styling."

The agents will:
1. **Next.js Page Agent:** Create route structure
2. **Component & Styling Agent:** Build hero, features, and CTA components
3. **Vercel Deployment Agent:** Configure and deploy

## Best Practices

### Content Management
- Store blog posts in `content/blog/` with kebab-case filenames
- Include complete frontmatter for SEO
- Use semantic headings (h2, h3) for structure
- Add alt text for images

### Component Development
- Use TypeScript for all components
- Follow server component by default, client when needed
- Implement proper error boundaries
- Add loading states

### Styling
- Use Tailwind utility classes over custom CSS
- Implement dark mode with `dark:` variants
- Ensure mobile-first responsive design
- Maintain consistent spacing scale

### Deployment
- Test locally with `npm run build`
- Use preview deployments for testing
- Set environment variables in Vercel dashboard
- Monitor deployments with Vercel Analytics

## Troubleshooting

### Build Failures

**TypeScript errors:**
```bash
npm run type-check
```

**ESLint errors:**
```bash
npm run lint
```

**Build errors:**
```bash
rm -rf .next
npm run build
```

### MDX Issues

**MDX not rendering:**
- Check file is in `content/blog/` directory
- Verify frontmatter format
- Ensure proper import in page component

### Deployment Issues

**Environment variables not set:**
```bash
vercel env pull .env.local
vercel env add VARIABLE_NAME production
```

**Build fails on Vercel:**
- Check logs: `vercel logs <deployment-url>`
- Verify Node version in `package.json` engines
- Ensure all dependencies are in `package.json`

## Tech Stack

- **Next.js 15** - React framework with App Router
- **TypeScript 5** - Type safety
- **Tailwind CSS 3.4** - Utility-first CSS
- **Framer Motion** - Animation library
- **MDX** - Markdown with JSX
- **next-mdx-remote** - MDX in Next.js
- **Vercel** - Deployment platform
- **next-pwa** - Progressive Web App support

## Resources

- [Next.js Documentation](https://nextjs.org/docs)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
- [Framer Motion Documentation](https://www.framer.com/motion)
- [MDX Documentation](https://mdxjs.com)
- [Vercel Documentation](https://vercel.com/docs)
- [TypeScript Documentation](https://www.typescriptlang.org/docs)

## Contributing

Found a bug or want to improve this plugin? Contributions are welcome!

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

See [CONTRIBUTING.md](../../CONTRIBUTING.md) for detailed guidelines.

## License

MIT License - see [LICENSE](../../LICENSE) for details.

## Support

- **Issues:** [GitHub Issues](https://github.com/sati-technology/sati-claude-marketplace/issues)
- **Documentation:** [Full Documentation](../../docs)
- **Examples:** Check the example projects in the marketplace

---

**Built by [Sati Technology](https://github.com/sati-technology)** | Part of the [Sati Claude Code Marketplace](https://github.com/sati-technology/sati-claude-marketplace)
