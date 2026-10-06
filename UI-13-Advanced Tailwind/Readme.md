# Advanced Tailwind

One-liners + shortest code for every escape hatch Tailwind gives you.

---

## 1. Arbitrary properties
**Use `[property:value]` to write any CSS declaration directly in a class.**
```tsx
<div className="[mask-type:luminance] [scrollbar-width:thin]">…</div>
```

## 2. Arbitrary values
**Use `utility-[value]` for one-off values inside an existing utility.**
```tsx
<div className="w-[420px] text-[13px] bg-[#0f172a] grid-cols-[1fr_2fr_auto]">…</div>
```

## 3. Arbitrary variants
**Use `[&_selector]:` or `[&:state]:` to invent a variant on the spot.**
```tsx
<ul className="[&>li]:py-2 [&>li:last-child]:border-0 [&_a]:text-indigo-600">…</ul>
```
```tsx
<button className="[&:nth-child(3)]:bg-rose-500">…</button>
```

## 4. Custom utilities
**Register reusable classes via `@layer utilities` or the `plugin()` API.**
```css
/* globals.css */
@layer utilities {
  .text-balance { text-wrap: balance; }
  .scrollbar-hide::-webkit-scrollbar { display: none; }
  .scrollbar-hide { scrollbar-width: none; }
}
```
```tsx
<h1 className="text-balance">Long title that wraps nicely</h1>
```

Plugin-style (config) with variants support:
```ts
// tailwind.config.ts
import plugin from "tailwindcss/plugin";

plugins: [
  plugin(({ addUtilities }) => {
    addUtilities({
      ".text-balance": { textWrap: "balance" },
      ".content-auto": { contentVisibility: "auto" },
    });
  }),
],
```

## 5. Custom theme values
**Extend `theme` for colors, spacing, fonts, radii, screens, etc.**
```ts
// tailwind.config.ts
theme: {
  extend: {
    colors: { brand: { DEFAULT: "#4f46e5", ink: "#312e81" } },
    spacing: { "18": "4.5rem", "safe": "env(safe-area-inset-bottom)" },
    fontFamily: { display: ["var(--font-playfair)", "serif"] },
    borderRadius: { "4xl": "2rem" },
  },
}
```
```tsx
<div className="p-18 pb-safe rounded-4xl bg-brand text-brand-ink">…</div>
```

## 6. CSS variables
**Drive themes with CSS vars and reference them via arbitrary values `bg-[var(--c)]`.**
```css
:root { --brand: 79 70 229; }
.dark { --brand: 129 140 248; }
```
```tsx
<button className="bg-[rgb(var(--brand))] text-white">…</button>
```
Or wire them into the theme:
```ts
colors: { brand: "rgb(var(--brand) / <alpha-value>)" }
```
```tsx
<button className="bg-brand hover:bg-brand/90">…</button>
```

## 7. Container queries
**Size children based on their parent's width, not the viewport — needs the `@tailwindcss/container-queries` plugin (v3) or native in v4.**
```ts
// tailwind.config.ts
plugins: [require("@tailwindcss/container-queries")],
```
```tsx
<div className="@container">
  <div className="grid grid-cols-1 @sm:grid-cols-2 @lg:grid-cols-3 gap-4">
    …
  </div>
</div>
```
Named containers:
```tsx
<div className="@container/sidebar">
  <div className="@md/sidebar:flex @md/sidebar:gap-4">…</div>
</div>
```

## 8. Advanced responsive layouts
**Stack breakpoints + container queries + arbitrary grid templates for granular layouts.**
```tsx
<section className="grid grid-cols-1 md:grid-cols-[220px_1fr] xl:grid-cols-[260px_1fr_320px] gap-6">
  <aside className="hidden md:block">Nav</aside>
  <main>Content</main>
  <aside className="hidden xl:block">TOC</aside>
</section>
```

## 9. Complex selectors
**Reach into children/siblings with arbitrary variants.**
```tsx
<div className="[&>*+*]:mt-4 [&_p]:leading-relaxed [&_h2+p]:mt-1">…</div>
<a className="peer">…</a>
<button className="peer-checked:[&>svg]:rotate-180">…</button>
```

## 10. Data attributes
**Style on HTML `data-*` via `data-[...]:` — great for state machines and third-party libs.**
```tsx
<div data-state="open" className="data-[state=open]:rotate-180 transition-transform">▾</div>
<div data-active className="data-[active]:bg-indigo-50 data-[active]:text-indigo-700">Tab</div>
```
Combined with `group`/`peer`:
```tsx
<tr data-selected className="group">
  <td className="group-data-[selected]:bg-indigo-50">…</td>
</tr>
```

