# Borders, Radius & Shadows

## 1. Border width
**Use `border-{0|2|4|8}` (or `border` = 1px) to set border thickness.**
```tsx
<div className="border border-slate-300">1px</div>
<div className="border-2 border-slate-300">2px</div>
```

## 2. Individual borders
**Target one side with `border-t/r/b/l` + width.**
```tsx
<div className="border-t border-slate-200">top only</div>
<div className="border-l-4 border-indigo-500 pl-4">left accent</div>
```

## 3. Border styles
**Use `border-solid` (default), `border-dashed`, `border-dotted`, `border-double`, `border-none`.**
```tsx
<div className="border-2 border-dashed border-slate-300">dashed</div>
```

## 4. Border radius
**Use `rounded-{none|sm|md|lg|xl|2xl|3xl|full}`.**
```tsx
<div className="rounded-lg">8px</div>
<div className="rounded-2xl">16px</div>
```

## 5. Rounded cards
**Use `rounded-2xl` (or `rounded-3xl` for hero cards) + `border` + `shadow-sm`.**
```tsx
<div className="rounded-2xl border border-slate-200 bg-white shadow-sm p-6">Card</div>
```

## 6. Rounded buttons
**Use `rounded-lg` (or `rounded-full` for pill buttons) + padding.**
```tsx
<button className="rounded-lg px-4 py-2 bg-indigo-600 text-white">Button</button>
<button className="rounded-full px-4 py-2 bg-slate-900 text-white">Pill</button>
```

## 7. Circular elements
**Use `rounded-full` + equal `w-*` and `h-*` (or `aspect-square`).**
```tsx
<img className="w-12 h-12 rounded-full object-cover" src="..." />
<div className="w-3 h-3 rounded-full bg-emerald-500" /> {/* status dot */}
```

## 8. Shadows
**Use `shadow-{sm|DEFAULT|md|lg|xl|2xl|inner|none}` to lift elements.**
```tsx
<div className="shadow-sm">subtle</div>
<div className="shadow-lg">prominent</div>
<div className="shadow-inner">inset</div>
```

## 9. Custom shadows
**Extend `theme.boxShadow` with named tokens.**
```ts
// tailwind.config.ts
theme: {
  extend: {
    boxShadow: {
      card: "0 1px 2px rgba(15,23,42,.04), 0 8px 24px -8px rgba(15,23,42,.08)",
      glow: "0 0 0 4px rgba(99,102,241,.25)",
    },
  },
}
```
```tsx
<div className="shadow-card">Soft card</div>
```

## 10. Rings
**Use `ring-{width}` + `ring-{color}` to draw an outline that doesn't affect layout.**
```tsx
<div className="ring-2 ring-indigo-500 rounded-lg p-4">Ringing</div>
```

## 11. Focus rings
**Use `focus:ring-2 focus:ring-indigo-500/40 focus:outline-none` on inputs/buttons.**
```tsx
<input className="rounded-lg border border-slate-300 focus:outline-none focus:ring-2 focus:ring-indigo-500/40 focus:border-indigo-500" />
```
Add `focus-visible:ring-*` to only show on keyboard focus:
```tsx
<button className="focus-visible:ring-2 focus-visible:ring-indigo-500 focus-visible:outline-none">
  Keyboard-friendly
</button>
```

## 12. Divide utilities
**Add borders between children with `divide-{x|y}` + `divide-{color}` + optional width.**
```tsx
<ul className="divide-y divide-slate-200">
  <li className="py-3">One</li>
  <li className="py-3">Two</li>
</ul>
```

## 13. Border opacity
**Suffix the color with `/xx` for translucent borders — great for dark UIs.**
```tsx
<div className="border border-white/20 bg-white/5">Glass card</div>
```

---

## 🧠 Quick reference

| Need | Classes |
|---|---|
| Hairline card | `rounded-2xl border border-slate-200 shadow-sm` |
| Elevated card | `rounded-2xl border border-slate-200 shadow-md` |
| Pill button | `rounded-full px-5 py-2 bg-indigo-600 text-white` |
| Avatar | `w-12 h-12 rounded-full object-cover` |
| Status dot | `w-2.5 h-2.5 rounded-full bg-emerald-500` |
| Left accent | `border-l-4 border-indigo-500 pl-4` |
| Divider list | `divide-y divide-slate-200` |
| Input focus | `focus:outline-none focus:ring-2 focus:ring-indigo-500/40 focus:border-indigo-500` |
| Glass panel | `border border-white/20 bg-white/5 backdrop-blur` |
| Soft custom shadow | `shadow-card` (extended token) |

