# Dashboard UI Blocks

Every block a real dashboard needs, distilled to one-liners + the core markup. Each entry is copy-paste ready and consistent with the earlier builds.

---

## 1. Responsive navbar
**Sticky, blurred, brand left, links center, actions right; collapses below `md`.**
```tsx
<header className="sticky top-0 z-50 h-14 bg-white/80 dark:bg-slate-950/80 backdrop-blur border-b border-slate-200 dark:border-slate-800">
  <div className="h-full px-4 sm:px-6 flex items-center gap-3">
    <button className="md:hidden p-2 rounded-lg hover:bg-slate-100 dark:hover:bg-slate-800">☰</button>
    <a href="/" className="font-bold tracking-tight">◆ Acme</a>
    <ul className="hidden md:flex gap-6 text-sm text-slate-600 dark:text-slate-400 ml-6">
      <li><a href="#" className="hover:text-indigo-600">Dashboard</a></li>
      <li><a href="#" className="hover:text-indigo-600">Projects</a></li>
    </ul>
    <div className="ml-auto flex items-center gap-2">{/* search + bell + avatar */}</div>
  </div>
</header>
```

## 2. Sidebar
**Fixed width, sticky, sectioned nav, active state, hidden on mobile.**
```tsx
<aside className="hidden lg:flex w-60 shrink-0 flex-col bg-white dark:bg-slate-900 border-r border-slate-200 dark:border-slate-800">
  <nav className="p-3 space-y-6 text-sm overflow-y-auto">
    {sections.map((s) => (
      <div key={s.title}>
        <p className="px-3 mb-2 text-[10px] font-semibold uppercase tracking-wider text-slate-500">{s.title}</p>
        <ul className="space-y-1">
          {s.items.map((i) => (
            <li key={i.href}>
              <a href={i.href} className={["flex items-center gap-2.5 px-3 py-2 rounded-lg transition-colors",
                active === i.href ? "bg-indigo-50 text-indigo-700 font-medium" : "text-slate-600 hover:bg-slate-100"].join(" ")}>
                <span aria-hidden>{i.icon}</span>{i.label}
              </a>
            </li>
          ))}
        </ul>
      </div>
    ))}
  </nav>
</aside>
```

## 3. Mobile sidebar
**Slide-in drawer with backdrop; close on route change or backdrop click.**
```tsx
{open && (
  <div className="fixed inset-0 z-50 lg:hidden">
    <div className="absolute inset-0 bg-black/50 backdrop-blur-sm" onClick={onClose} aria-hidden />
    <div className="absolute inset-y-0 left-0 w-72 bg-white dark:bg-slate-900 p-4 space-y-2 animate-fadeUp">
      <div className="flex items-center justify-between mb-4">
        <span className="font-bold">◆ Acme</span>
        <button onClick={onClose} aria-label="Close" className="p-1.5 rounded-lg hover:bg-slate-100">✕</button>
      </div>
      {links.map((l) => <a key={l.href} href={l.href} className="block px-3 py-2 rounded-lg text-sm hover:bg-slate-100">{l.label}</a>)}
    </div>
  </div>
)}
```

## 4. Dashboard cards
**Reusable card with optional header / body / footer slots; container-query aware.**
```tsx
<div className="@container rounded-2xl bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 shadow-sm overflow-hidden">
  {(title || actions) && (
    <div className="flex flex-col @md:flex-row @md:items-center @md:justify-between gap-3 p-5 border-b border-slate-200 dark:border-slate-800">
      <div className="min-w-0">
        {title && <h3 className="font-semibold truncate">{title}</h3>}
        {subtitle && <p className="text-xs text-slate-500 truncate">{subtitle}</p>}
      </div>
      {actions && <div className="flex gap-2 shrink-0">{actions}</div>}
    </div>
  )}
  <div className="p-5">{children}</div>
</div>
```

