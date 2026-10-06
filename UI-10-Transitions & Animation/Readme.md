# Transitions, Transforms & Animations

## 1. `transition`
**Enables smooth transitions on a curated set of properties (colors, opacity, shadow, transform).**
```tsx
<button className="transition hover:bg-indigo-700">Hover</button>
```

## 2. `transition-colors`
**Transitions color, background-color, border-color, text-decoration-color, fill, stroke.**
```tsx
<a className="transition-colors hover:text-indigo-600">Link</a>
```

## 3. `transition-transform`
**Transitions transform properties (scale, rotate, translate, skew).**
```tsx
<div className="transition-transform hover:scale-105">Zoom</div>
```

## 4. `transition-opacity`
**Transitions opacity — perfect for fades.**
```tsx
<div className="opacity-0 transition-opacity hover:opacity-100">Fade in</div>
```

## 5. Duration
**Use `duration-{75|100|150|200|300|500|700|1000}` to set transition time.**
```tsx
<div className="transition duration-300 hover:scale-105">300ms</div>
```

## 6. Delay
**Use `delay-{ms}` to wait before starting.**
```tsx
<div className="transition delay-150 duration-300 hover:scale-105">Delayed</div>
```

## 7. Easing
**Use `ease-linear`, `ease-in`, `ease-out`, `ease-in-out` (or custom `ease-[cubic-bezier(...)]`).**
```tsx
<div className="transition ease-out hover:-translate-y-1">Smooth</div>
```

## 8. Transform
**Apply transforms via utilities — combine multiple in one class list.**
```tsx
<div className="scale-105 rotate-3 translate-x-2">...</div>
```

## 9. Scale
**Use `scale-{0|50|75|90|95|100|105|110|125|150}` or axis-specific `scale-x-*`, `scale-y-*`.**
```tsx
<img className="hover:scale-110 transition-transform" />
```

## 10. Rotate
**Use `rotate-{0|1|2|3|6|12|45|90|180}` or negative `-rotate-45`.**
```tsx
<div className="rotate-45">Diamond</div>
```

## 11. Translate
**Use `translate-x-{n}` / `translate-y-{n}` / negative values.**
```tsx
<div className="group-hover:translate-x-1 transition-transform">→</div>
```

## 12. Skew
**Use `skew-x-{n}` / `skew-y-{n}` for a slanted look.**
```tsx
<div className="skew-y-3">Skewed</div>
```

## 13. Built-in animations
**Use `animate-{spin|ping|pulse|bounce|none}` for common keyframe animations.**
```tsx
<div className="animate-spin">⟳</div>
<div className="animate-pulse">Loading…</div>
<div className="animate-bounce">↓</div>
<div className="animate-ping">•</div>
```

## 14. Custom animations
**Extend `theme.animation` + `theme.keyframes` in the config.**
```ts
// tailwind.config.ts
theme: {
  extend: {
    animation: {
      "fade-up": "fadeUp .6s ease-out both",
      "float":   "float 6s ease-in-out infinite",
      "shimmer": "shimmer 2s linear infinite",
    },
    keyframes: {
      fadeUp: {
        "0%":   { opacity: "0", transform: "translateY(16px)" },
        "100%": { opacity: "1", transform: "translateY(0)" },
      },
      float: {
        "0%, 100%": { transform: "translateY(0)" },
        "50%":      { transform: "translateY(-10px)" },
      },
      shimmer: {
        "0%":   { backgroundPosition: "-200% 0" },
        "100%": { backgroundPosition: "200% 0" },
      },
    },
  },
}
```
```tsx
<div className="animate-fade-up">Fades in</div>
<div className="animate-float">Floats</div>
```

---

## 🧠 Quick reference

| Need | Classes |
|---|---|
| Generic smooth state | `transition duration-200 ease-out` |
| Color-only | `transition-colors duration-200` |
| Transform-only | `transition-transform duration-300` |
| Fade-in | `opacity-0 group-hover:opacity-100 transition-opacity duration-300` |
| Lift on hover | `transition-transform hover:-translate-y-1` |
| Zoom on hover | `transition-transform hover:scale-105` |
| Spinner | `animate-spin` (use `motion-safe:`) |
| Skeleton | `animate-pulse bg-slate-200` |
| Online dot | `animate-ping` (as an absolutely positioned halo) |
| Bouncing arrow | `animate-bounce` |
| Custom entrance | `animate-fade-up` via config |

---

## ▶️ One-pager demo: every concept in one page

