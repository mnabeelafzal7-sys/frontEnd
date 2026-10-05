# Tailwind Color System

## 1. Tailwind color system
**Each color has 11 shades (`50` lightest → `950` darkest) — pick by lightness, not guess.**
```tsx
<div className="bg-indigo-50 text-indigo-900">...</div>
```

## 2. Background colors
**Use `bg-{color}-{shade}` on any element.**
```tsx
<div className="bg-emerald-500">...</div>
```

## 3. Text colors
**Use `text-{color}-{shade}`.**
```tsx
<p className="text-rose-600">Error text</p>
```

## 4. Border colors
**Use `border-{color}-{shade}` alongside a width (`border`).**
```tsx
<div className="border border-slate-300">...</div>
```

## 5. Ring colors
**Use `ring-{color}-{shade}` with `ring-2` for focus/outline effects.**
```tsx
<input className="ring-2 ring-indigo-500 focus:ring-indigo-600" />
```

## 6. Opacity
**Use `opacity-{0..100}` on the element, or `/xx` on a color for background alpha.**
```tsx
<div className="bg-black/50 text-white/90">overlay</div>
```

## 7. Color combinations
**Pair a light bg + dark text + mid-tone border from the same family for harmony.**
```tsx
<div className="bg-indigo-50 text-indigo-900 border border-indigo-200">...</div>
```

## 8. Neutral color palettes
**Use `slate`, `gray`, `zinc`, `neutral`, or `stone` for UI chrome.**
```tsx
<div className="bg-white text-slate-800 border-slate-200">card</div>
```

## 9. Brand color palettes
**Pick one hue (e.g. `indigo`) and use it consistently for CTAs, links, focus rings.**
```tsx
<button className="bg-indigo-600 text-white hover:bg-indigo-700 ring-2 ring-indigo-500/40">…</button>
```

## 10. Dark color palettes
**Invert: dark bg, light text, desaturated borders.**
```tsx
<div className="bg-slate-900 text-slate-100 border border-slate-700">...</div>
```

## 11. Gradient backgrounds
**Use `bg-gradient-to-{dir}` + `from-*` + `to-*`.**
```tsx
<div className="bg-gradient-to-r from-indigo-500 to-purple-500">...</div>
```

## 12. Gradient text
**Add `bg-clip-text text-transparent` to a gradient background.**
```tsx
<h1 className="bg-gradient-to-r from-indigo-600 to-pink-600 bg-clip-text text-transparent">
  Gradient
</h1>
```

## 13. Multi-color gradients
**Add `via-*` between `from-*` and `to-*` for three-stop gradients.**
```tsx
<div className="bg-gradient-to-r from-rose-500 via-amber-400 to-emerald-500">...</div>
```

## 14. Hover color changes
**Prefix color utilities with `hover:` for state changes.**
```tsx
<button className="bg-slate-800 hover:bg-slate-700 text-white">Hover me</button>
```

---

## 🧠 Shade cheat-sheet

| Shade | Use for |
|---|---|
| `50` | Page background tints, subtle highlights |
| `100` | Hover backgrounds, badges |
| `200` | Borders, dividers |
| `300` | Disabled text, muted borders |
| `400` | Placeholder text, icons |
| `500` | Primary brand color |
| `600` | Primary buttons, links |
| `700` | Hover on primary buttons |
| `800` | Headings on dark UI |
| `900` | Dark backgrounds, dark headings |
| `950` | Near-black, dark mode surfaces |

---

## 🎨 Palette cheat-sheet

| Family | Vibe |
|---|---|
| `slate` | Cool neutral (default in Tailwind UI) |
| `gray` | True neutral |
| `zinc` | Slightly cool neutral |
| `neutral` | Pure neutral |
| `stone` | Warm neutral |
| `indigo` / `violet` / `purple` | Brand / SaaS |
| `emerald` / `teal` | Success / finance |
| `rose` / `red` | Error / destructive |
| `amber` / `yellow` | Warning |
| `sky` / `blue` | Info |

---

## ▶️ One-pager demo: every concept on one page

