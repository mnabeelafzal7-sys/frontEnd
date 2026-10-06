# Tailwind + Next.js (App Router)

## 1. Tailwind with Next.js
**Install Tailwind, point `content` at `./app`, import `globals.css` once in the root layout.**
```bash
npm install -D tailwindcss postcss autoprefixer && npx tailwindcss init -p
```
```ts
// tailwind.config.ts
content: ["./app/**/*.{ts,tsx}", "./components/**/*.{ts,tsx}"]
```

## 2. App Router styling
**Every route lives in `app/`; styling flows from `layout.tsx` → `page.tsx` → nested layouts.**
```
app/
├── layout.tsx          # root: <html>, <body>, providers
├── page.tsx            # home
├── dashboard/
│   ├── layout.tsx      # nested shell (sidebar, nav)
│   └── page.tsx        # dashboard page
```

## 3. Server Component styling
**Default in App Router — style freely; no hooks, no event handlers.**
```tsx
// app/blog/page.tsx (Server Component by default)
export default async function Page() {
  const posts = await fetchPosts();
  return (
    <ul className="divide-y divide-slate-200">
      {posts.map((p) => (
        <li key={p.id} className="py-3 text-sm text-slate-700">{p.title}</li>
      ))}
    </ul>
  );
}
```

## 4. Client Component styling
**Add `"use client"` at the top when you need state, effects, or events.**
```tsx
"use client";
import { useState } from "react";

export function Counter() {
  const [n, setN] = useState(0);
  return (
    <button onClick={() => setN(n + 1)}
            className="px-4 py-2 rounded-lg bg-indigo-600 text-white hover:bg-indigo-700 transition">
      Count: {n}
    </button>
  );
}
```

## 5. Layout styling
**Root layout wraps the whole app — put global shell (fonts, providers, body bg) here.**
```tsx
// app/layout.tsx
import "./globals.css";
import { Inter } from "next/font/google";

const inter = Inter({ subsets: ["latin"], variable: "--font-inter" });

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en" className={inter.variable}>
      <body className="min-h-screen bg-slate-50 text-slate-800 antialiased font-sans">
        {children}
      </body>
    </html>
  );
}
```

## 6. Page styling
**Each `page.tsx` owns its own container + spacing — don't repeat the shell.**
```tsx
// app/pricing/page.tsx
export default function Page() {
  return (
    <main className="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8 py-12 space-y-8">
      <h1 className="text-3xl sm:text-4xl font-bold tracking-tight">Pricing</h1>
      {/* sections */}
    </main>
  );
}
```

## 7. Responsive Next.js navbar
**Sticky + backdrop blur; collapse links below `md`, expand at `md+`.**
```tsx
// components/Navbar.tsx (Server Component is fine — no state)
import Link from "next/link";

export function Navbar() {
  return (
    <header className="sticky top-0 z-50 bg-white/80 dark:bg-slate-950/80 backdrop-blur border-b border-slate-200 dark:border-slate-800">
      <nav className="max-w-7xl mx-auto flex items-center justify-between h-14 px-4 sm:px-6">
        <Link href="/" className="font-bold tracking-tight">◆ Acme</Link>
        <ul className="hidden md:flex items-center gap-6 text-sm text-slate-600 dark:text-slate-400">
          <li><Link href="/pricing" className="hover:text-indigo-600 transition-colors">Pricing</Link></li>
          <li><Link href="/docs" className="hover:text-indigo-600 transition-colors">Docs</Link></li>
        </ul>
        <Link href="/login" className="px-4 py-2 rounded-lg bg-indigo-600 text-white text-sm font-medium hover:bg-indigo-700 transition">
          Sign in
        </Link>
      </nav>
    </header>
  );
}
```
For a mobile drawer, make it a Client Component with `useState`.