## 11. Accessibility variants
**Target `aria-*` states and roles for automatic a11y-correct styling.**
```tsx
<button aria-pressed className="aria-pressed:bg-indigo-600 aria-pressed:text-white">
  Toggle
</button>
<div role="tab" aria-selected className="aria-selected:border-b-2 aria-selected:border-indigo-600">
  Tab
</div>
<input aria-invalid className="aria-invalid:border-rose-500 aria-invalid:ring-rose-500/20" />
```
Also: `motion-reduce:`, `motion-safe:`, `contrast-more:`, `contrast-less:`, `forced-colors:`.

## 12. Reduced-motion variants
**Gate animations behind `motion-safe:`; provide a static fallback with `motion-reduce:`.**
```tsx
<div className="motion-safe:animate-bounce motion-reduce:transition-none">
  …
</div>
```
```tsx
<button className="transition-transform hover:scale-105 motion-reduce:hover:scale-100">
  Hover me
</button>
```

## 13. Print styles
**Use `print:` (and `print:hidden`) to control what shows on paper.**
```tsx
<nav className="print:hidden">…</nav>
<button className="print:hidden">Download</button>
<article className="print:text-black print:bg-white">
  Printable content
</article>
```
```css
/* Or a global print baseline */
@media print {
  a::after { content: " (" attr(href) ")"; }
}
```

---

## 🧠 Cheat-sheet

| Need | Syntax |
|---|---|
| Arbitrary value | `w-[420px]`, `text-[13px]`, `bg-[#0f172a]` |
| Arbitrary property | `[mask-type:luminance]`, `[scrollbar-width:thin]` |
| Arbitrary variant | `[&>li]:py-2`, `[&:nth-child(3)]:bg-rose-500` |
| Custom utility | `@layer utilities { .x { … } }` or `plugin()` |
| Custom theme | `theme.extend.{colors,spacing,fontFamily,…}` |
| CSS variable | `bg-[rgb(var(--brand))]` or `colors.brand: "rgb(var(--brand)/<alpha-value>)"` |
| Container query | `@container` + `@sm:` `@md:` `@lg:` (plugin/v4) |
| Named container | `@container/name` + `@md/name:` |
| Complex selector | `[&_a]:underline [&>*+*]:mt-4` |
| Data attribute | `data-[state=open]:`, `group-data-[active]:` |
| ARIA state | `aria-pressed:`, `aria-selected:`, `aria-invalid:` |
| Reduced motion | `motion-safe:`, `motion-reduce:` |
| Print | `print:hidden`, `print:block`, `print:text-black` |

---

## ▶️ One-pager demo: everything in one page