## 5. Statistics
**KPI card with label, value (tabular nums), and colored change indicator.**
```tsx
<div className="rounded-2xl bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 p-5 shadow-sm">
  <p className="text-xs uppercase tracking-wider text-slate-500">{label}</p>
  <p className="text-2xl font-bold tracking-tight text-slate-900 dark:text-slate-50 mt-2 [font-variant-numeric:tabular-nums]">{value}</p>
  <p className={["text-xs mt-1 font-medium", positive ? "text-emerald-600 dark:text-emerald-400" : "text-rose-600 dark:text-rose-400"].join(" ")}>
    {change} vs last week
  </p>
</div>
```

## 6. Charts area
**Bar chart with CSS only; label row + bars in flex, height % driven by data.**
```tsx
<div className="flex items-end gap-1.5 h-40">
  {series.map((p) => (
    <div key={p.label} className="flex-1 flex flex-col items-center gap-2">
      <div className="w-full rounded-t bg-gradient-to-t from-indigo-500 to-purple-400 transition-[height] duration-500"
           style={{ height: `${(p.value / max) * 100}%` }} />
      <span className="text-[10px] text-slate-500">{p.label}</span>
    </div>
  ))}
</div>
```

## 7. AI agent cards
**Card per agent: avatar / icon, name, status badge, run stats, CTA.**
```tsx
<div className="rounded-2xl bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 p-5 shadow-sm
                hover:shadow-md hover:-translate-y-1 transition-all">
  <div className="flex items-start justify-between gap-3">
    <div className="flex items-center gap-3 min-w-0">
      <div className="w-10 h-10 rounded-xl bg-gradient-to-br from-indigo-500 to-purple-500 grid place-items-center text-white text-lg shrink-0">🤖</div>
      <div className="min-w-0">
        <p className="font-semibold truncate">{agent.name}</p>
        <p className="text-xs text-slate-500 truncate">{agent.model}</p>
      </div>
    </div>
    <span className={["text-xs px-2 py-1 rounded-full border whitespace-nowrap",
      agent.status === "running" ? "bg-emerald-50 text-emerald-700 border-emerald-200" : "bg-slate-100 text-slate-600 border-slate-200"].join(" ")}>
      {agent.status}
    </span>
  </div>
  <div className="grid grid-cols-3 gap-3 mt-5 text-center">
    <div><p className="text-lg font-bold">{agent.runs}</p><p className="text-xs text-slate-500">Runs</p></div>
    <div><p className="text-lg font-bold">{agent.success}%</p><p className="text-xs text-slate-500">Success</p></div>
    <div><p className="text-lg font-bold">{agent.latency}ms</p><p className="text-xs text-slate-500">Latency</p></div>
  </div>
</div>
```

## 8. User profile
**Cover + overlapping avatar + name + role + actions; card-wrapped.**
```tsx
<div className="rounded-3xl bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 shadow-sm overflow-hidden">
  <div className="h-32 bg-gradient-to-r from-indigo-500 to-purple-500" />
  <div className="px-6 -mt-12 flex flex-col sm:flex-row sm:items-end gap-4">
    <img src="/avatar.jpg" alt="" className="w-24 h-24 rounded-full border-4 border-white dark:border-slate-900 shadow-md" />
    <div className="pb-2">
      <h1 className="text-xl font-semibold">Ayesha Khan</h1>
      <p className="text-sm text-slate-500">Frontend Engineer · Karachi</p>
    </div>
    <div className="sm:ml-auto pb-2 flex gap-2">
      <button className="px-4 py-2 rounded-lg bg-indigo-600 text-white text-sm">Follow</button>
      <button className="px-4 py-2 rounded-lg border border-slate-300 text-sm">Message</button>
    </div>
  </div>
</div>
```

## 9. Notifications
**Bell icon with dot; anchored panel with divided rows + unread indicator.**
```tsx
<ul className="divide-y divide-slate-100 dark:divide-slate-800 max-h-72 overflow-y-auto">
  {items.map((n) => (
    <li key={n.id} className="px-4 py-3 hover:bg-slate-50 dark:hover:bg-slate-800/50 flex items-start gap-3">
      <span className={["mt-1.5 w-2 h-2 rounded-full shrink-0", n.unread ? "bg-indigo-500" : "bg-slate-300"].join(" ")} />
      <div className="flex-1 min-w-0">
        <p className="text-sm text-slate-800 dark:text-slate-100">{n.title}</p>
        <p className="text-xs text-slate-500">{n.when}</p>
      </div>
    </li>
  ))}
</ul>
```