## 8. Dashboard layout
**Nested `layout.tsx` under `/dashboard` owns the shell: sidebar + content.**
```tsx
// app/dashboard/layout.tsx
export default function DashboardLayout({ children }: { children: React.ReactNode }) {
  return (
    <div className="min-h-screen flex">
      <aside className="hidden lg:flex w-60 shrink-0 flex-col bg-white dark:bg-slate-900 border-r border-slate-200 dark:border-slate-800">
        <div className="h-14 flex items-center px-4 font-bold border-b border-slate-200 dark:border-slate-800">
          ◆ Acme
        </div>
        <nav className="p-3 space-y-1 text-sm">
          <a className="block px-3 py-2 rounded-lg hover:bg-slate-100 dark:hover:bg-slate-800">Overview</a>
          <a className="block px-3 py-2 rounded-lg hover:bg-slate-100 dark:hover:bg-slate-800">Analytics</a>
          <a className="block px-3 py-2 rounded-lg hover:bg-slate-100 dark:hover:bg-slate-800">Settings</a>
        </nav>
      </aside>
      <main className="flex-1 min-w-0 p-4 sm:p-6 lg:p-8">{children}</main>
    </div>
  );
}
```

## 9. Authentication UI
**Route group `(auth)` for auth pages + centered card layout.**
```tsx
// app/(auth)/layout.tsx
export default function AuthLayout({ children }: { children: React.ReactNode }) {
  return (
    <div className="min-h-screen grid place-items-center p-4 bg-slate-100">
      <div className="w-full max-w-md">{children}</div>
    </div>
  );
}
```
```tsx
// app/(auth)/login/page.tsx
export default function LoginPage() {
  return (
    <div className="rounded-3xl bg-white border border-slate-200 shadow-sm p-6 sm:p-8">
      <h1 className="text-2xl font-bold tracking-tight mb-1">Welcome back</h1>
      <p className="text-sm text-slate-500 mb-6">Sign in to your account.</p>
      {/* form components */}
    </div>
  );
}
```

## 10. Loading UI
**Add `loading.tsx` in any route folder — Next renders it automatically with Suspense.**
```tsx
// app/dashboard/loading.tsx
export default function Loading() {
  return (
    <div className="space-y-4 p-6">
      <div className="h-6 w-40 rounded bg-slate-200 animate-pulse" />
      <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
        {Array.from({ length: 4 }).map((_, i) => (
          <div key={i} className="rounded-2xl bg-white border border-slate-200 p-5">
            <div className="h-3 w-16 rounded bg-slate-200 animate-pulse mb-3" />
            <div className="h-6 w-24 rounded bg-slate-200 animate-pulse" />
          </div>
        ))}
      </div>
    </div>
  );
}
```

## 11. Error UI
**Add `error.tsx` — must be a Client Component, receives `error` + `reset`.**
```tsx
// app/dashboard/error.tsx
"use client";

export default function Error({ error, reset }: { error: Error; reset: () => void }) {
  return (
    <div className="min-h-[60vh] grid place-items-center p-6">
      <div className="max-w-md w-full rounded-2xl bg-white border border-rose-200 p-6 text-center space-y-4">
        <div className="text-3xl">⚠️</div>
        <h2 className="text-xl font-semibold text-slate-900">Something went wrong</h2>
        <p className="text-sm text-slate-600">{error.message || "Please try again."}</p>
        <div className="flex gap-3 justify-center">
          <button onClick={reset}
                  className="px-4 py-2 rounded-lg bg-indigo-600 text-white text-sm font-medium hover:bg-indigo-700">
            Try again
          </button>
          <a href="/" className="px-4 py-2 rounded-lg border border-slate-300 text-sm font-medium hover:bg-slate-50">
            Go home
          </a>
        </div>
      </div>
    </div>
  );
}
```

## 12. Not-found UI
**Add `not-found.tsx` at app root (or per-route) for 404s.**
```tsx
// app/not-found.tsx
export default function NotFound() {
  return (
    <div className="min-h-[80vh] grid place-items-center p-6">
      <div className="text-center space-y-4 max-w-md">
        <p className="text-6xl font-bold bg-gradient-to-r from-indigo-600 to-purple-600 bg-clip-text text-transparent">
          404
        </p>
        <h1 className="text-2xl font-semibold text-slate-900">Page not found</h1>
        <p className="text-sm text-slate-600">The page you're looking for doesn't exist.</p>
        <a href="/" className="inline-block px-4 py-2 rounded-lg bg-indigo-600 text-white text-sm font-medium hover:bg-indigo-700">
          Back home
        </a>
      </div>
    </div>
  );
}
```

