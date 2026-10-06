# **Dark Mode**
## 1. Understand dark mode
**Tailwind has a built-in `dark:` variant — you choose *how* it activates (media or class).**
```tsx
<div className="bg-white dark:bg-slate-900">...</div>
```

## 2. Configure dark mode
**Set `darkMode: "class"` (or `"media"` or `"selector"`) in `tailwind.config`.**
```ts
// tailwind.config.ts
import type { Config } from "tailwindcss";

const config: Config = {
  darkMode: "class",
  content: ["./app/**/*.{ts,tsx}", "./components/**/*.{ts,tsx}"],
  theme: { extend: {} },
  plugins: [],
};

export default config;
```

## 3. Use `dark:`
**Prefix any utility with `dark:` and it applies when dark mode is active.**
```tsx
<p className="text-slate-900 dark:text-slate-100">Hello</p>
```

## 4. Dark backgrounds
**Pair a light page background with its dark counterpart (usually `slate-900/950`).**
```tsx
<body className="bg-white dark:bg-slate-950">
```

## 5. Dark text
**Use light text on dark surfaces; mute secondary text with lower-contrast shades.**
```tsx
<p className="text-slate-800 dark:text-slate-100">Title</p>
<p className="text-slate-500 dark:text-slate-400">Muted</p>
```

## 6. Dark borders
**Borders usually need to darken less than the background — use `slate-700`/`800`.**
```tsx
<div className="border border-slate-200 dark:border-slate-800">...</div>
```

## 7. Dark cards
**Cards lift off the page with a slightly lighter surface + darker border.**
```tsx
<div className="bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 rounded-2xl p-6
                shadow-sm dark:shadow-none">
  Card
</div>
```

## 8. Dark forms
**Invert input background, border, text, and placeholder; keep focus ring visible.**
```tsx
<input className="w-full px-3.5 py-2.5 rounded-xl
                  bg-white dark:bg-slate-900
                  text-slate-900 dark:text-slate-100
                  placeholder:text-slate-400 dark:placeholder:text-slate-500
                  border border-slate-300 dark:border-slate-700
                  focus:outline-none focus:border-indigo-500 focus:ring-4 focus:ring-indigo-500/20
                  dark:focus:border-indigo-400 dark:focus:ring-indigo-400/25" />
```

## 9. Dark navigation
**Keep sticky headers readable — light surface flips to a translucent dark.**
```tsx
<header className="sticky top-0 z-50
                   bg-white/80 dark:bg-slate-950/80
                   backdrop-blur
                   border-b border-slate-200 dark:border-slate-800">
  <nav className="h-14 px-4 flex items-center justify-between
                  text-slate-800 dark:text-slate-100">
    …
  </nav>
</header>
```

## 10. Dark dashboards
**Cards + charts + stat text all need matched dark counterparts; pick a *single* surface color per level.**
```tsx
<div className="min-h-screen bg-slate-50 dark:bg-slate-950">
  <div className="rounded-2xl bg-white dark:bg-slate-900
                  border border-slate-200 dark:border-slate-800 p-5">
    <p className="text-xs uppercase text-slate-500 dark:text-slate-400">Revenue</p>
    <p className="text-2xl font-bold text-slate-900 dark:text-slate-50">$12.4k</p>
  </div>
</div>
```

## 11. Light/dark color consistency
**Define semantic tokens once, reference them everywhere — don't scatter shades.**
```ts
// tailwind.config.ts
theme: {
  extend: {
    colors: {
      surface: { DEFAULT: "#ffffff", dark: "#0f172a" },
      ink:     { DEFAULT: "#0f172a", dark: "#f1f5f9" },
      line:    { DEFAULT: "#e2e8f0", dark: "#1e293b" },
    },
  },
}
```
```tsx
<div className="bg-surface dark:bg-surface-dark text-ink dark:text-ink-dark
                border border-line dark:border-line-dark">
  Consistent everywhere
</div>
```