```tsx
// app/page.tsx
export default function Home() {
  return (
    <main className="min-h-screen bg-slate-50 text-slate-800 p-6 sm:p-10 space-y-14 max-w-5xl mx-auto">

      <h1 className="text-3xl sm:text-4xl font-bold tracking-tight">
        Transitions, Transforms & Animations
      </h1>

      {/* ── 1. transition (default) ── */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">transition</h2>
        <button className="px-4 py-2 rounded-lg bg-indigo-600 text-white font-medium
                           transition hover:bg-indigo-700 hover:shadow-lg">
          Hover me
        </button>
      </section>

      {/* ── 2. transition-colors ── */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">transition-colors</h2>
        <a href="#" className="text-slate-700 font-medium
                                transition-colors duration-300
                                hover:text-indigo-600">
          Color-only transition
        </a>
      </section>

      {/* ── 3 + 5. transition-transform + duration ── */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">transition-transform + duration</h2>
        <div className="flex flex-wrap gap-4">
          {[
            { label: "duration-150", cls: "duration-150" },
            { label: "duration-300", cls: "duration-300" },
            { label: "duration-700", cls: "duration-700" },
          ].map((d) => (
            <div
              key={d.label}
              className={`w-32 h-24 rounded-xl bg-white border border-slate-200 grid place-items-center text-xs
                          transition-transform ${d.cls} ease-out
                          hover:scale-110 hover:shadow-lg`}
            >
              {d.label}
            </div>
          ))}
        </div>
      </section>

      {/* ── 4. transition-opacity ── */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">transition-opacity</h2>
        <div className="group relative w-full max-w-sm h-40 rounded-2xl overflow-hidden bg-slate-900">
          <img
            src="https://picsum.photos/seed/fade/800/400"
            alt=""
            className="absolute inset-0 w-full h-full object-cover
                       opacity-100 group-hover:opacity-60
                       transition-opacity duration-500"
          />
          <div className="absolute inset-0 grid place-items-center text-white
                          opacity-0 group-hover:opacity-100
                          transition-opacity duration-500 delay-100">
            <p className="font-semibold">Hover to reveal</p>
          </div>
        </div>
      </section>

      {/* ── 6. Delay ── */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Delay</h2>
        <div className="flex gap-3">
          {[0, 100, 200, 300].map((d) => (
            <button
              key={d}
              className="px-4 py-2 rounded-lg bg-slate-900 text-white text-sm
                         transition-transform duration-300 ease-out
                         hover:-translate-y-2"
              style={{ transitionDelay: `${d}ms` }}
            >
              delay-{d}
            </button>
          ))}
        </div>
      </section>

      {/* ── 7. Easing ── */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Easing</h2>
        <div className="flex flex-wrap gap-3">
          {["ease-linear", "ease-in", "ease-out", "ease-in-out"].map((e) => (
            <div
              key={e}
              className={`px-4 py-2 rounded-lg bg-white border border-slate-200 text-xs
                          transition-transform duration-500 ${e}
                          hover:translate-x-4`}
            >
              {e}
            </div>
          ))}
        </div>
      </section>

      {/* ── 8 + 9 + 10 + 11 + 12. Transform utilities ── */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Transforms</h2>
        <div className="flex flex-wrap gap-4">
          <div className="w-24 h-24 rounded-xl bg-indigo-100 grid place-items-center text-xs
                          transition-transform hover:scale-110">
            scale
          </div>
          <div className="w-24 h-24 rounded-xl bg-emerald-100 grid place-items-center text-xs
                          transition-transform hover:rotate-12">
            rotate
          </div>
          <div className="w-24 h-24 rounded-xl bg-amber-100 grid place-items-center text-xs
                          transition-transform hover:translate-x-3 hover:-translate-y-2">
            translate
          </div>
          <div className="w-24 h-24 rounded-xl bg-rose-100 grid place-items-center text-xs
                          transition-transform hover:skew-y-6">
            skew
          </div>
          <div className="w-24 h-24 rounded-xl bg-purple-100 grid place-items-center text-xs
                          transition-transform hover:scale-110 hover:rotate-6 hover:shadow-xl">
            combo
          </div>
        </div>
      </section>

      {/* ── 13. Built-in animations ── */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Built-in animations</h2>
        <div className="flex flex-wrap gap-6 items-center">

          <div className="text-center space-y-2">
            <div className="w-12 h-12 rounded-full border-4 border-indigo-500 border-t-transparent
                            animate-spin mx-auto" />
            <p className="text-xs text-slate-500">animate-spin</p>
          </div>

          <div className="text-center space-y-2">
            <div className="w-12 h-12 rounded-full bg-indigo-200 animate-pulse mx-auto" />
            <p className="text-xs text-slate-500">animate-pulse</p>
          </div>

          <div className="text-center space-y-2">
            <div className="text-3xl animate-bounce">↓</div>
            <p className="text-xs text-slate-500">animate-bounce</p>
          </div>

          <div className="text-center space-y-2">
            <div className="relative w-3 h-3 mx-auto">
              <span className="absolute inset-0 rounded-full bg-emerald-400 animate-ping" />
              <span className="relative block w-3 h-3 rounded-full bg-emerald-500" />
            </div>
            <p className="text-xs text-slate-500">animate-ping</p>
          </div>

          <div className="text-center space-y-2">
            <div className="w-32 h-4 rounded-full bg-slate-200 overflow-hidden">
              <div className="h-full w-1/2 bg-indigo-500 animate-pulse" />
            </div>
            <p className="text-xs text-slate-500">skeleton bar</p>
          </div>

        </div>
      </section>

      {/* ── 14. Custom animations ── */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Custom animations</h2>
        <div className="flex flex-wrap gap-6 items-center">

          <div className="w-40 h-20 rounded-xl bg-white border border-slate-200 shadow-sm
                          grid place-items-center text-xs animate-fade-up">
            animate-fade-up
          </div>

          <div className="w-40 h-20 rounded-xl bg-gradient-to-br from-indigo-500 to-purple-500
                          text-white grid place-items-center text-xs animate-float">
            animate-float
          </div>

          <div className="w-40 h-20 rounded-xl overflow-hidden bg-slate-200
                          bg-[linear-gradient(90deg,#e2e8f0_25%,#f1f5f9_50%,#e2e8f0_75%)]
                          bg-[length:200%_100%] animate-shimmer" />

        </div>
      </section>

      {/* ── Combo: card hover ── */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Combined: card hover</h2>
        <a href="#" className="group block w-full max-w-sm rounded-2xl overflow-hidden bg-white
                               border border-slate-200 shadow-sm
                               transition-all duration-300 ease-out
                               hover:-translate-y-1.5 hover:shadow-2xl">
          <div className="overflow-hidden">
            <img
              src="https://picsum.photos/seed/card/800/500"
              alt=""
              className="w-full h-48 object-cover
                         transition-transform duration-700 ease-out
                         group-hover:scale-110"
            />
          </div>
          <div className="p-5">
            <h3 className="font-semibold transition-colors group-hover:text-indigo-600">
              Everything together
            </h3>
            <span className="inline-flex items-center gap-1 text-sm text-indigo-600
                             opacity-0 translate-y-1
                             transition-all duration-300
                             group-hover:opacity-100 group-hover:translate-y-0">
              Read more →
            </span>
          </div>
        </a>
      </section>

    </main>
  );
}
```

