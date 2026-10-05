# Positioning & Layering

## 1. `relative`
**Establishes a positioning context; children with `absolute` anchor to it.**
```tsx
<div className="relative">...</div>
```

## 2. `absolute`
**Removes from flow and positions against nearest positioned ancestor.**
```tsx
<div className="absolute top-2 right-2">badge</div>
```

## 3. `fixed`
**Positions relative to the viewport; stays put on scroll.**
```tsx
<button className="fixed bottom-6 right-6">FAB</button>
```

## 4. `sticky`
**Stays in normal flow until it hits an offset, then sticks.**
```tsx
<header className="sticky top-0 bg-white">Nav</header>
```

## 5. `inset-*`
**Shorthand for all four sides — great for full-cover overlays.**
```tsx
<div className="absolute inset-0 bg-black/40">overlay</div>
```

## 6. `top-*` / 7. `right-*` / 8. `bottom-*` / 9. `left-*`
**Offset a positioned element on a single side.**
```tsx
<div className="absolute top-0 right-0">top-right</div>
<div className="absolute bottom-4 left-4">bottom-left</div>
```

## 10. `z-*`
**Controls stacking order (`z-0`, `z-10`, `z-20`, `z-30`, `z-40`, `z-50`, `z-auto`).**
```tsx
<div className="relative z-50">modal</div>
```

## 11. Layered components
**Combine `relative` + absolutely positioned children + z-index for stacking.**
```tsx
<div className="relative">
  <img className="w-full rounded-xl" />
  <span className="absolute top-2 left-2 z-10 bg-black/70 text-white px-2 py-1 rounded text-xs">
    New
  </span>
</div>
```

## 12. Absolute badges
**Pin a badge to any corner of a relatively positioned parent.**
```tsx
<div className="relative inline-block">
  <img src="..." className="w-12 h-12 rounded-full" />
  <span className="absolute -top-1 -right-1 w-3 h-3 bg-emerald-500 rounded-full ring-2 ring-white" />
</div>
```

## 13. Floating buttons
**Use `fixed` + corner offsets for a FAB (floating action button).**
```tsx
<button className="fixed bottom-6 right-6 z-40 w-14 h-14 rounded-full bg-indigo-600 text-white shadow-lg hover:bg-indigo-700">
  +
</button>
```

## 14. Sticky navigation
**`sticky top-0` + a z-index + backdrop blur for a modern sticky header.**
```tsx
<header className="sticky top-0 z-50 bg-white/80 backdrop-blur border-b border-slate-200">
  <nav className="max-w-7xl mx-auto flex items-center justify-between px-4 h-16">…</nav>
</header>
```

## 15. Modal positioning
**Center with `fixed inset-0 grid place-items-center` + a dark backdrop.**
```tsx
{open && (
  <div className="fixed inset-0 z-50 grid place-items-center p-4">
    {/* Backdrop */}
    <div className="absolute inset-0 bg-black/50" onClick={close} />
    {/* Panel */}
    <div className="relative z-10 w-full max-w-md rounded-2xl bg-white p-6 shadow-2xl">
      Modal content
    </div>
  </div>
)}
```

---

## 🧠 Positioning cheat-sheet

| Utility | Behaviour | Typical use |
|---|---|---|
| `static` | Default flow | Normal content |
| `relative` | Flow + anchor for children | Card wrapper |
| `absolute` | Out of flow, anchors to nearest `relative` | Badges, overlays |
| `fixed` | Out of flow, anchors to viewport | FAB, mobile menu, toast |
| `sticky` | Flow until offset, then fixed | Header, sidebar, TOC |
| `inset-0` | Stretch to all edges | Overlay |
| `-top-1 -right-1` | Negative offsets for overlap | Notification dot |
| `z-50` | High stacking | Modal, dropdown |
| `z-40` | Below modal, above content | FAB, sticky header |

---

## ▶️ One-pager demo: every concept in one page