```tsx
// app/page.tsx
export default function Home() {
  return (
    <main className="min-h-screen bg-slate-50 text-slate-800 p-6 sm:p-10 space-y-10">

      {/* 1 + 12. Gradient text heading */}
      <h1 className="text-3xl sm:text-5xl font-bold tracking-tight bg-gradient-to-r from-indigo-600 via-purple-600 to-pink-600 bg-clip-text text-transparent">
        Tailwind Color System
      </h1>

      {/* 2, 3, 4, 8. Neutral card with bg / text / border */}
      <section className="bg-white text-slate-800 border border-slate-200 rounded-2xl p-6 shadow-sm">
        <h2 className="text-xl font-semibold mb-2">Neutral card</h2>
        <p className="text-slate-600 text-sm leading-relaxed">
          Built from the <span className="font-mono text-slate-900">slate</span> family — clean,
          cool, and easy on the eyes.
        </p>
      </section>

      {/* 9. Brand palette — primary button with hover + ring focus */}
      <section className="flex flex-wrap gap-3">
        <button className="px-4 py-2 rounded-lg bg-indigo-600 text-white font-medium hover:bg-indigo-700 ring-2 ring-indigo-500/40 ring-offset-2 transition">
          Primary
        </button>
        <button className="px-4 py-2 rounded-lg bg-slate-800 text-white font-medium hover:bg-slate-700 transition">
          Secondary
        </button>
        <button className="px-4 py-2 rounded-lg bg-emerald-600 text-white font-medium hover:bg-emerald-700 transition">
          Success
        </button>
        <button className="px-4 py-2 rounded-lg bg-rose-600 text-white font-medium hover:bg-rose-700 transition">
          Danger
        </button>
      </section>

      {/* 7. Color combinations — tinted badges */}
      <section className="flex flex-wrap gap-2">
        <span className="bg-indigo-50 text-indigo-700 border border-indigo-200 px-3 py-1 rounded-full text-xs font-medium">Indigo</span>
        <span className="bg-emerald-50 text-emerald-700 border border-emerald-200 px-3 py-1 rounded-full text-xs font-medium">Emerald</span>
        <span className="bg-amber-50 text-amber-700 border border-amber-200 px-3 py-1 rounded-full text-xs font-medium">Amber</span>
        <span className="bg-rose-50 text-rose-700 border border-rose-200 px-3 py-1 rounded-full text-xs font-medium">Rose</span>
      </section>

      {/* 6. Opacity — overlay demo */}
      <section className="relative h-40 rounded-2xl overflow-hidden bg-gradient-to-br from-indigo-500 to-purple-600">
        <div className="absolute inset-0 bg-black/40" />
        <div className="relative h-full flex flex-col items-center justify-center text-white/90 space-y-1">
          <p className="text-lg font-semibold">bg-black/40 overlay</p>
          <p className="text-sm text-white/70">text-white/70 for muted copy</p>
        </div>
      </section>

      {/* 11. Gradient background */}
      <section className="bg-gradient-to-r from-sky-500 to-indigo-600 text-white rounded-2xl p-6">
        <h2 className="text-lg font-semibold">Simple gradient</h2>
        <p className="text-white/80 text-sm mt-1">from-sky-500 → to-indigo-600</p>
      </section>

      {/* 13. Multi-color gradient */}
      <section className="bg-gradient-to-r from-rose-500 via-amber-400 to-emerald-500 text-white rounded-2xl p-6">
        <h2 className="text-lg font-semibold">Multi-color gradient</h2>
        <p className="text-white/90 text-sm mt-1">rose → amber → emerald</p>
      </section>

      {/* 10. Dark palette card */}
      <section className="bg-slate-900 text-slate-100 border border-slate-700 rounded-2xl p-6">
        <h2 className="text-lg font-semibold">Dark card</h2>
        <p className="text-slate-400 text-sm mt-1 leading-relaxed">
          Dark surfaces use <span className="font-mono text-slate-200">slate-900</span> with
          <span className="font-mono text-slate-200"> slate-400</span> for muted text.
        </p>
        <button className="mt-4 px-4 py-2 rounded-lg bg-indigo-500 text-white text-sm font-medium hover:bg-indigo-400 transition">
          Action
        </button>
      </section>

      {/* 5. Ring colors — focus input */}
      <section className="bg-white border border-slate-200 rounded-2xl p-6 space-y-3">
        <label className="text-sm font-medium text-slate-700">Email</label>
        <input
          type="email"
          placeholder="you@example.com"
          className="w-full px-3 py-2 rounded-lg border border-slate-300 placeholder:text-slate-400
                     focus:outline-none focus:border-indigo-500 focus:ring-2 focus:ring-indigo-500/40"
        />
        <p className="text-xs text-slate-500">
          Ring on focus uses <code className="text-indigo-700 bg-indigo-50 px-1 rounded">ring-indigo-500/40</code>
        </p>
      </section>

      {/* 14. Hover color changes — link */}
      <p className="text-slate-600">
        Read the{" "}
        <a href="#" className="text-indigo-600 hover:text-indigo-800 underline underline-offset-4 transition-colors">
          full guide
        </a>
        .
      </p>

    </main>
  );
}
```

---

## ✅ Coverage checklist

| Concept | Where in demo |
|---|---|
| Color system | Whole page uses shade scale (`50 → 900`) |
| Background colors | Every card + buttons |
| Text colors | `text-slate-*`, `text-indigo-*`, etc. |
| Border colors | `border-slate-200`, `border-indigo-200` |
| Ring colors | Input focus + primary button focus |
| Opacity | `bg-black/40`, `text-white/70` |
| Color combinations | Tinted badges (bg-50 / text-700 / border-200) |
| Neutral palettes | Slate cards + dark card |
| Brand palettes | Indigo primary buttons/links |
| Dark palettes | `bg-slate-900 text-slate-100 border-slate-700` |
| Gradient background | Simple two-stop + hero dark |
| Gradient text | H1 with `bg-clip-text text-transparent` |
| Multi-color gradients | rose → amber → emerald banner |
| Hover color changes | Buttons, links, `hover:bg-*-700` |

---
5. **Contrast audit** — pair `text-*-700` on `bg-*-50` for WCAG AA.

Want me to fold this into your GitHub profile repo as a `/colors` route with a README that mirrors the palette + shade cheat-sheets above?