---

## 🔧 Toggle pattern (class strategy)

```tsx
// components/ThemeToggle.tsx
"use client";
import { useEffect, useState } from "react";

export default function ThemeToggle() {
  const [dark, setDark] = useState(false);

  // On mount: read saved preference / system
  useEffect(() => {
    const saved = localStorage.getItem("theme");
    const prefers = window.matchMedia("(prefers-color-scheme: dark)").matches;
    const isDark = saved ? saved === "dark" : prefers;
    setDark(isDark);
    document.documentElement.classList.toggle("dark", isDark);
  }, []);

  function toggle() {
    const next = !dark;
    setDark(next);
    document.documentElement.classList.toggle("dark", next);
    localStorage.setItem("theme", next ? "dark" : "light");
  }

  return (
    <button
      onClick={toggle}
      aria-label="Toggle dark mode"
      className="p-2 rounded-lg hover:bg-slate-100 dark:hover:bg-slate-800
                 focus:outline-none focus-visible:ring-2 focus-visible:ring-indigo-500
                 transition-colors"
    >
      {dark ? "☀️" : "🌙"}
    </button>
  );
}
```

Add an inline script in `layout.tsx` to prevent flash-of-wrong-theme (FOWT):

```tsx
// app/layout.tsx — inside <head>
<script
  dangerouslySetInnerHTML={{
    __html: `
      try {
        var t = localStorage.getItem('theme');
        var d = t ? t === 'dark'
                  : window.matchMedia('(prefers-color-scheme: dark)').matches;
        if (d) document.documentElement.classList.add('dark');
      } catch (e) {}
    `,
  }}
/>
```

---

## 🎨 Dark-mode palette cheat-sheet

| Light | Dark | Purpose |
|---|---|---|
| `bg-white` | `bg-slate-950` / `bg-slate-900` | Page surface |
| `bg-slate-50` | `bg-slate-900` | Subtle surface |
| `bg-slate-100` | `bg-slate-800` | Muted surface |
| `text-slate-900` | `text-slate-50` | Primary text |
| `text-slate-600` | `text-slate-400` | Secondary text |
| `text-slate-400` | `text-slate-500` | Muted text |
| `border-slate-200` | `border-slate-800` | Default border |
| `border-slate-300` | `border-slate-700` | Stronger border |
| `shadow-md` | `shadow-none` (or keep subtle) | Shadows lose value in dark |
| `bg-indigo-600` | `bg-indigo-500` | Primary often needs to lift |
| `text-indigo-600` | `text-indigo-400` | Links need to brighten |
| `bg-emerald-50` | `bg-emerald-500/10` | Tinted success surface |
| `bg-rose-50` | `bg-rose-500/10` | Tinted error surface |

---

## 🧠 Rules of thumb

1. **Don't invert; re-tune.** Pure inversion looks harsh. Nudge lightness and saturation.
2. **Fewer layers in dark.** Cards are lighter than page, not darker.
3. **Shadows die in dark.** Replace with borders or subtle glows.
4. **Tinted surfaces via alpha.** `bg-emerald-500/10` reads better than `bg-emerald-900`.
5. **Keep contrast ≥ 4.5:1.** Especially for body text and links.
6. **Brand color often lifts one shade.** `indigo-600` → `indigo-500`.
7. **Test in both modes at once.** A side-by-side or toggle keeps you honest.

---

## ▶️ One-pager demo: full page in both modes