## 13. SEO-friendly responsive layouts
**Export `metadata` (or `generateMetadata`) from server pages; semantic HTML + responsive classes.**
```tsx
// app/blog/[slug]/page.tsx
import type { Metadata } from "next";

export async function generateMetadata({ params }: { params: { slug: string } }): Promise<Metadata> {
  const post = await getPost(params.slug);
  return {
    title: post.title,
    description: post.excerpt,
    openGraph: { title: post.title, images: [post.cover] },
  };
}

export default async function Page({ params }: { params: { slug: string } }) {
  const post = await getPost(params.slug);
  return (
    <article className="max-w-3xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
      <h1 className="text-3xl sm:text-4xl lg:text-5xl font-bold tracking-tight leading-tight">
        {post.title}
      </h1>
      <p className="mt-4 text-base sm:text-lg text-slate-600 leading-relaxed">{post.excerpt}</p>
      {/* body */}
    </article>
  );
}
```

---

## 🧠 App Router styling map

| File | Purpose | Component type |
|---|---|---|
| `app/layout.tsx` | Root shell — html, body, fonts, providers | Server |
| `app/page.tsx` | Home route | Server (default) |
| `app/**/layout.tsx` | Nested shell (sidebar, tabs, etc.) | Server |
| `app/**/page.tsx` | Route content | Server |
| `app/**/loading.tsx` | Suspense fallback | Server |
| `app/**/error.tsx` | Error boundary | **Client** |
| `app/**/not-found.tsx` | 404 UI | Server |
| `app/(group)/` | Route group — share a layout, no URL segment | — |
| `app/api/*/route.ts` | API handlers | Server |

---

## ▶️ One-pager demo: file tree + every file

```
app/
├── layout.tsx
├── globals.css
├── page.tsx
├── loading.tsx
├── error.tsx                 (client)
├── not-found.tsx
├── (auth)/
│   ├── layout.tsx
│   └── login/
│       └── page.tsx
└── dashboard/
    ├── layout.tsx
    ├── loading.tsx
    ├── error.tsx             (client)
    └── page.tsx
components/
├── Navbar.tsx
└── Sidebar.tsx
```

**`app/globals.css`**
```css
@tailwind base;
@tailwind components;
@tailwind utilities;

html { scroll-behavior: smooth; }
```

**`app/layout.tsx`**
```tsx
import "./globals.css";
import type { Metadata } from "next";
import { Inter } from "next/font/google";

const inter = Inter({ subsets: ["latin"], variable: "--font-inter" });

export const metadata: Metadata = {
  title: { default: "Acme", template: "%s · Acme" },
  description: "Responsive Next.js app with Tailwind.",
};

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en" className={inter.variable}>
      <body className="min-h-screen bg-slate-50 text-slate-800 antialiased font-sans">
        {children}
      </body>
    </html>
  );
}
```

**`app/page.tsx`**
```tsx
export default function Home() {
  return (
    <main className="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8 py-16 space-y-6 text-center">
      <h1 className="text-4xl sm:text-5xl lg:text-6xl font-bold tracking-tight text-balance">
        Ship faster with Next.js + Tailwind
      </h1>
      <p className="text-base sm:text-lg text-slate-600 leading-relaxed max-w-2xl mx-auto">
        App Router, Server Components, responsive layouts — all in one place.
      </p>
      <div className="flex flex-col sm:flex-row gap-3 justify-center">
        <a href="/dashboard" className="px-6 py-3 rounded-xl bg-indigo-600 text-white font-medium hover:bg-indigo-700 transition">
          Open dashboard
        </a>
        <a href="/login" className="px-6 py-3 rounded-xl border border-slate-300 font-medium hover:bg-slate-50 transition">
          Sign in
        </a>
      </div>
    </main>
  );
}
```