---

## ⚙️ Config for the custom animations used above

```ts
// tailwind.config.ts
import type { Config } from "tailwindcss";

const config: Config = {
  content: ["./app/**/*.{ts,tsx}", "./components/**/*.{ts,tsx}"],
  theme: {
    extend: {
      animation: {
        "fade-up": "fadeUp .6s ease-out both",
        "float":   "float 6s ease-in-out infinite",
        "shimmer": "shimmer 2s linear infinite",
      },
      keyframes: {
        fadeUp: {
          "0%":   { opacity: "0", transform: "translateY(16px)" },
          "100%": { opacity: "1", transform: "translateY(0)" },
        },
        float: {
          "0%, 100%": { transform: "translateY(0)" },
          "50%":      { transform: "translateY(-10px)" },
        },
        shimmer: {
          "0%":   { backgroundPosition: "-200% 0" },
          "100%": { backgroundPosition: "200% 0" },
        },
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
| `transition` | Buttons, cards |
| `transition-colors` | Text link |
| `transition-transform` | Scale/duration demo + transforms row |
| `transition-opacity` | Image fade reveal |
| Duration | 150 / 300 / 700 comparison |
| Delay | 0 / 100 / 200 / 300 buttons |
| Easing | linear / in / out / in-out |
| Transform | Combined card demo |
| Scale | `hover:scale-110` |
| Rotate | `hover:rotate-12` |
| Translate | `hover:translate-x-3 -translate-y-2` |
| Skew | `hover:skew-y-6` |
| Built-in: `animate-spin` | Spinner |
| Built-in: `animate-pulse` | Pulse dot + skeleton bar |
| Built-in: `animate-bounce` | Bouncing arrow |
| Built-in: `animate-ping` | Notification halo |
| Custom animations | `fade-up`, `float`, `shimmer` |

---