```tsx
// app/page.tsx
import ThemeToggle from "@/components/ThemeToggle";

export default function Home() {
  return (
    <div className="min-h-screen bg-slate-50 dark:bg-slate-950 text-slate-800 dark:text-slate-100">

      {/* ── 9. Navigation ── */}
      <header className="sticky top-0 z-50 bg-white/80 dark:bg-slate-950/80 backdrop-blur
                         border-b border-slate-200 dark:border-slate-800">
        <nav className="max-w-5xl mx-auto flex items-center justify-between px-4 sm:px-6 h-14">
          <a href="#" className="font-bold tracking-tight text-slate-900 dark:text-slate-50">
            ◆ Acme
          </a>
          <div className="flex items-center gap-2">
            <a href="#" className="hidden sm:inline text-sm text-slate-600 dark:text-slate-400 hover:text-indigo-600 dark:hover:text-indigo-400 transition-colors">
              Docs
            </a>
            <a href="#" className="hidden sm:inline text-sm text-slate-600 dark:text-slate-400 hover:text-indigo-600 dark:hover:text-indigo-400 transition-colors">
              Pricing
            </a>
            <ThemeToggle />
          </div>
        </nav>
      </header>

      <main className="max-w-5xl mx-auto px-4 sm:px-6 py-10 space-y-10">

        {/* ── Heading ── */}
        <header className="space-y-2">
          <h1 className="text-3xl sm:text-4xl font-bold tracking-tight text-slate-900 dark:text-slate-50">
            Dark Mode Demo
          </h1>
          <p className="text-slate-600 dark:text-slate-400 leading-relaxed">
            Every component below has a matched dark counterpart.
          </p>
        </header>

        {/* ── 7. Cards ── */}
        <section className="grid grid-cols-1 sm:grid-cols-3 gap-4">
          {[
            { label: "Revenue", value: "$12.4k" },
            { label: "Users", value: "1,284" },
            { label: "Orders", value: "342" },
          ].map((s) => (
            <div
              key={s.label}
              className="rounded-2xl bg-white dark:bg-slate-900
                         border border-slate-200 dark:border-slate-800
                         shadow-sm dark:shadow-none p-5"
            >
              <p className="text-xs uppercase tracking-wider text-slate-500 dark:text-slate-400">
                {s.label}
              </p>
              <p className="text-2xl font-bold text-slate-900 dark:text-slate-50 mt-2">
                {s.value}
              </p>
            </div>
          ))}
        </section>

        {/* ── 4 + 5 + 6. Backgrounds, text, borders ── */}
        <section className="rounded-2xl bg-white dark:bg-slate-900
                            border border-slate-200 dark:border-slate-800 p-6 space-y-3">
          <h2 className="text-lg font-semibold text-slate-900 dark:text-slate-50">
            Text & borders
          </h2>
          <p className="text-slate-700 dark:text-slate-300">
            Primary body text — slate-700 / slate-300.
          </p>
          <p className="text-slate-500 dark:text-slate-400">
            Secondary text — slate-500 / slate-400.
          </p>
          <p className="text-slate-400 dark:text-slate-500">
            Muted text — slate-400 / slate-500.
          </p>
          <div className="border border-slate-200 dark:border-slate-800 rounded-xl p-3 text-sm">
            Bordered block — slate-200 / slate-800
          </div>
        </section>

        {/* ── 8. Form ── */}
        <section className="rounded-2xl bg-white dark:bg-slate-900
                            border border-slate-200 dark:border-slate-800 p-6 space-y-4">
          <h2 className="text-lg font-semibold text-slate-900 dark:text-slate-50">
            Form
          </h2>

          <div className="space-y-1.5">
            <label className="text-sm font-medium text-slate-700 dark:text-slate-300">
              Email
            </label>
            <input
              placeholder="you@example.com"
              className="w-full px-3.5 py-2.5 rounded-xl
                         bg-white dark:bg-slate-950
                         text-slate-900 dark:text-slate-100
                         placeholder:text-slate-400 dark:placeholder:text-slate-500
                         border border-slate-300 dark:border-slate-700
                         focus:outline-none
                         focus:border-indigo-500 focus:ring-4 focus:ring-indigo-500/20
                         dark:focus:border-indigo-400 dark:focus:ring-indigo-400/25
                         transition-all duration-200"
            />
          </div>

          <div className="space-y-1.5">
            <label className="text-sm font-medium text-slate-700 dark:text-slate-300">
              Message
            </label>
            <textarea
              rows={3}
              placeholder="Type something…"
              className="w-full px-3.5 py-2.5 rounded-xl resize-none
                         bg-white dark:bg-slate-950
                         text-slate-900 dark:text-slate-100
                         placeholder:text-slate-400 dark:placeholder:text-slate-500
                         border border-slate-300 dark:border-slate-700
                         focus:outline-none focus:border-indigo-500 focus:ring-4 focus:ring-indigo-500/20
                         dark:focus:border-indigo-400 dark:focus:ring-indigo-400/25"
            />
          </div>

          <label className="inline-flex items-center gap-2 cursor-pointer">
            <input type="checkbox" className="peer sr-only" />
            <span className="w-5 h-5 rounded-md border border-slate-300 dark:border-slate-700 bg-white dark:bg-slate-950
                             grid place-items-center text-white text-xs transition
                             peer-checked:bg-indigo-600 peer-checked:border-indigo-600
                             peer-focus-visible:ring-2 peer-focus-visible:ring-indigo-500 peer-focus-visible:ring-offset-2
                             dark:peer-focus-visible:ring-offset-slate-900">
              ✓
            </span>
            <span className="text-sm text-slate-700 dark:text-slate-300">
              Subscribe to updates
            </span>
          </label>

          <div className="flex flex-col sm:flex-row gap-3 pt-2">
            <button className="flex-1 py-2.5 rounded-xl font-medium
                               bg-indigo-600 dark:bg-indigo-500 text-white
                               hover:bg-indigo-700 dark:hover:bg-indigo-400
                               transition-colors
                               focus:outline-none focus-visible:ring-2 focus-visible:ring-indigo-500 focus-visible:ring-offset-2
                               dark:focus-visible:ring-offset-slate-900">
              Save
            </button>
            <button className="flex-1 py-2.5 rounded-xl font-medium
                               border border-slate-300 dark:border-slate-700
                               text-slate-700 dark:text-slate-300
                               hover:bg-slate-50 dark:hover:bg-slate-800
                               transition-colors
                               focus:outline-none focus-visible:ring-2 focus-visible:ring-slate-500 focus-visible:ring-offset-2
                               dark:focus-visible:ring-offset-slate-900">
              Cancel
            </button>
          </div>
        </section>

        {/* ── Tinted states in both modes ── */}
        <section className="grid grid-cols-1 sm:grid-cols-3 gap-4">
          <div className="rounded-xl p-4 text-sm
                          bg-emerald-50 dark:bg-emerald-500/10
                          text-emerald-800 dark:text-emerald-300
                          border border-emerald-200 dark:border-emerald-500/20">
            ✓ Success message
          </div>
          <div className="rounded-xl p-4 text-sm
                          bg-amber-50 dark:bg-amber-500/10
                          text-amber-800 dark:text-amber-300
                          border border-amber-200 dark:border-amber-500/20">
            ⚠ Warning message
          </div>
          <div className="rounded-xl p-4 text-sm
                          bg-rose-50 dark:bg-rose-500/10
                          text-rose-800 dark:text-rose-300
                          border border-rose-200 dark:border-rose-500/20">
            ✕ Error message
          </div>
        </section>

      </main>
    </div>
  );
}
```

---

## ✅ Coverage checklist

| Concept | Where |
|---|---|
| Understand dark mode | Built-in `dark:` variant |
| Configure dark mode | `darkMode: "class"` in config |
| Use `dark:` | Everywhere in the demo |
| Dark backgrounds | Page + cards + inputs |
| Dark text | Heading / body / muted tiers |
| Dark borders | Cards, inputs, dividers |
| Dark cards | Stats + forms sections |
| Dark forms | Input, textarea, checkbox, buttons |
| Dark navigation | Sticky header |
| Dark dashboards | Stat card pattern |
| Light/dark color consistency | Matched shade pairs + tinted states |

---