**`app/dashboard/layout.tsx`**
```tsx
import Link from "next/link";

export default function DashboardLayout({ children }: { children: React.ReactNode }) {
  return (
    <div className="min-h-screen flex">
      <aside className="hidden lg:flex w-60 shrink-0 flex-col bg-white border-r border-slate-200">
        <Link href="/" className="h-14 flex items-center px-4 font-bold border-b border-slate-200">◆ Acme</Link>
        <nav className="p-3 space-y-1 text-sm">
          <Link href="/dashboard" className="block px-3 py-2 rounded-lg hover:bg-slate-100">Overview</Link>
          <Link href="/dashboard/analytics" className="block px-3 py-2 rounded-lg hover:bg-slate-100">Analytics</Link>
          <Link href="/dashboard/settings" className="block px-3 py-2 rounded-lg hover:bg-slate-100">Settings</Link>
        </nav>
      </aside>
      <main className="flex-1 min-w-0 p-4 sm:p-6 lg:p-8">{children}</main>
    </div>
  );
}
```

**`app/dashboard/page.tsx`**
```tsx
export default function DashboardPage() {
  return (
    <div className="space-y-6">
      <h1 className="text-2xl font-bold tracking-tight">Dashboard</h1>
      <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
        {["Revenue", "Users", "Orders", "Conversion"].map((label) => (
          <div key={label} className="rounded-2xl bg-white border border-slate-200 p-5 shadow-sm">
            <p className="text-xs uppercase tracking-wider text-slate-500">{label}</p>
            <p className="text-2xl font-bold text-slate-900 mt-2">—</p>
          </div>
        ))}
      </div>
    </div>
  );
}
```

**`app/loading.tsx`**
```tsx
export default function Loading() {
  return (
    <div className="min-h-screen grid place-items-center">
      <div className="w-8 h-8 rounded-full border-2 border-slate-300 border-t-indigo-600 animate-spin" />
    </div>
  );
}
```

**`app/error.tsx`**
```tsx
"use client";
export default function Error({ error, reset }: { error: Error; reset: () => void }) {
  return (
    <div className="min-h-[60vh] grid place-items-center p-6">
      <div className="max-w-md text-center space-y-4">
        <h2 className="text-xl font-semibold">Something went wrong</h2>
        <p className="text-sm text-slate-600">{error.message}</p>
        <button onClick={reset} className="px-4 py-2 rounded-lg bg-indigo-600 text-white text-sm">Try again</button>
      </div>
    </div>
  );
}
```

**`app/not-found.tsx`**
```tsx
export default function NotFound() {
  return (
    <div className="min-h-[80vh] grid place-items-center p-6 text-center">
      <div className="space-y-3">
        <p className="text-6xl font-bold bg-gradient-to-r from-indigo-600 to-purple-600 bg-clip-text text-transparent">404</p>
        <h1 className="text-2xl font-semibold">Page not found</h1>
        <a href="/" className="inline-block px-4 py-2 rounded-lg bg-indigo-600 text-white text-sm">Back home</a>
      </div>
    </div>
  );
}
```

---

## ✅ Coverage checklist

| Concept | Where |
|---|---|
| Tailwind with Next.js | Install + `content` + `globals.css` |
| App Router styling | File-tree layout |
| Server Component styling | `page.tsx`, `layout.tsx` default |
| Client Component styling | `error.tsx`, form toggle |
| Layout styling | Root + dashboard + auth layouts |
| Page styling | `page.tsx` container discipline |
| Responsive Next.js navbar | `Navbar.tsx` sticky + `md:` links |
| Dashboard layout | `app/dashboard/layout.tsx` sidebar shell |
| Authentication UI | `app/(auth)/` route group |
| Loading UI | `app/**/loading.tsx` |
| Error UI | `app/**/error.tsx` (Client) |
| Not-found UI | `app/not-found.tsx` |
| SEO-friendly responsive layouts | `metadata` + `generateMetadata` + semantic HTML |

---
