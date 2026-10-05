# Interaction States

## 1. `hover:`
**Applies styles when the pointer is over the element.**
```tsx
<button className="hover:bg-indigo-700">Hover</button>
```

## 2. `focus:`
**Applies when the element receives focus (mouse or keyboard).**
```tsx
<input className="focus:ring-2 focus:ring-indigo-500" />
```

## 3. `active:`
**Applies while the element is being pressed (mouse down / touch).**
```tsx
<button className="active:scale-95">Press me</button>
```

## 4. `visited:`
**Applies to visited `<a>` links (limited CSS properties).**
```tsx
<a className="text-indigo-600 visited:text-purple-600">Link</a>
```

## 5. `disabled:`
**Applies when a form control has `disabled` attribute.**
```tsx
<button disabled className="disabled:opacity-50 disabled:cursor-not-allowed">Save</button>
```

## 6. `checked:`
**Applies when a checkbox/radio is checked.**
```tsx
<input type="checkbox" className="checked:bg-indigo-600" />
```

## 7. `group-hover:`
**Child reacts to the parent's hover when parent has `group`.**
```tsx
<a className="group">
  <span className="group-hover:text-indigo-600">Title</span>
  <span className="group-hover:translate-x-1 transition">→</span>
</a>
```

## 8. `group-focus:`
**Child reacts to the parent's focus.**
```tsx
<div className="group">
  <input className="peer" />
  <p className="hidden group-focus:block">Focused!</p>
</div>
```

## 9. `peer`
**Mark a sibling so other siblings can react to its state.**
```tsx
<input id="toggle" type="checkbox" className="peer hidden" />
<label htmlFor="toggle" className="peer-checked:bg-indigo-600">Toggle</label>
```

## 10. `peer-*`
**Sibling variants: `peer-hover:`, `peer-focus:`, `peer-checked:`, `peer-disabled:`, `peer-invalid:`, `peer-placeholder-shown:` etc.**
```tsx
<input type="email" required className="peer" placeholder=" " />
<span className="hidden peer-invalid:block text-rose-500 text-xs">Invalid email</span>
```

## 11. Focus-visible states
**Only apply on keyboard focus (not mouse clicks) — the a11y-friendly default.**
```tsx
<button className="focus:outline-none focus-visible:ring-2 focus-visible:ring-indigo-500 focus-visible:ring-offset-2">
  Keyboard-friendly
</button>
```

## 12. Button interaction states
**Stack hover + active + focus-visible + disabled for a full state set.**
```tsx
<button className="
  px-4 py-2 rounded-lg bg-indigo-600 text-white font-medium
  hover:bg-indigo-700
  active:bg-indigo-800 active:scale-[.98]
  focus:outline-none focus-visible:ring-2 focus-visible:ring-indigo-500 focus-visible:ring-offset-2
  disabled:opacity-50 disabled:cursor-not-allowed disabled:hover:bg-indigo-600
  transition
">
  Save
</button>
```

## 13. Form interaction states
**Style placeholder, focus, invalid, and disabled — often via `peer` for sibling hints.**
```tsx
<div>
  <input
    type="email"
    required
    placeholder="you@example.com"
    className="
      w-full px-3 py-2 rounded-lg border border-slate-300
      placeholder:text-slate-400
      focus:outline-none focus:border-indigo-500 focus:ring-2 focus:ring-indigo-500/30
      disabled:bg-slate-100 disabled:cursor-not-allowed
      invalid:border-rose-500 invalid:focus:ring-rose-500/30
    "
  />
  <p className="hidden text-rose-500 text-xs mt-1 peer-invalid:block">Please enter a valid email.</p>
</div>
```

## 14. Card hover effects
**Combine `group` + lift + shadow + content reveal on hover.**
```tsx
<a className="group block rounded-2xl border border-slate-200 bg-white shadow-sm
               hover:shadow-lg hover:-translate-y-1 transition-all duration-300">
  <div className="overflow-hidden rounded-t-2xl">
    <img className="w-full h-48 object-cover group-hover:scale-105 transition-transform duration-500" />
  </div>
  <div className="p-5">
    <h3 className="font-semibold group-hover:text-indigo-600 transition-colors">Title</h3>
    <span className="opacity-0 group-hover:opacity-100 transition-opacity text-sm text-indigo-600">
      Read more →
    </span>
  </div>
</a>
```

---

## 🧠 Variant cheat-sheet