---

## ▶️ One-pager demo: every concept in one page

```tsx
// app/page.tsx
export default function Home() {
  return (
    <main className="min-h-screen bg-slate-50 text-slate-800 p-6 sm:p-10 space-y-10">

      <h1 className="text-3xl sm:text-4xl font-bold tracking-tight">
        Borders, Radius & Shadows
      </h1>

      {/* 1 + 4. Border widths + radius */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Border widths</h2>
        <div className="flex flex-wrap gap-3">
          <div className="border border-slate-300 rounded-md px-4 py-2 text-sm">1px</div>
          <div className="border-2 border-slate-300 rounded-md px-4 py-2 text-sm">2px</div>
          <div className="border-4 border-slate-300 rounded-md px-4 py-2 text-sm">4px</div>
          <div className="border-8 border-slate-300 rounded-md px-4 py-2 text-sm">8px</div>
        </div>
      </section>

      {/* 2. Individual borders */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Individual borders</h2>
        <div className="bg-white rounded-lg border-t border-slate-200 p-4 text-sm">
          Only a top border
        </div>
        <div className="bg-white rounded-lg border-l-4 border-indigo-500 pl-4 py-3 text-sm">
          Left accent bar
        </div>
      </section>

      {/* 3. Border styles */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Border styles</h2>
        <div className="grid grid-cols-2 sm:grid-cols-4 gap-3 text-xs text-center">
          <div className="border-2 border-solid border-slate-400 rounded-lg p-3">solid</div>
          <div className="border-2 border-dashed border-slate-400 rounded-lg p-3">dashed</div>
          <div className="border-2 border-dotted border-slate-400 rounded-lg p-3">dotted</div>
          <div className="border-4 border-double border-slate-400 rounded-lg p-3">double</div>
        </div>
      </section>

      {/* 4. Border radius scale */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Radius scale</h2>
        <div className="flex flex-wrap gap-3 text-xs">
          <div className="bg-indigo-100 px-4 py-2 rounded-none">none</div>
          <div className="bg-indigo-100 px-4 py-2 rounded-sm">sm</div>
          <div className="bg-indigo-100 px-4 py-2 rounded-md">md</div>
          <div className="bg-indigo-100 px-4 py-2 rounded-lg">lg</div>
          <div className="bg-indigo-100 px-4 py-2 rounded-xl">xl</div>
          <div className="bg-indigo-100 px-4 py-2 rounded-2xl">2xl</div>
          <div className="bg-indigo-100 px-4 py-2 rounded-full">full</div>
        </div>
      </section>

      {/* 5. Rounded cards */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Rounded cards</h2>
        <div className="grid grid-cols-1 sm:grid-cols-2 gap-4">
          <div className="rounded-2xl border border-slate-200 bg-white shadow-sm p-6">
            <h3 className="font-semibold">Soft card</h3>
            <p className="text-sm text-slate-600 mt-1">rounded-2xl + border + shadow-sm</p>
          </div>
          <div className="rounded-2xl border border-slate-200 bg-white shadow-md p-6">
            <h3 className="font-semibold">Elevated card</h3>
            <p className="text-sm text-slate-600 mt-1">rounded-2xl + border + shadow-md</p>
          </div>
        </div>
      </section>

      {/* 6. Rounded buttons */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Rounded buttons</h2>
        <div className="flex flex-wrap gap-3">
          <button className="rounded-md px-4 py-2 bg-indigo-600 text-white text-sm font-medium hover:bg-indigo-700">rounded-md</button>
          <button className="rounded-lg px-4 py-2 bg-indigo-600 text-white text-sm font-medium hover:bg-indigo-700">rounded-lg</button>
          <button className="rounded-xl px-4 py-2 bg-indigo-600 text-white text-sm font-medium hover:bg-indigo-700">rounded-xl</button>
          <button className="rounded-full px-5 py-2 bg-slate-900 text-white text-sm font-medium hover:bg-slate-800">pill</button>
        </div>
      </section>

      {/* 7. Circular elements */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Circular elements</h2>
        <div className="flex items-center gap-4">
          <img
            src="https://i.pravatar.cc/96?img=12"
            alt="avatar"
            className="w-16 h-16 rounded-full object-cover ring-2 ring-white shadow-md"
          />
          <div className="flex items-center gap-2 text-sm">
            <span className="w-2.5 h-2.5 rounded-full bg-emerald-500" /> online
            <span className="w-2.5 h-2.5 rounded-full bg-amber-500" /> away
            <span className="w-2.5 h-2.5 rounded-full bg-slate-300" /> offline
          </div>
        </div>
      </section>

      {/* 8. Shadows scale */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Shadow scale</h2>
        <div className="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-6 gap-4">
          {["shadow-sm", "shadow", "shadow-md", "shadow-lg", "shadow-xl", "shadow-2xl"].map((s) => (
            <div key={s} className={`bg-white rounded-xl p-4 text-center text-xs ${s}`}>{s}</div>
          ))}
        </div>
      </section>

      {/* 9. Custom shadow */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Custom shadow</h2>
        <div className="rounded-2xl bg-white p-6 shadow-card border border-slate-200">
          Uses <code className="text-indigo-700 bg-indigo-50 px-1 rounded">shadow-card</code> from the Tailwind config.
        </div>
      </section>

      {/* 10 + 11. Rings + focus rings */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Rings & focus rings</h2>

        <div className="rounded-xl ring-2 ring-indigo-500 p-4 bg-white text-sm">ring-2 ring-indigo-500</div>
        <div className="rounded-xl ring-4 ring-emerald-400/50 p-4 bg-white text-sm">ring-4 ring-emerald-400/50</div>

        <input
          type="email"
          placeholder="Focus me with Tab / click"
          className="w-full max-w-md px-3 py-2 rounded-lg border border-slate-300
                     placeholder:text-slate-400
                     focus:outline-none focus:border-indigo-500 focus:ring-2 focus:ring-indigo-500/40"
        />

        <button className="rounded-lg px-4 py-2 bg-indigo-600 text-white text-sm font-medium
                           focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-indigo-500 focus-visible:ring-offset-2">
          Keyboard focus ring
        </button>
      </section>

      {/* 12. Divide utilities */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Divide utilities</h2>

        <ul className="divide-y divide-slate-200 bg-white rounded-2xl border border-slate-200 px-4">
          <li className="py-3 text-sm">Item one</li>
          <li className="py-3 text-sm">Item two</li>
          <li className="py-3 text-sm">Item three</li>
        </ul>

        <div className="flex divide-x divide-slate-200 bg-white rounded-2xl border border-slate-200">
          <div className="flex-1 p-4 text-sm text-center">Column A</div>
          <div className="flex-1 p-4 text-sm text-center">Column B</div>
          <div className="flex-1 p-4 text-sm text-center">Column C</div>
        </div>
      </section>

      {/* 13. Border opacity — glass card */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Border opacity / glass</h2>
        <div className="rounded-2xl p-8 bg-gradient-to-br from-indigo-500 to-purple-600">
          <div className="rounded-2xl border border-white/20 bg-white/10 backdrop-blur p-6 text-white">
            <p className="font-semibold">Glass card</p>
            <p className="text-sm text-white/70 mt-1">
              border-white/20 · bg-white/10 · backdrop-blur
            </p>
          </div>
        </div>
      </section>

    </main>
  );
}
```

