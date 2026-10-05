# Responsive Design

## 1. Understand mobile-first design
**Write base styles for mobile first, then layer larger screens with `sm:`, `md:`, `lg:` prefixes.**
```tsx
<div className="text-sm md:text-base lg:text-lg">...</div>
```

## 2. Use `sm:`
**Applies at ≥640px (small tablets / large phones landscape).**
```tsx
<div className="p-2 sm:p-4">...</div>
```

## 3. Use `md:`
**Applies at ≥768px (tablets).**
```tsx
<div className="grid-cols-1 md:grid-cols-2">...</div>
```

## 4. Use `lg:`
**Applies at ≥1024px (laptops).**
```tsx
<div className="hidden lg:block">...</div>
```

## 5. Use `xl:`
**Applies at ≥1280px (desktops).**
```tsx
<div className="max-w-xl xl:max-w-2xl">...</div>
```

## 6. Use `2xl:`
**Applies at ≥1536px (large monitors).**
```tsx
<div className="text-base 2xl:text-lg">...</div>
```

## 7. Change typography responsively
**Scale font size, weight, and leading per breakpoint.**
```tsx
<h1 className="text-2xl sm:text-3xl md:text-4xl lg:text-5xl font-bold">Title</h1>
```

## 8. Change spacing responsively
**Scale padding, margin, and gap across breakpoints.**
```tsx
<section className="p-4 sm:p-6 md:p-8 lg:p-12 space-y-3 md:space-y-6">...</section>
```

## 9. Change layout responsively
**Switch between stacked and multi-column layouts at breakpoints.**
```tsx
<div className="flex flex-col md:flex-row">...</div>
```

## 10. Hide/show elements responsively
**Use `hidden` + `md:block` (or `md:hidden`) to toggle visibility per screen.**
```tsx
<span className="hidden md:inline">Desktop only</span>
<span className="md:hidden">Mobile only</span>
```

## 11. Change grid columns responsively
**Start with 1 column, add more as the screen grows.**
```tsx
<div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">...</div>
```

## 12. Change flex direction responsively
**Stack on mobile, row on desktop (or vice versa).**
```tsx
<div className="flex flex-col md:flex-row md:items-center">...</div>
```

## 13. Build mobile navigation
**Hamburger on mobile, full menu on desktop — pure Tailwind with `peer` + `hidden`.**
```tsx
<nav className="p-4">
  <input id="nav" type="checkbox" className="peer hidden" />
  <label htmlFor="nav" className="md:hidden cursor-pointer text-2xl">☰</label>
  <ul className="hidden peer-checked:flex flex-col gap-2 mt-3 md:flex md:flex-row md:gap-6 md:mt-0">
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</nav>
```

## 14. Build responsive cards
**Grid of cards: 1 col mobile → 2 → 3 → 4 as screen grows.**
```tsx
<div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-4">
  {items.map((i) => (
    <div key={i} className="bg-white p-4 rounded-xl shadow">Card {i}</div>
  ))}
</div>
```

## 15. Build responsive tables
**Show a table on desktop; render stacked cards on mobile.**
```tsx
{/* Mobile: card list */}
<div className="md:hidden space-y-3">
  {rows.map((r) => (
    <div key={r.id} className="bg-white p-4 rounded-xl shadow">
      <p className="font-semibold">{r.name}</p>
      <p className="text-sm text-slate-500">{r.email}</p>
    </div>
  ))}
</div>

{/* Desktop: real table */}
<table className="hidden md:table w-full bg-white rounded-xl shadow overflow-hidden">
  <thead className="bg-slate-100 text-left text-sm">
    <tr><th className="p-3">Name</th><th className="p-3">Email</th></tr>
  </thead>
  <tbody>
    {rows.map((r) => (
      <tr key={r.id} className="border-t">
        <td className="p-3">{r.name}</td>
        <td className="p-3">{r.email}</td>
      </tr>
    ))}
  </tbody>
</table>
```

## 16. Build responsive hero sections
**Stacked hero on mobile, split image + text on desktop; typography scales up.**
```tsx
<section className="flex flex-col-reverse md:flex-row items-center gap-6 md:gap-10 p-6 md:p-12">
  <div className="flex-1 text-center md:text-left space-y-4">
    <h1 className="text-3xl md:text-5xl font-bold tracking-tight">Build faster with Tailwind</h1>
    <p className="text-slate-600 text-base md:text-lg leading-relaxed">
      Ship responsive UIs without writing custom CSS.
    </p>
    <button className="px-5 py-3 rounded-lg bg-indigo-600 text-white font-medium hover:bg-indigo-700">
      Get Started
    </button>
  </div>
  <img src="https://picsum.photos/600/400" className="flex-1 rounded-2xl shadow-lg w-full object-cover" />
</section>
```

---

## 🧠 Breakpoint cheat-sheet

| Prefix | Min-width | Target |
|---|---|---|
| (none) | 0px | Mobile |
| `sm:` | 640px | Large phones / small tablets |
| `md:` | 768px | Tablets |
| `lg:` | 1024px | Laptops |
| `xl:` | 1280px | Desktops |
| `2xl:` | 1536px | Large monitors |

All are **min-width** — Tailwind is mobile-first.

---

## ▶️ One-pager demo: every concept in a single page

