# UI Design Patterns

Every screen you'll build in a real product, distilled to one-liners + minimal code.

---

## 1. Design a navbar
**Sticky, blurred, brand-left, links-center, actions-right.**
```tsx
<header className="sticky top-0 z-50 bg-white/80 backdrop-blur border-b border-slate-200">
  <nav className="max-w-7xl mx-auto flex items-center justify-between h-14 px-4 sm:px-6">
    <a href="/" className="font-bold tracking-tight">◆ Acme</a>
    <ul className="hidden md:flex gap-6 text-sm text-slate-600">
      <li><a href="#" className="hover:text-indigo-600">Product</a></li>
      <li><a href="#" className="hover:text-indigo-600">Pricing</a></li>
    </ul>
    <a href="#" className="px-4 py-2 rounded-lg bg-indigo-600 text-white text-sm font-medium">Sign in</a>
  </nav>
</header>
```

## 2. Design a mega menu
**Trigger with hover/focus; reveal a full-width panel with grouped columns.**
```tsx
<div className="relative group">
  <button className="px-3 py-2 text-sm font-medium text-slate-700 group-hover:text-indigo-600">Product ▾</button>
  <div className="absolute left-1/2 -translate-x-1/2 top-full mt-2 w-[720px] max-w-[90vw]
                  hidden group-hover:block group-focus-within:block
                  rounded-2xl bg-white border border-slate-200 shadow-xl p-6
                  grid grid-cols-3 gap-6 z-50">
    <div>
      <p className="text-xs font-semibold uppercase tracking-wider text-slate-500 mb-3">Features</p>
      <a href="#" className="block py-1.5 text-sm text-slate-700 hover:text-indigo-600">Analytics</a>
      <a href="#" className="block py-1.5 text-sm text-slate-700 hover:text-indigo-600">Automation</a>
    </div>
    {/* two more columns */}
  </div>
</div>
```

## 3. Design a hero section
**Big headline + subhead + two CTAs + image/mockup, mobile-first, gradient overlay.**
```tsx
<section className="relative overflow-hidden">
  <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-16 sm:py-24 grid lg:grid-cols-2 gap-10 items-center">
    <div className="space-y-5 text-center lg:text-left">
      <h1 className="text-4xl sm:text-5xl lg:text-6xl font-bold tracking-tight leading-tight">
        Ship faster with <span className="bg-gradient-to-r from-indigo-600 to-purple-600 bg-clip-text text-transparent">Acme</span>
      </h1>
      <p className="text-lg text-slate-600 max-w-xl mx-auto lg:mx-0 leading-relaxed">
        Everything you need to build, launch, and scale.
      </p>
      <div className="flex flex-col sm:flex-row gap-3 justify-center lg:justify-start">
        <a href="#" className="px-6 py-3 rounded-xl bg-indigo-600 text-white font-medium hover:bg-indigo-700">Get started</a>
        <a href="#" className="px-6 py-3 rounded-xl border border-slate-300 font-medium hover:bg-slate-50">Book a demo</a>
      </div>
    </div>
    <img src="/hero.png" alt="" className="rounded-2xl shadow-2xl w-full" />
  </div>
</section>
```

## 4. Design feature cards
**3-col grid on desktop; icon + title + description; hover lift.**
```tsx
<div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
  {features.map((f) => (
    <div key={f.title} className="rounded-2xl bg-white border border-slate-200 p-6 shadow-sm
                                  hover:shadow-md hover:-translate-y-1 transition-all">
      <div className="w-10 h-10 rounded-xl bg-indigo-50 text-indigo-600 grid place-items-center mb-4">{f.icon}</div>
      <h3 className="font-semibold text-slate-900 mb-1">{f.title}</h3>
      <p className="text-sm text-slate-600 leading-relaxed">{f.desc}</p>
    </div>
  ))}
</div>
```