---

## ⚙️ Add custom shadows to `tailwind.config.ts`

```ts
import type { Config } from "tailwindcss";

const config: Config = {
  content: ["./app/**/*.{ts,tsx}", "./components/**/*.{ts,tsx}"],
  theme: {
    extend: {
      boxShadow: {
        card:  "0 1px 2px rgba(15,23,42,.04), 0 8px 24px -8px rgba(15,23,42,.08)",
        glow:  "0 0 0 4px rgba(99,102,241,.25)",
        inset: "inset 0 1px 2px rgba(15,23,42,.06)",
      },
    },
  },
  plugins: [],
};

export default config;
```

---

## ✅ Coverage checklist

| Concept | Where |
|---|---|
| Border width | 1 / 2 / 4 / 8px row |
| Individual borders | `border-t`, `border-l-4` |
| Border styles | solid / dashed / dotted / double |
| Border radius | Full scale demo |
| Rounded cards | `rounded-2xl border shadow-sm/md` |
| Rounded buttons | `rounded-md/lg/xl/full` |
| Circular elements | Avatar + status dots |
| Shadows | Full scale row |
| Custom shadows | `shadow-card` from config |
| Rings | `ring-2`, `ring-4 ring-*/50` |
| Focus rings | Input + `focus-visible:` button |
| Divide utilities | `divide-y` list + `divide-x` row |
| Border opacity | `border-white/20` glass card |

---
5. **Dark mode borders** — `dark:border-slate-700` + `dark:divide-slate-800`.

Want me to fold this into your GitHub profile repo as a `/borders` route with a README section that mirrors the reference table above?
