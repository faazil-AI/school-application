# Development Guidelines

## Important: Next.js 15 Compatibility

This project uses **Next.js 15** with the App Router. The framework has breaking changes from previous versions:
- APIs, conventions, and file structure may differ from older documentation
- Always refer to `node_modules/next/dist/docs/` or [Next.js 15 official docs](https://nextjs.org/docs) before writing new code
- Use TypeScript for type safety

## Key Technologies

- **Framework**: Next.js 15 (App Router)
- **Language**: TypeScript 5
- **Database**: PostgreSQL 17 + Prisma ORM
- **Auth**: Auth.js (NextAuth v5) with Email OTP & Google Sign-In
- **UI**: React 19, Tailwind CSS 4, Radix UI components
- **Validation**: Zod for schema validation
- **Email**: Resend (primary) / SMTP (fallback)

## Development Commands

```bash
npm run dev           # Start development server
npm run build         # Build for production
npm run start         # Production server
npm run lint          # Run ESLint
npm run type-check    # TypeScript type checking
npm run db:studio    # Prisma Studio (database GUI)
npm run db:seed      # Seed database
```

## Code Quality Standards

- Use TypeScript strictly (no `any` types)
- Run `npm run lint` before commits
- Run `npm run type-check` to catch type errors
- Follow Next.js App Router patterns
- Keep components functional and modular

For complete setup and deployment instructions, refer to [README.md](./README.md).