## 5. Design pricing cards
**3 tiers, middle highlighted, badge, features list, CTA.**
```tsx
<div className="grid grid-cols-1 md:grid-cols-3 gap-6 lg:gap-8 items-stretch">
  {plans.map((p) => (
    <div key={p.name} className={[
      "relative flex flex-col rounded-3xl p-6 sm:p-8 border",
      p.highlight ? "border-indigo-600 bg-indigo-600 text-white shadow-2xl lg:scale-105"
                  : "border-slate-200 bg-white shadow-sm"
    ].join(" ")}>
      {p.badge && <span className="absolute -top-3 left-1/2 -translate-x-1/2 bg-white text-indigo-700 text-xs font-semibold px-3 py-1 rounded-full border">Popular</span>}
      <h3 className="text-lg font-semibold">{p.name}</h3>
      <p className="mt-4 mb-6"><span className="text-4xl font-bold">${p.price}</span><span className="text-sm opacity-70">/mo</span></p>
      <ul className="space-y-2 text-sm flex-1">
        {p.features.map((f) => <li key={f} className="flex gap-2"><span>✓</span>{f}</li>)}
      </ul>
      <button className={["mt-6 w-full py-3 rounded-xl font-medium", p.highlight ? "bg-white text-indigo-700" : "bg-indigo-600 text-white"].join(" ")}>
        Choose {p.name}
      </button>
    </div>
  ))}
</div>
```

## 6. Design testimonials
**Grid of quote cards with avatar, name, role; optionally a large featured quote.**
```tsx
<figure className="rounded-2xl bg-white border border-slate-200 p-6 shadow-sm space-y-4">
  <blockquote className="text-slate-800 leading-relaxed">"We shipped our MVP in a week."</blockquote>
  <figcaption className="flex items-center gap-3">
    <img src="https://i.pravatar.cc/40?img=12" alt="" className="w-10 h-10 rounded-full" />
    <div>
      <p className="text-sm font-semibold text-slate-900">Ayesha Khan</p>
      <p className="text-xs text-slate-500">CTO, Northwind</p>
    </div>
  </figcaption>
</figure>
```

## 7. Design FAQ
**`<details>` accordions with chevron rotate; no JS needed.**
```tsx
<div className="max-w-3xl mx-auto divide-y divide-slate-200 rounded-2xl border border-slate-200 bg-white">
  {faqs.map((f) => (
    <details key={f.q} className="group p-5">
      <summary className="flex items-center justify-between cursor-pointer list-none font-medium text-slate-900">
        {f.q}
        <span className="text-slate-400 group-open:rotate-180 transition-transform">▾</span>
      </summary>
      <p className="mt-3 text-sm text-slate-600 leading-relaxed">{f.a}</p>
    </details>
  ))}
</div>
```

## 8. Design CTA section
**Wide card with gradient background, headline, subhead, one or two buttons.**
```tsx
<section className="max-w-5xl mx-auto px-4 sm:px-6 my-16">
  <div className="rounded-3xl bg-gradient-to-br from-indigo-600 to-purple-600 text-white p-8 sm:p-12 text-center space-y-5">
    <h2 className="text-2xl sm:text-3xl font-bold tracking-tight">Ready to build?</h2>
    <p className="text-indigo-100 max-w-xl mx-auto">Join thousands of teams shipping faster with Acme.</p>
    <div className="flex flex-col sm:flex-row gap-3 justify-center">
      <a href="#" className="px-6 py-3 rounded-xl bg-white text-indigo-700 font-medium hover:bg-indigo-50">Get started</a>
      <a href="#" className="px-6 py-3 rounded-xl border border-white/40 text-white font-medium hover:bg-white/10">Talk to sales</a>
    </div>
  </div>
</section>
```

## 9. Design footer
**Multi-column with brand + link groups + bottom bar; stacks on mobile.**
```tsx
<footer className="border-t border-slate-200 bg-white">
  <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12 grid grid-cols-2 md:grid-cols-4 gap-8 text-sm">
    <div className="col-span-2 md:col-span-1">
      <p className="font-bold text-base">◆ Acme</p>
      <p className="text-slate-500 mt-2">Build better products, faster.</p>
    </div>
    <div>
      <p className="font-semibold mb-3">Product</p>
      <ul className="space-y-2 text-slate-500">
        <li><a href="#">Features</a></li><li><a href="#">Pricing</a></li>
      </ul>
    </div>
    {/* Company + Legal columns */}
  </div>
  <div className="border-t border-slate-200 py-6 text-center text-xs text-slate-500">© 2025 Acme</div>
</footer>
```

## 10. Design dashboard
**Shell = sidebar + topbar + content grid; mobile-first.**
```tsx
<div className="min-h-screen flex">
  <Sidebar className="hidden lg:flex" />
  <div className="flex-1 min-w-0 flex flex-col">
    <Topbar />
    <main className="flex-1 p-4 sm:p-6 lg:p-8 space-y-6">
      <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
        {stats.map((s) => <StatCard key={s.label} {...s} />)}
      </div>
      <div className="grid grid-cols-1 lg:grid-cols-2 gap-6">
        <Chart /><ActivityFeed />
      </div>
    </main>
  </div>
</div>
```