```tsx
// app/page.tsx
export default function Home() {
  return (
    <main className="min-h-screen bg-slate-50 text-slate-800 p-6 sm:p-10 space-y-14 max-w-5xl mx-auto">

      <h1 className="text-3xl sm:text-4xl font-bold tracking-tight text-balance">
        Advanced Tailwind — arbitrary values, variants & extensions
      </h1>

      {/* ── 1 + 2. Arbitrary property + value ── */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Arbitrary properties & values</h2>
        <div className="flex flex-wrap gap-3">
          <div className="w-[220px] h-[88px] rounded-2xl bg-[#4f46e5] text-[13px] text-white
                          grid place-items-center [mask-type:luminance]">
            w-[220px] · bg-[#4f46e5] · text-[13px]
          </div>
          <div className="w-[180px] h-[88px] rounded-2xl bg-white border border-slate-200
                          grid place-items-center [scrollbar-width:thin] text-xs">
            [scrollbar-width:thin]
          </div>
        </div>
      </section>

      {/* ── 3. Arbitrary variants (deep selectors) ── */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Arbitrary variants</h2>
        <ul className="bg-white rounded-2xl border border-slate-200 divide-y divide-slate-100
                       px-5 [&>li]:py-3 [&>li:last-child]:pb-5 [&_a]:text-indigo-600 [&_a:hover]:underline">
          <li>Row one with <a href="#">a link</a></li>
          <li>Row two with <a href="#">another link</a></li>
          <li>Row three — every row styled via <code className="text-xs">[&>li]:py-3</code></li>
        </ul>
      </section>

      {/* ── 4. Custom utilities ── */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Custom utilities</h2>
        <p className="max-w-md text-balance text-slate-700">
          <code className="text-xs">text-balance</code> — a custom utility registered
          with @layer utilities that balances line lengths for nicer headlines.
        </p>
        <div className="overflow-x-auto scrollbar-hide max-w-xs">
          <div className="flex gap-3">
            {Array.from({ length: 12 }).map((_, i) => (
              <span key={i} className="shrink-0 px-3 py-1 rounded-full bg-white border border-slate-200 text-xs">
                chip {i + 1}
              </span>
            ))}
          </div>
        </div>
        <p className="text-xs text-slate-500">
          Scroll horizontally — <code>scrollbar-hide</code> hides the scrollbar.
        </p>
      </section>

      {/* ── 5. Custom theme values ── */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Custom theme values</h2>
        <div className="p-18 pb-safe rounded-4xl bg-brand text-white">
          <p className="font-medium">Custom spacing, radius & color</p>
          <p className="text-xs text-white/80 mt-1">
            <code>p-18 · pb-safe · rounded-4xl · bg-brand</code>
          </p>
        </div>
      </section>

      {/* ── 6. CSS variables ── */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">CSS variables</h2>
        <div className="flex flex-wrap gap-3">
          <button className="px-4 py-2 rounded-lg bg-[rgb(var(--brand))] text-white text-sm font-medium">
            bg-[rgb(var(--brand))]
          </button>
          <button className="px-4 py-2 rounded-lg bg-brand/90 hover:bg-brand text-white text-sm font-medium transition">
            bg-brand/90 (with alpha)
          </button>
        </div>
      </section>

      {/* ── 7 + 8. Container queries + advanced responsive layouts ── */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Container queries</h2>
        <div className="grid grid-cols-1 md:grid-cols-[280px_1fr] gap-6">

          {/* Narrow container — stacks inside itself until it's wide */}
          <div className="@container bg-white rounded-2xl border border-slate-200 p-4">
            <p className="text-xs text-slate-500 mb-2">Sidebar container</p>
            <div className="grid grid-cols-1 @sm:grid-cols-2 gap-3">
              {[1, 2, 3, 4].map((n) => (
                <div key={n} className="rounded-lg bg-slate-100 p-3 text-xs text-center">
                  Item {n}
                </div>
              ))}
            </div>
          </div>

          {/* Wide container — goes 3-up when it has room */}
          <div className="@container bg-white rounded-2xl border border-slate-200 p-4">
            <p className="text-xs text-slate-500 mb-2">Main container</p>
            <div className="grid grid-cols-1 @sm:grid-cols-2 @lg:grid-cols-3 gap-3">
              {[1, 2, 3, 4, 5, 6].map((n) => (
                <div key={n} className="rounded-lg bg-indigo-50 p-3 text-xs text-center">
                  Card {n}
                </div>
              ))}
            </div>
          </div>
        </div>
        <p className="text-xs text-slate-500">
          Resize the page — cards re-flow based on <strong>their parent's width</strong>, not the viewport.
        </p>
      </section>

      {/* ── 9. Complex selectors ── */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Complex selectors</h2>
        <div className="bg-white rounded-2xl border border-slate-200 p-5
                        [&>*+*]:mt-3 [&_h3]:text-base [&_h3]:font-semibold [&_h3+p]:mt-1 [&_p]:text-slate-600">
          <h3>Heading one</h3>
          <p>Paragraph spacing applied via <code className="text-xs">[&_h3+p]:mt-1</code>.</p>
          <h3>Heading two</h3>
          <p>All sibling gaps via <code className="text-xs">[&>*+*]:mt-3</code>.</p>
        </div>
      </section>

      {/* ── 10. Data attributes ── */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Data attributes</h2>
        <details className="group bg-white rounded-2xl border border-slate-200 p-4">
          <summary className="cursor-pointer list-none flex items-center justify-between
                              data-[open]:font-semibold">
            <span>Click to expand</span>
            <span className="transition-transform group-open:rotate-180">▾</span>
          </summary>
          <p className="mt-3 text-sm text-slate-600">
            Styled via <code className="text-xs">group-open:</code> and
            <code className="text-xs"> data-[open]:</code>.
          </p>
        </details>

        <div className="flex gap-2">
          {["one", "two", "three"].map((t, i) => (
            <button
              key={t}
              data-active={i === 0 ? "" : undefined}
              className="px-3 py-1.5 rounded-lg text-sm border border-slate-200 bg-white
                         data-[active]:bg-indigo-50 data-[active]:text-indigo-700 data-[active]:border-indigo-200"
            >
              Tab {t}
            </button>
          ))}
        </div>
      </section>

      {/* ── 11. Accessibility variants ── */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Accessibility variants</h2>

        <button
          aria-pressed="true"
          className="px-4 py-2 rounded-lg border border-slate-300 bg-white text-sm font-medium
                     aria-pressed:bg-indigo-600 aria-pressed:text-white aria-pressed:border-indigo-600
                     transition-colors"
        >
          aria-pressed toggle
        </button>

        <div className="flex gap-2" role="tablist">
          {["Overview", "Analytics"].map((t, i) => (
            <button
              key={t}
              role="tab"
              aria-selected={i === 0}
              className="px-3 py-1.5 text-sm rounded-md
                         aria-selected:bg-slate-900 aria-selected:text-white
                         text-slate-600 hover:bg-slate-100 transition-colors"
            >
              {t}
            </button>
          ))}
        </div>

        <input
          aria-invalid
          defaultValue="bad"
          className="w-full max-w-sm px-3 py-2 rounded-lg border border-slate-300
                     aria-invalid:border-rose-400 aria-invalid:ring-4 aria-invalid:ring-rose-500/15
                     focus:outline-none"
        />
      </section>

      {/* ── 12. Reduced motion ── */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Reduced motion</h2>
        <div className="flex flex-wrap gap-3 items-center">
          <div className="w-12 h-12 rounded-full bg-indigo-500
                          motion-safe:animate-bounce motion-reduce:bg-slate-300"
                          aria-hidden />
          <button className="px-4 py-2 rounded-lg bg-indigo-600 text-white text-sm
                             transition-transform hover:scale-105
                             motion-reduce:hover:scale-100 motion-reduce:transition-none">
            Hover — no motion if reduced
          </button>
          <p className="text-xs text-slate-500">
            Toggle "Reduce motion" in your OS to see the fallback.
          </p>
        </div>
      </section>

      {/* ── 13. Print styles ── */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Print styles</h2>
        <div className="rounded-2xl border border-slate-200 bg-white p-5">
          <div className="flex items-center justify-between print:hidden">
            <p className="text-sm text-slate-500">Interactive controls (hidden on print)</p>
            <button className="px-3 py-1.5 rounded-lg bg-indigo-600 text-white text-xs">
              Download
            </button>
          </div>
          <article className="mt-4 print:mt-0 print:text-black">
            <h3 className="font-semibold">Printable invoice</h3>
            <p className="text-sm text-slate-600 print:text-black mt-1">
              Try <kbd className="px-1 border rounded">⌘P</kbd> / <kbd className="px-1 border rounded">Ctrl+P</kbd>
              — the button and header disappear, this content stays.
            </p>
          </article>
        </div>
      </section>

    </main>
  );
}
```