## 10. Search
**Input with keyboard focus ring; command-palette variant uses fixed modal shell.**
```tsx
<input type="search" placeholder="Search…"
       className="w-full px-3 py-1.5 rounded-lg text-sm bg-slate-100 dark:bg-slate-900
                  placeholder:text-slate-400 border border-transparent
                  focus:outline-none focus:bg-white dark:focus:bg-slate-950
                  focus:border-indigo-500 focus:ring-2 focus:ring-indigo-500/30 transition-colors" />
```

## 11. Data table
**Head + rows + hover + status badges; wrap in `overflow-x-auto`.**
```tsx
<div className="rounded-2xl bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 shadow-sm overflow-hidden">
  <div className="overflow-x-auto">
    <table className="w-full text-sm">
      <thead className="bg-slate-50 dark:bg-slate-950/50 text-slate-500 dark:text-slate-400 text-left">
        <tr><th className="px-5 py-3 font-medium">Name</th><th className="px-5 py-3 font-medium">Status</th></tr>
      </thead>
      <tbody className="divide-y divide-slate-200 dark:divide-slate-800">
        {rows.map((r) => (
          <tr key={r.id} className="hover:bg-slate-50 dark:hover:bg-slate-800/50 transition-colors">
            <td className="px-5 py-3 font-medium">{r.name}</td>
            <td className="px-5 py-3"><span className="text-xs px-2 py-1 rounded-full bg-emerald-50 text-emerald-700 border border-emerald-200">Active</span></td>
          </tr>
        ))}
      </tbody>
    </table>
  </div>
</div>
```

## 12. Modal
**Fixed inset-0 + backdrop + centered panel; Escape closes, body scroll locks.**
```tsx
<div className="fixed inset-0 z-50 grid place-items-center p-4">
  <div className="absolute inset-0 bg-black/50 backdrop-blur-sm" onClick={onClose} aria-hidden />
  <div role="dialog" aria-modal="true" className="relative z-10 w-full max-w-lg rounded-2xl bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 shadow-2xl animate-fadeUp">
    <div className="flex items-center justify-between px-5 py-4 border-b border-slate-200 dark:border-slate-800">
      <h3 className="font-semibold">{title}</h3>
      <button onClick={onClose} aria-label="Close" className="p-1.5 rounded-lg hover:bg-slate-100">✕</button>
    </div>
    <div className="p-5">{children}</div>
  </div>
</div>
```

## 13. Form
**Field wrapper + shared input base; state colors layered on top.**
```tsx
<div className="space-y-1.5">
  <label className="text-sm font-medium text-slate-700 dark:text-slate-300">Email</label>
  <input className="w-full px-3.5 py-2.5 rounded-xl text-sm bg-white dark:bg-slate-900 border border-slate-300 dark:border-slate-700
                    placeholder:text-slate-400 focus:outline-none focus:border-indigo-500 focus:ring-4 focus:ring-indigo-500/20" />
</div>
```

## 14. Buttons
**`cva`-style variants + sizes + loading + disabled, with focus-visible ring.**
```tsx
<button className="inline-flex items-center gap-2 px-4 py-2.5 rounded-xl text-sm font-medium
                   bg-indigo-600 text-white shadow-sm
                   hover:-translate-y-0.5 hover:bg-indigo-700
                   active:translate-y-0 active:scale-[.98]
                   focus:outline-none focus-visible:ring-2 focus-visible:ring-indigo-500 focus-visible:ring-offset-2
                   disabled:opacity-60 disabled:cursor-not-allowed disabled:hover:translate-y-0
                   transition-all duration-200">
  Save
</button>
```

## 15. Badges
**Semantic tones via a static map; small, pill-shaped, bordered.**
```tsx
<span className="inline-flex items-center gap-1.5 text-xs font-medium px-2.5 py-1 rounded-full border bg-emerald-50 text-emerald-700 border-emerald-200">
  Active
</span>
```