```tsx
"use client";
import { useState } from "react";

export default function Home() {
  const [open, setOpen] = useState(false);

  return (
    <div className="min-h-screen bg-slate-50 text-slate-800">

      {/* ── 14. Sticky navigation ── */}
      <header className="sticky top-0 z-50 bg-white/80 backdrop-blur border-b border-slate-200">
        <nav className="max-w-5xl mx-auto flex items-center justify-between px-4 sm:px-6 h-16">
          <span className="font-bold tracking-tight">◆ Positioning</span>
          <button
            onClick={() => setOpen(true)}
            className="px-4 py-2 rounded-lg bg-indigo-600 text-white text-sm font-medium hover:bg-indigo-700 transition"
          >
            Open modal
          </button>
        </nav>
      </header>

      <main className="max-w-5xl mx-auto px-4 sm:px-6 py-10 space-y-12">

        {/* ── 11 + 12. Layered card with absolute badge ── */}
        <section>
          <h2 className="text-lg font-semibold mb-4">Layered components & absolute badges</h2>
          <div className="grid grid-cols-1 sm:grid-cols-2 gap-6">

            {/* Image card with corner badge */}
            <div className="relative rounded-2xl overflow-hidden shadow-md">
              <img
                src="https://picsum.photos/seed/a/600/400"
                alt=""
                className="w-full h-48 object-cover"
              />
              {/* absolute badge (top-left) */}
              <span className="absolute top-3 left-3 z-10 bg-black/70 text-white text-xs px-2 py-1 rounded-full backdrop-blur">
                New
              </span>
              {/* absolute gradient overlay (inset-0) */}
              <div className="absolute inset-0 bg-gradient-to-t from-black/60 to-transparent" />
              {/* absolute caption (bottom-left) */}
              <div className="absolute bottom-3 left-3 right-3 text-white">
                <p className="font-semibold">Layered card</p>
                <p className="text-xs text-white/80">inset-0 overlay + absolute badge</p>
              </div>
            </div>

            {/* Avatar with notification dot */}
            <div className="rounded-2xl bg-white p-6 shadow-sm border border-slate-200 flex items-center gap-4">
              <div className="relative inline-block">
                <img
                  src="https://i.pravatar.cc/96?img=12"
                  alt="avatar"
                  className="w-16 h-16 rounded-full object-cover ring-2 ring-white shadow"
                />
                {/* Notification dot — absolute, negative offsets */}
                <span className="absolute -top-0.5 -right-0.5 w-4 h-4 bg-emerald-500 rounded-full ring-2 ring-white" />
                {/* Count badge */}
                <span className="absolute -bottom-1 -right-1 min-w-[1.25rem] h-5 px-1 grid place-items-center text-[10px] font-bold bg-rose-500 text-white rounded-full ring-2 ring-white">
                  3
                </span>
              </div>
              <div>
                <p className="font-semibold">Ayesha Khan</p>
                <p className="text-xs text-slate-500">Online · 3 new messages</p>
              </div>
            </div>
          </div>
        </section>

        {/* ── 1 + 2 + 5. Relative + absolute + inset demo ── */}
        <section>
          <h2 className="text-lg font-semibold mb-4">Relative + absolute + inset-0</h2>
          <div className="relative h-40 rounded-2xl bg-gradient-to-br from-indigo-500 to-purple-600 overflow-hidden">
            <div className="absolute inset-0 grid place-items-center text-white">
              <p className="font-semibold">Perfectly centered via inset-0 + grid</p>
            </div>
            <span className="absolute top-2 right-2 bg-white/20 text-white text-xs px-2 py-1 rounded-full">
              top-2 right-2
            </span>
            <span className="absolute bottom-2 left-2 bg-white/20 text-white text-xs px-2 py-1 rounded-full">
              bottom-2 left-2
            </span>
          </div>
        </section>

        {/* ── 10. Z-index stack demo ── */}
        <section>
          <h2 className="text-lg font-semibold mb-4">Z-index stacking</h2>
          <div className="relative h-40">
            <div className="absolute left-0 top-4 w-40 h-24 rounded-xl bg-slate-300 grid place-items-center text-xs z-0">
              z-0
            </div>
            <div className="absolute left-16 top-10 w-40 h-24 rounded-xl bg-indigo-300 grid place-items-center text-xs z-10">
              z-10
            </div>
            <div className="absolute left-32 top-16 w-40 h-24 rounded-xl bg-indigo-500 text-white grid place-items-center text-xs z-20">
              z-20
            </div>
          </div>
        </section>

        {/* ── 4. Sticky sidebar demo ── */}
        <section className="grid grid-cols-1 lg:grid-cols-3 gap-6">
          <aside className="lg:col-span-1">
            <div className="sticky top-20 rounded-2xl bg-white border border-slate-200 p-5 shadow-sm">
              <p className="font-semibold">Sticky sidebar</p>
              <p className="text-xs text-slate-500 mt-1">
                <code className="bg-slate-100 px-1 rounded">sticky top-20</code>
              </p>
            </div>
          </aside>
          <div className="lg:col-span-2 space-y-4">
            {Array.from({ length: 6 }).map((_, i) => (
              <div key={i} className="rounded-2xl bg-white border border-slate-200 p-5 shadow-sm">
                <p className="font-medium">Scroll content #{i + 1}</p>
                <p className="text-sm text-slate-500 mt-1">
                  Scroll and watch the sidebar stick below the header.
                </p>
              </div>
            ))}
          </div>
        </section>

      </main>

      {/* ── 13. Floating action button (fixed) ── */}
      <button
        aria-label="New item"
        className="fixed bottom-6 right-6 z-40 w-14 h-14 rounded-full bg-indigo-600 text-white text-2xl font-bold shadow-lg hover:bg-indigo-700 hover:shadow-xl transition grid place-items-center"
      >
        +
      </button>

      {/* ── 15. Modal (fixed inset-0 + grid place-items-center) ── */}
      {open && (
        <div className="fixed inset-0 z-50 grid place-items-center p-4">
          {/* Backdrop */}
          <div
            className="absolute inset-0 bg-black/50 backdrop-blur-sm"
            onClick={() => setOpen(false)}
            aria-hidden
          />
          {/* Panel */}
          <div
            role="dialog"
            aria-modal="true"
            className="relative z-10 w-full max-w-md rounded-2xl bg-white p-6 shadow-2xl border border-slate-200"
          >
            <h3 className="text-lg font-semibold">Modal title</h3>
            <p className="text-sm text-slate-600 mt-2 leading-relaxed">
              This modal is centered with{" "}
              <code className="bg-slate-100 px-1 rounded">fixed inset-0 grid place-items-center</code>{" "}
              and layered above the page with{" "}
              <code className="bg-slate-100 px-1 rounded">z-50</code>.
            </p>
            <div className="mt-6 flex gap-3 justify-end">
              <button
                onClick={() => setOpen(false)}
                className="px-4 py-2 rounded-lg border border-slate-300 text-sm font-medium hover:bg-slate-50"
              >
                Cancel
              </button>
              <button
                onClick={() => setOpen(false)}
                className="px-4 py-2 rounded-lg bg-indigo-600 text-white text-sm font-medium hover:bg-indigo-700"
              >
                Confirm
              </button>
            </div>
          </div>
        </div>
      )}
    </div>
  );
}
```