```tsx
// app/page.tsx
export default function Home() {
  const items = [1, 2, 3, 4];
  const rows = [
    { id: 1, name: "Ayesha", email: "ayesha@x.com" },
    { id: 2, name: "Bilal", email: "bilal@x.com" },
    { id: 3, name: "Sara", email: "sara@x.com" },
  ];

  return (
    <div className="min-h-screen bg-slate-100">
      {/* Mobile nav — pure Tailwind toggle */}
      <nav className="bg-white p-4 shadow-sm">
        <div className="flex justify-between items-center">
          <span className="font-bold">Logo</span>
          <input id="nav" type="checkbox" className="peer hidden" />
          <label htmlFor="nav" className="md:hidden cursor-pointer text-2xl">☰</label>
          <ul className="hidden peer-checked:flex flex-col gap-3 absolute top-16 left-0 right-0 bg-white p-4 shadow md:shadow-none md:static md:flex md:flex-row md:gap-6">
            <li><a href="#" className="hover:text-indigo-600">Home</a></li>
            <li><a href="#" className="hover:text-indigo-600">About</a></li>
            <li><a href="#" className="hover:text-indigo-600">Contact</a></li>
          </ul>
        </div>
      </nav>

      {/* Responsive Hero */}
      <section className="flex flex-col-reverse md:flex-row items-center gap-6 md:gap-10 p-6 md:p-12">
        <div className="flex-1 text-center md:text-left space-y-4">
          <h1 className="text-3xl md:text-5xl font-bold tracking-tight">
            Build faster with Tailwind
          </h1>
          <p className="text-slate-600 text-base md:text-lg leading-relaxed">
            Ship responsive UIs without writing custom CSS.
          </p>
          <button className="px-5 py-3 rounded-lg bg-indigo-600 text-white font-medium hover:bg-indigo-700 transition">
            Get Started
          </button>
        </div>
        <img
          src="https://picsum.photos/600/400"
          className="flex-1 rounded-2xl shadow-lg w-full object-cover"
          alt="hero"
        />
      </section>

      {/* Responsive cards */}
      <section className="p-6 md:p-8">
        <h2 className="text-xl md:text-2xl font-semibold mb-4">Features</h2>
        <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
          {items.map((i) => (
            <div key={i} className="bg-white p-4 md:p-6 rounded-xl shadow-sm">
              <p className="font-semibold">Feature {i}</p>
              <p className="text-sm text-slate-500 mt-1">Short description here.</p>
            </div>
          ))}
        </div>
      </section>

      {/* Responsive table */}
      <section className="p-6 md:p-8">
        <h2 className="text-xl md:text-2xl font-semibold mb-4">Users</h2>

        {/* Mobile: cards */}
        <div className="md:hidden space-y-3">
          {rows.map((r) => (
            <div key={r.id} className="bg-white p-4 rounded-xl shadow-sm">
              <p className="font-semibold">{r.name}</p>
              <p className="text-sm text-slate-500">{r.email}</p>
            </div>
          ))}
        </div>

        {/* Desktop: table */}
        <table className="hidden md:table w-full bg-white rounded-xl shadow-sm overflow-hidden">
          <thead className="bg-slate-100 text-left text-sm">
            <tr>
              <th className="p-3">Name</th>
              <th className="p-3">Email</th>
            </tr>
          </thead>
          <tbody>
            {rows.map((r) => (
              <tr key={r.id} className="border-t">
                <td className="p-3">{r.name}</td>
                <td className="p-3">{r.email}</td>
              </tr>
            ))}
          </tbody>
        </table>
      </section>

      {/* Hide/show demo */}
      <p className="hidden md:block text-center p-4 text-sm text-slate-500">
        You're on desktop 🖥️
      </p>
      <p className="md:hidden text-center p-4 text-sm text-slate-500">
        You're on mobile 📱
      </p>
    </div>
  );
}
```

---

## ✅ Coverage checklist

| Concept | Where |
|---|---|
| Mobile-first | All base classes written without prefix |
| `sm:` / `md:` / `lg:` / `xl:` | Cards, nav, hero, typography |
| `2xl:` | (extension point — e.g. `2xl:text-lg`) |
| Responsive typography | Hero `text-3xl md:text-5xl` |
| Responsive spacing | `p-6 md:p-12`, `gap-4 md:gap-10` |
| Responsive layout | `flex-col-reverse md:flex-row` |
| Hide/show | `hidden md:table`, `md:hidden`, peer toggle |
| Responsive grid | `grid-cols-1 sm:grid-cols-2 lg:grid-cols-4` |
| Flex direction flip | Nav + hero |
| Mobile nav | `peer` + `peer-checked:flex` |
| Responsive cards | Feature grid |
| Responsive table | Cards on mobile, table on `md+` |
| Responsive hero | Image + text split |

---

## 🚀 Suggested next extensions

1. **Container queries** — Tailwind v4 `@container` for component-level responsiveness.
2. **Dark mode responsive combo** — `dark:md:bg-slate-900`.
3. **JS mobile nav** — swap the `peer` hack for a `useState` toggle for animated menus.
4. **`<picture>` with `srcSet`** — serve different hero images per breakpoint.

Want me to fold this into your GitHub profile repo next — as a `/responsive-design` route plus a README section with this checklist?