## 11. Design sidebar
**Fixed width, sectioned nav, active state, sticky; hidden on mobile.**
```tsx
<aside className="hidden lg:flex w-60 shrink-0 flex-col bg-white border-r border-slate-200">
  <a href="/" className="h-14 flex items-center px-4 font-bold border-b border-slate-200">◆ Acme</a>
  <nav className="p-3 space-y-1 text-sm overflow-y-auto">
    {items.map((i) => (
      <a key={i.href} href={i.href}
         className={["flex items-center gap-2 px-3 py-2 rounded-lg transition-colors",
                     active ? "bg-indigo-50 text-indigo-700 font-medium" : "text-slate-600 hover:bg-slate-100"].join(" ")}>
        {i.icon} {i.label}
      </a>
    ))}
  </nav>
</aside>
```

## 12. Design a data table
**Header row + zebra-free rows + hover + status badges; stack as cards on mobile.**
```tsx
<div className="rounded-2xl bg-white border border-slate-200 shadow-sm overflow-hidden">
  <div className="overflow-x-auto">
    <table className="w-full text-sm">
      <thead className="bg-slate-50 text-slate-500 text-left">
        <tr><th className="px-5 py-3 font-medium">Name</th><th className="px-5 py-3 font-medium">Status</th></tr>
      </thead>
      <tbody className="divide-y divide-slate-200">
        {rows.map((r) => (
          <tr key={r.id} className="hover:bg-slate-50 transition-colors">
            <td className="px-5 py-3 font-medium text-slate-800">{r.name}</td>
            <td className="px-5 py-3">
              <span className="inline-block text-xs px-2 py-1 rounded-full bg-emerald-50 text-emerald-700 border border-emerald-200">Active</span>
            </td>
          </tr>
        ))}
      </tbody>
    </table>
  </div>
</div>
```

## 13. Design a notification panel
**Dropdown anchored to a bell; unread dots, divided rows, footer action.**
```tsx
<div className="fixed bottom-24 right-4 sm:right-6 z-50 w-80 rounded-2xl bg-white border border-slate-200 shadow-2xl overflow-hidden">
  <div className="px-4 py-3 border-b border-slate-200 flex items-center justify-between">
    <h3 className="font-semibold text-sm">Notifications</h3>
    <button className="text-xs text-slate-500 hover:text-slate-800">Mark all read</button>
  </div>
  <ul className="divide-y divide-slate-100 max-h-72 overflow-y-auto">
    {items.map((n) => (
      <li key={n.id} className="px-4 py-3 hover:bg-slate-50 flex items-start gap-3">
        <span className={`mt-1.5 w-2 h-2 rounded-full shrink-0 ${n.unread ? "bg-indigo-500" : "bg-slate-300"}`} />
        <div className="flex-1 min-w-0">
          <p className="text-sm text-slate-800">{n.title}</p>
          <p className="text-xs text-slate-500">{n.when}</p>
        </div>
      </li>
    ))}
  </ul>
  <a href="#" className="block text-center text-xs py-3 border-t border-slate-200 text-indigo-600 hover:bg-slate-50">View all</a>
</div>
```

## 14. Design a profile page
**Cover + avatar overlap + name + meta + tabs + activity.**
```tsx
<div className="rounded-3xl bg-white border border-slate-200 shadow-sm overflow-hidden">
  <div className="h-32 bg-gradient-to-r from-indigo-500 to-purple-500" />
  <div className="px-6 -mt-12 flex flex-col sm:flex-row sm:items-end gap-4">
    <img src="/avatar.jpg" alt="" className="w-24 h-24 rounded-full border-4 border-white shadow-md" />
    <div className="pb-2">
      <h1 className="text-xl font-semibold">Ayesha Khan</h1>
      <p className="text-sm text-slate-500">Frontend Engineer · Karachi</p>
    </div>
    <div className="sm:ml-auto pb-2 flex gap-2">
      <button className="px-4 py-2 rounded-lg bg-indigo-600 text-white text-sm font-medium">Follow</button>
      <button className="px-4 py-2 rounded-lg border border-slate-300 text-sm font-medium">Message</button>
    </div>
  </div>
</div>
```