---

## ⚙️ Required config bits

```ts
// tailwind.config.ts
import type { Config } from "tailwindcss";
import plugin from "tailwindcss/plugin";

const config: Config = {
  darkMode: "class",
  content: ["./app/**/*.{ts,tsx}", "./components/**/*.{ts,tsx}"],
  theme: {
    extend: {
      colors: {
        brand: "rgb(var(--brand) / <alpha-value>)",
      },
      spacing: {
        "18": "4.5rem",
        safe: "env(safe-area-inset-bottom)",
      },
      borderRadius: {
        "4xl": "2rem",
      },
    },
  },
  plugins: [
    require("@tailwindcss/container-queries"),
    plugin(({ addUtilities }) => {
      addUtilities({
        ".text-balance": { textWrap: "balance" },
        ".content-auto": { contentVisibility: "auto" },
      });
    }),
  ],
};

export default config;
```

```css
/* app/globals.css */
@tailwind base;
@tailwind components;
@tailwind utilities;

:root {
  --brand: 79 70 229;      /* indigo-600 */
}
.dark {
  --brand: 129 140 248;    /* indigo-400 */
}

@layer utilities {
  .scrollbar-hide::-webkit-scrollbar { display: none; }
  .scrollbar-hide { scrollbar-width: none; }
}

@media print {
  a::after { content: " (" attr(href) ")"; }
}
```

Install the container-queries plugin:
```bash
npm install -D @tailwindcss/container-queries
```

---

## ✅ Coverage checklist

| Concept | Where |
|---|---|
| Arbitrary properties | `[mask-type:luminance]`, `[scrollbar-width:thin]` |
| Arbitrary values | `w-[220px]`, `bg-[#4f46e5]`, `text-[13px]` |
| Arbitrary variants | `[&>li]:py-3`, `[&_a:hover]:underline` |
| Custom utilities | `text-balance`, `scrollbar-hide` |
| Custom theme values | `p-18`, `pb-safe`, `rounded-4xl`, `bg-brand` |
| CSS variables | `--brand` + `bg-[rgb(var(--brand))]` |
| Container queries | `@container` + `@sm:` / `@lg:` |
| Advanced responsive layouts | `grid-cols-[280px_1fr]` |
| Complex selectors | `[&>*+*]`, `[&_h3+p]` |
| Data attributes | `data-[active]:`, `group-open:` |
| Accessibility variants | `aria-pressed:`, `aria-selected:`, `aria-invalid:` |
| Reduced-motion variants | `motion-safe:`, `motion-reduce:` |
| Print styles | `print:hidden`, `print:text-black` |

---
