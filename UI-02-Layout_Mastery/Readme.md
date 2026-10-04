# Layout Mastery

## 1. Understand CSS box model through Tailwind
**Every element = content + padding + border + margin; Tailwind exposes each layer via `p-*`, `border-*`, `m-*`.**
```tsx
<div className="m-2 border-4 border-blue-500 p-4">content</div>
```

## 2. Use `block`
**Element takes full width and starts on a new line.**
```tsx
<div className="block">Full-width block</div>
```

## 3. Use `inline`
**Element flows with text; width/height are ignored.**
```tsx
<span className="inline text-red-500">inline</span>
```

## 4. Use `inline-block`
**Flows inline but accepts width, height, padding, margin.**
```tsx
<span className="inline-block w-24 h-10 bg-blue-200">btn</span>
```

## 5. Use `flex`
**Turns a container into a flexbox (children become flex items).**
```tsx
<div className="flex">...</div>
```

## 6. Use `flex-row`
**Lays flex children horizontally (default direction).**
```tsx
<div className="flex flex-row">...</div>
```

## 7. Use `flex-col`
**Stacks flex children vertically.**
```tsx
<div className="flex flex-col">...</div>
```

## 8. Use `flex-wrap`
**Wraps flex items onto new lines when they overflow.**
```tsx
<div className="flex flex-wrap">...</div>
```

## 9. Use `justify-*`
**Aligns items along the main axis (start, end, center, between, around, evenly).**
```tsx
<div className="flex justify-between">...</div>
```

## 10. Use `items-*`
**Aligns items along the cross axis (start, end, center, baseline, stretch).**
```tsx
<div className="flex items-center">...</div>
```

## 11. Use `content-*`
**Aligns multi-line flex content as a whole along the cross axis (needs `flex-wrap`).**
```tsx
<div className="flex flex-wrap content-between h-40">...</div>
```

## 12. Use `gap-*`
**Adds spacing between flex/grid items (row and column).**
```tsx
<div className="flex gap-4">...</div>
```

## 13. Use `space-x-*`
**Adds horizontal margin between adjacent children (except the first).**
```tsx
<div className="flex space-x-4">...</div>
```

## 14. Use `space-y-*`
**Adds vertical margin between stacked children (except the first).**
```tsx
<div className="space-y-3">...</div>
```

## 15. Use `grid`
**Turns a container into a CSS grid.**
```tsx
<div className="grid">...</div>
```

## 16. Define grid columns
**`grid-cols-{n}` sets the number of equal-width columns.**
```tsx
<div className="grid grid-cols-3 gap-4">...</div>
```

## 17. Define grid rows
**`grid-rows-{n}` sets the number of equal-height rows.**
```tsx
<div className="grid grid-rows-2 gap-4 h-64">...</div>
```

## 18. Use `col-span-*`
**Makes an item span multiple columns.**
```tsx
<div className="grid grid-cols-4"><div className="col-span-2">wide</div></div>
```

## 19. Use responsive grids
**Prefix grid utilities with breakpoints (`sm:`, `md:`, `lg:`) to change columns per screen.**
```tsx
<div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">...</div>
```

## 20. Use `place-items-*`
**Shorthand for `align-items` + `justify-items` on grid/flex containers.**
```tsx
<div className="grid place-items-center h-64">centered</div>
```

---

## 🧠 Quick mental model

| Need | Use |
|---|---|
| Flow like text | `inline` / `inline-block` |
| Full width row | `block` |
| 1D layout | `flex` + `justify-*` / `items-*` / `gap-*` |
| 2D layout | `grid` + `grid-cols-*` / `col-span-*` |
| Perfect centering | `flex items-center justify-center` or `grid place-items-center` |
| Sibling spacing | `space-x-*` / `space-y-*` (no gap support in older browsers) |

---

## ▶️ One-pager demo: Dashboard layout using every concept

```tsx
// app/page.tsx
export default function Home() {
  return (
    <main className="min-h-screen bg-slate-100 p-6 space-y-6">
      {/* 1. Block heading */}
      <h1 className="block text-2xl font-bold text-slate-800">
        Layout Mastery Dashboard
      </h1>

      {/* 2. Flex row with justify-between */}
      <div className="flex justify-between items-center bg-white p-4 rounded-xl shadow">
        <span className="inline-block px-3 py-1 bg-indigo-100 text-indigo-700 rounded-full text-sm">
          inline-block badge
        </span>
        <span className="text-sm text-slate-500">
          Last updated <span className="inline text-emerald-600">just now</span>
        </span>
      </div>

      {/* 3. Responsive grid with col-span */}
      <section className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
        <div className="lg:col-span-2 bg-white p-6 rounded-xl shadow h-32 grid place-items-center">
          Wide card (col-span-2)
        </div>
        <div className="bg-white p-6 rounded-xl shadow h-32 grid place-items-center">
          Card A
        </div>
        <div className="bg-white p-6 rounded-xl shadow h-32 grid place-items-center">
          Card B
        </div>
      </section>

      {/* 4. Flex-col with space-y */}
      <section className="flex flex-col space-y-3 bg-white p-6 rounded-xl shadow">
        <p className="font-medium text-slate-700">Stacked with space-y-3</p>
        <p className="text-sm text-slate-500">Item one</p>
        <p className="text-sm text-slate-500">Item two</p>
      </section>

      {/* 5. Flex-wrap + content-between + space-x */}
      <section className="flex flex-wrap content-between gap-4 h-40 bg-white p-4 rounded-xl shadow">
        {[1, 2, 3, 4, 5, 6].map((n) => (
          <span
            key={n}
            className="inline-block w-20 h-10 bg-gradient-to-r from-purple-400 to-indigo-500 text-white text-sm grid place-items-center rounded"
          >
            tag {n}
          </span>
        ))}
      </section>

      {/* 6. Grid rows + place-items */}
      <section className="grid grid-rows-2 grid-cols-3 gap-3 h-48 bg-white p-4 rounded-xl shadow">
        <div className="col-span-2 bg-slate-200 rounded grid place-items-center text-sm">rows demo</div>
        <div className="bg-slate-200 rounded grid place-items-center text-sm">B</div>
        <div className="bg-slate-200 rounded grid place-items-center text-sm">C</div>
        <div className="col-span-2 bg-slate-200 rounded grid place-items-center text-sm">D (span 2)</div>
      </section>
    </main>
  );
}
```