## 15. Design a settings page
**Two-column: nav on left, form on right; sections with save actions.**
```tsx
<div className="grid grid-cols-1 md:grid-cols-[220px_minmax(0,1fr)] gap-8">
  <nav className="space-y-1 text-sm">
    {["Profile", "Account", "Notifications", "Security", "Billing"].map((s, i) => (
      <a key={s} href="#"
         className={["block px-3 py-2 rounded-lg",
                     i === 0 ? "bg-indigo-50 text-indigo-700 font-medium" : "text-slate-600 hover:bg-slate-100"].join(" ")}>
        {s}
      </a>
    ))}
  </nav>
  <div className="space-y-6">
    <section className="rounded-2xl bg-white border border-slate-200 p-6 space-y-4">
      <h2 className="font-semibold">Profile</h2>
      <div className="grid grid-cols-1 sm:grid-cols-2 gap-4">
        <label className="space-y-1.5"><span className="text-sm text-slate-700">Name</span><input className="w-full px-3 py-2 rounded-lg border border-slate-300" /></label>
        <label className="space-y-1.5"><span className="text-sm text-slate-700">Email</span><input className="w-full px-3 py-2 rounded-lg border border-slate-300" /></label>
      </div>
      <div className="flex justify-end"><button className="px-4 py-2 rounded-lg bg-indigo-600 text-white text-sm">Save</button></div>
    </section>
  </div>
</div>
```

## 16. Design authentication pages
**Route group with centered card, logo, heading, form, social auth, footer link.**
```tsx
// app/(auth)/layout.tsx
export default function AuthLayout({ children }: { children: React.ReactNode }) {
  return (
    <div className="min-h-screen grid place-items-center p-4 bg-slate-100">
      <div className="w-full max-w-md">
        <div className="text-center mb-6"><a href="/" className="font-bold text-lg">◆ Acme</a></div>
        {children}
      </div>
    </div>
  );
}
```
```tsx
// app/(auth)/login/page.tsx
<div className="rounded-3xl bg-white border border-slate-200 shadow-sm p-6 sm:p-8 space-y-5">
  <header>
    <h1 className="text-2xl font-bold tracking-tight">Welcome back</h1>
    <p className="text-sm text-slate-500 mt-1">Sign in to your account.</p>
  </header>
  <form className="space-y-4">
    <input placeholder="you@example.com" className="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 focus:outline-none focus:ring-4 focus:ring-indigo-500/20 focus:border-indigo-500" />
    <input type="password" placeholder="••••••••" className="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 focus:outline-none focus:ring-4 focus:ring-indigo-500/20 focus:border-indigo-500" />
    <button className="w-full py-3 rounded-xl bg-indigo-600 text-white font-medium hover:bg-indigo-700">Sign in</button>
  </form>
  <div className="flex items-center gap-3"><div className="flex-1 h-px bg-slate-200" /><span className="text-xs text-slate-400">OR</span><div className="flex-1 h-px bg-slate-200" /></div>
  <div className="flex gap-3">
    <button className="flex-1 py-2.5 rounded-xl border border-slate-300 text-sm">Google</button>
    <button className="flex-1 py-2.5 rounded-xl border border-slate-300 text-sm">GitHub</button>
  </div>
  <p className="text-center text-sm text-slate-500">New here? <a href="/signup" className="text-indigo-600 font-medium">Create an account</a></p>
</div>
```

---

## 🧠 Design cheat-sheet

| Pattern | Layout primitive | Key utilities |
|---|---|---|
| Navbar | `flex justify-between` | `sticky top-0 backdrop-blur` |
| Mega menu | `absolute` panel | `group-hover:block group-focus-within:block` |
| Hero | `grid lg:grid-cols-2` | `text-4xl sm:text-5xl lg:text-6xl` |
| Feature cards | `grid sm:grid-cols-2 lg:grid-cols-3` | `hover:-translate-y-1` |
| Pricing | `grid md:grid-cols-3` | highlight `lg:scale-105` |
| Testimonials | grid of `figure` | `<blockquote>` + `<figcaption>` |
| FAQ | `<details>` | `group-open:rotate-180` |
| CTA | single card | `bg-gradient-to-br` |
| Footer | `grid md:grid-cols-4` | `col-span-2 md:col-span-1` |
| Dashboard | shell | sidebar + topbar + content |
| Sidebar | `sticky top-*` | active = `bg-brand/10 text-brand` |
| Data table | `<table>` | `divide-y` + status badges |
| Notification panel | `fixed` or dropdown | `divide-y` + unread dots |
| Profile | cover + `-mt-12` avatar | `rounded-full border-4 border-white` |
| Settings | `grid md:grid-cols-[220px_1fr]` | sectioned cards |
| Auth | `grid place-items-center` | `max-w-md` card |

---