## 16. Loading states
**Spinner + Skeleton; both respect reduced motion.**
```tsx
<span className="inline-block w-6 h-6 rounded-full border-2 border-slate-300 border-t-indigo-600 animate-spin motion-reduce:animate-none" />
<div className="animate-pulse rounded-lg bg-slate-200 dark:bg-slate-800 h-4 w-2/3" />
```

## 17. Error states
**Rose border + ring + `role="alert"` message + retry action.**
```tsx
<div role="alert" className="rounded-xl border border-rose-200 bg-rose-50 dark:bg-rose-500/10 p-4 text-sm text-rose-800 dark:text-rose-200 flex items-start gap-3">
  <span aria-hidden>⚠</span>
  <div className="flex-1">
    <p className="font-medium">Something went wrong</p>
    <p className="text-xs opacity-80 mt-0.5">{message}</p>
  </div>
  <button className="text-xs font-medium underline">Retry</button>
</div>
```

## 18. Dark mode
**Class strategy + CSS variables + FOWT-prevention script + `dark:` on every surface.**
```tsx
<div className="bg-white dark:bg-slate-900 text-slate-900 dark:text-slate-100 border border-slate-200 dark:border-slate-800">
  Themed surface
</div>
```

## 19. Responsive mobile design
**Mobile-first; stack on small, grid on `md`/`lg`; hide non-essential chrome on mobile.**
```tsx
<div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
  {/* auto reflows */}
</div>
```

## 20. Hover effects
**Lift + shadow + color shift, with motion-safe gating.**
```tsx
className="transition-all duration-300 hover:-translate-y-1 hover:shadow-lg motion-reduce:hover:translate-y-0"
```

## 21. Focus states
**Prefer `focus-visible:` with a ring; always remove default outline.**
```tsx
className="focus:outline-none focus-visible:ring-2 focus-visible:ring-indigo-500 focus-visible:ring-offset-2"
```

## 22. Transitions
**`transition` + `duration-*` + `ease-out`; keep under 300ms for UI.**
```tsx
className="transition-colors duration-200 ease-out"
```

## 23. Accessible controls
**Correct roles, ARIA states, keyboard support, meaningful labels.**
```tsx
<button aria-pressed={on} aria-label="Toggle theme" className="focus-visible:ring-2">…</button>
<div role="tablist">…</div>
<div role="dialog" aria-modal="true">…</div>
```

## 24. Clean reusable components
**`cva` variants + `cn()` merge + slot API + typed props.**
```tsx
export const Button = ({ variant, size, className, ...rest }: Props) => (
  <button className={cn(btn({ variant, size }), className)} {...rest} />
);
```

---

## 🧩 Block combination map

| Screen | Blocks used |
|---|---|
| **Overview** | Navbar + Sidebar + Stats + Charts + Activity |
| **Customers** | Navbar + Data table + Badges + Search |
| **AI Agents** | Navbar + Agent cards + Status badges + Modal |
| **Profile** | Navbar + Profile card + Tabs |
| **Notifications** | Navbar + Notification panel |
| **Settings** | Navbar + Form + Buttons + Toggles |
| **Auth** | Centered card + Form + Buttons |
| **Error page** | Error state + Retry action |

---

## 🎨 Rules that keep every block consistent

1. **One accent color** (`brand`) for CTAs, links, active states.
2. **One radius scale** — `rounded-xl` for controls, `rounded-2xl` for cards, `rounded-3xl` for hero surfaces.
3. **One shadow scale** — `shadow-sm` default, `shadow-md` hover, `shadow-2xl` modal.
4. **One spacing rhythm** — `p-5` cards, `gap-4`/`gap-6` grids, `space-y-6` sections.
5. **One focus ring** — `focus-visible:ring-2 focus-visible:ring-brand focus-visible:ring-offset-2`.
6. **One motion contract** — `transition-*` + `duration-200/300` + `ease-out`.
7. **Semantic tokens** — `bg-surface`, `text-ink`, `border-line` in both themes.
8. **Always accessible** — `role`, `aria-*`, keyboard, `motion-reduce:`.

---