| Variant | Trigger |
|---|---|
| `hover:` | Pointer over element |
| `focus:` | Element focused (any input) |
| `focus-visible:` | Keyboard-only focus (recommended for buttons) |
| `focus-within:` | A descendant is focused |
| `active:` | Mouse/touch press |
| `visited:` | Visited link (limited props) |
| `disabled:` | `disabled` attribute |
| `enabled:` | Not disabled |
| `checked:` | Checkbox/radio checked |
| `indeterminate:` | Checkbox indeterminate |
| `required:` / `optional:` | Form input required state |
| `valid:` / `invalid:` | Browser validation state |
| `placeholder-shown:` | Placeholder visible (empty) |
| `group-hover:` | Parent `.group` hovered |
| `group-focus:` / `group-focus-within:` | Parent focus state |
| `peer-hover:` / `peer-focus:` / `peer-checked:` | Sibling `.peer` state |

---

## ▶️ One-pager demo: every state on one page

```tsx
// app/page.tsx
export default function Home() {
  return (
    <main className="min-h-screen bg-slate-50 text-slate-800 p-6 sm:p-10 space-y-12 max-w-4xl mx-auto">

      <h1 className="text-3xl sm:text-4xl font-bold tracking-tight">Interaction States</h1>

      {/* ── 12. Button interaction states ── */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Button states</h2>
        <div className="flex flex-wrap gap-3">
          <button className="px-4 py-2 rounded-lg bg-indigo-600 text-white font-medium
                             hover:bg-indigo-700 active:bg-indigo-800 active:scale-[.98]
                             focus:outline-none focus-visible:ring-2 focus-visible:ring-indigo-500 focus-visible:ring-offset-2
                             transition">
            Primary
          </button>

          <button disabled className="px-4 py-2 rounded-lg bg-indigo-600 text-white font-medium
                                      disabled:opacity-50 disabled:cursor-not-allowed">
            Disabled
          </button>

          <button className="px-4 py-2 rounded-lg border border-slate-300 font-medium
                             hover:bg-slate-100 active:bg-slate-200
                             focus:outline-none focus-visible:ring-2 focus-visible:ring-slate-500">
            Secondary
          </button>

          <a href="#" className="px-3 py-2 text-sm text-indigo-600 underline underline-offset-4
                                 hover:text-indigo-800 visited:text-purple-600">
            Visited link
          </a>
        </div>
      </section>

      {/* ── 11. Focus vs focus-visible comparison ── */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Focus vs focus-visible</h2>
        <p className="text-sm text-slate-500">
          Tab into both. Only the second shows a ring on keyboard focus (nothing on mouse click).
        </p>
        <div className="flex flex-wrap gap-3">
          <button className="px-4 py-2 rounded-lg bg-slate-800 text-white text-sm
                             focus:ring-2 focus:ring-rose-500 focus:outline-none">
            focus:
          </button>
          <button className="px-4 py-2 rounded-lg bg-slate-800 text-white text-sm
                             focus:outline-none focus-visible:ring-2 focus-visible:ring-emerald-500 focus-visible:ring-offset-2">
            focus-visible:
          </button>
        </div>
      </section>

      {/* ── 13. Form interaction states ── */}
      <section className="space-y-3 max-w-md">
        <h2 className="text-lg font-semibold">Form states</h2>

        <div>
          <label className="text-sm font-medium text-slate-700">Email</label>
          <input
            type="email"
            required
            placeholder="you@example.com"
            className="mt-1 w-full px-3 py-2 rounded-lg border border-slate-300
                       placeholder:text-slate-400
                       focus:outline-none focus:border-indigo-500 focus:ring-2 focus:ring-indigo-500/30
                       disabled:bg-slate-100 disabled:cursor-not-allowed
                       invalid:border-rose-500 invalid:focus:ring-rose-500/30"
          />
        </div>

        <div>
          <label className="text-sm font-medium text-slate-700">Disabled input</label>
          <input
            disabled
            value="Can't edit this"
            className="mt-1 w-full px-3 py-2 rounded-lg border border-slate-300 bg-slate-100 text-slate-500 cursor-not-allowed"
          />
        </div>

        {/* ── 9 + 10. peer-checked toggle ── */}
        <div className="flex items-center gap-3 pt-2">
          <input id="toggle" type="checkbox" className="peer sr-only" />
          <label
            htmlFor="toggle"
            className="relative w-11 h-6 rounded-full bg-slate-300 cursor-pointer transition
                       peer-checked:bg-indigo-600
                       peer-focus-visible:ring-2 peer-focus-visible:ring-indigo-500 peer-focus-visible:ring-offset-2
                       after:content-[''] after:absolute after:top-0.5 after:left-0.5
                       after:w-5 after:h-5 after:bg-white after:rounded-full after:transition
                       peer-checked:after:translate-x-5"
          />
          <span className="text-sm text-slate-600">Enable notifications</span>
        </div>

        {/* ── 10. peer-invalid hint ── */}
        <div>
          <input
            type="email"
            required
            placeholder="Invalid email demo (type 'abc')"
            className="peer w-full px-3 py-2 rounded-lg border border-slate-300
                       focus:outline-none focus:border-indigo-500 focus:ring-2 focus:ring-indigo-500/30
                       invalid:border-rose-500"
          />
          <p className="hidden peer-invalid:block text-rose-500 text-xs mt-1">
            Please enter a valid email.
          </p>
        </div>
      </section>

      {/* ── 7. group-hover ── */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">group-hover</h2>
        <a href="#" className="group inline-flex items-center gap-2 px-4 py-3 rounded-xl
                               bg-white border border-slate-200 shadow-sm hover:shadow-md transition">
          <span className="w-8 h-8 rounded-lg bg-indigo-100 group-hover:bg-indigo-600 transition-colors
                           grid place-items-center text-indigo-600 group-hover:text-white transition-colors">
            ★
          </span>
          <span className="font-medium text-slate-800 group-hover:text-indigo-600 transition-colors">
            Hover the card
          </span>
          <span className="text-slate-400 group-hover:translate-x-1 transition-transform">→</span>
        </a>
      </section>

      {/* ── 14. Card hover effects ── */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">Card hover effects</h2>
        <div className="grid grid-cols-1 sm:grid-cols-2 gap-5">
          {[1, 2].map((n) => (
            <a
              key={n}
              href="#"
              className="group block rounded-2xl overflow-hidden bg-white border border-slate-200 shadow-sm
                         hover:shadow-xl hover:-translate-y-1 transition-all duration-300
                         focus:outline-none focus-visible:ring-2 focus-visible:ring-indigo-500 focus-visible:ring-offset-2"
            >
              <div className="relative aspect-video overflow-hidden">
                <img
                  src={`https://picsum.photos/seed/state${n}/800/450`}
                  alt=""
                  className="w-full h-full object-cover group-hover:scale-110 transition-transform duration-500"
                />
                <span className="absolute top-3 left-3 bg-white/90 backdrop-blur text-slate-800
                                 text-xs font-semibold px-2 py-1 rounded-full">
                  New
                </span>
              </div>
              <div className="p-5 space-y-1">
                <h3 className="font-semibold group-hover:text-indigo-600 transition-colors">
                  Card title {n}
                </h3>
                <p className="text-sm text-slate-600">
                  Zoom, lift, shadow, and title color all respond to hover.
                </p>
                <span className="inline-flex items-center gap-1 text-sm font-medium text-indigo-600
                                 opacity-0 -translate-x-1 group-hover:opacity-100 group-hover:translate-x-0
                                 transition-all duration-300">
                  Read more →
                </span>
              </div>
            </a>
          ))}
        </div>
      </section>

      {/* ── 6. checked state ── */}
      <section className="space-y-3">
        <h2 className="text-lg font-semibold">checked: state</h2>
        <label className="flex items-center gap-3 cursor-pointer">
          <input type="checkbox" className="w-5 h-5 rounded accent-indigo-600
                                            checked:bg-indigo-600 checked:border-indigo-600" />
          <span className="text-sm">Remember me</span>
        </label>
      </section>

      {/* ── 8. group-focus-within ── */}
      <section className="space-y-3 max-w-md">
        <h2 className="text-lg font-semibold">group-focus-within</h2>
        <div className="group rounded-xl border border-slate-300 bg-white p-1
                        focus-within:border-indigo-500 focus-within:ring-2 focus-within:ring-indigo-500/30 transition">
          <input
            placeholder="Focus me — the wrapper lights up"
            className="w-full px-3 py-2 rounded-lg focus:outline-none bg-transparent"
          />
        </div>
      </section>

    </main>
  );
}
```

---

## ✅ Coverage checklist

| Concept | Where |
|---|---|
| `hover:` | Buttons, links, cards |
| `focus:` | Input + "focus:" button demo |
| `active:` | Primary button (`active:scale-[.98]`) |
| `visited:` | Visited link |
| `disabled:` | Disabled button + input |
| `checked:` | Checkbox with `accent-indigo-600` |
| `group-hover:` | Inline card + image card |
| `group-focus:` / `focus-within:` | Wrapped input highlighting its container |
| `peer` + `peer-*` | Toggle switch, invalid email hint |
| Focus-visible | Dedicated comparison + all CTAs |
| Button interaction states | Full stack on primary button |
| Form interaction states | Email input (placeholder, focus, invalid, disabled) |
| Card hover effects | Zoom + lift + shadow + title + reveal CTA |

---