---

## 🎯 Layering strategy used

| Layer | z-index | What lives here |
|---|---|---|
| Page content | default | Main grid & sections |
| FAB | `z-40` | Floating action button |
| Sticky header | `z-50` | Top navigation |
| Modal backdrop | `z-50` (inside `fixed inset-0 z-50`) | Dark overlay |
| Modal panel | `z-10` (inside modal container) | Dialog itself |
| Absolute badges | `z-10` | Corner labels, dots |

Rule of thumb: **pick a small set of layers (0 / 10 / 20 / 40 / 50)** and never fight the numbers.

---

## ✅ Coverage checklist

| Concept | Where |
|---|---|
| `relative` | Card wrappers, image cards, avatar wrapper |
| `absolute` | Badges, notification dot, overlays, layered stack |
| `fixed` | FAB, modal container |
| `sticky` | Top nav, sticky sidebar |
| `inset-*` | `inset-0` overlay + centered content |
| `top-*` / `right-*` / `bottom-*` / `left-*` | Corner badges & labels |
| `z-*` | `z-0`/`z-10`/`z-20` stacking, `z-40` FAB, `z-50` nav & modal |
| Layered components | Image card with overlay + badge |
| Absolute badges | "New" chip, notification dot, count badge |
| Floating buttons | Fixed FAB |
| Sticky navigation | Sticky blurred header |
| Modal positioning | `fixed inset-0 grid place-items-center` + backdrop |

---

6. **Focus trap in modal** — combine with `focus-visible:ring` and a small `useEffect`.

Want me to fold this into your GitHub profile repo as a `/positioning` route with a README section that mirrors the cheat-sheet + layering strategy tables above?
