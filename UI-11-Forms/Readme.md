# Forms & Inputs

## 1. Input styling
**Use a consistent border + radius + padding, then layer focus and disabled states.**
```tsx
<input className="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 text-sm
                  focus:outline-none focus:border-indigo-500 focus:ring-4 focus:ring-indigo-500/15
                  disabled:bg-slate-100 disabled:cursor-not-allowed" />
```

## 2. Select styling
**Style `<select>` the same way; add a custom chevron with `appearance-none` + a background icon.**
```tsx
<select className="w-full appearance-none px-3.5 py-2.5 pr-10 rounded-xl border border-slate-300 text-sm
                   focus:outline-none focus:border-indigo-500 focus:ring-4 focus:ring-indigo-500/15
                   bg-[url('data:image/svg+xml;utf8,<svg xmlns=%22http://www.w3.org/2000/svg%22 fill=%22none%22 stroke=%22%2364748b%22 stroke-width=%222%22 viewBox=%220 0 24 24%22><path d=%22M6 9l6 6 6-6%22/></svg>')]
                   bg-no-repeat bg-[length:1rem] bg-[right_0.75rem_center]">
  <option>Choose…</option>
</select>
```

## 3. Checkbox styling
**Hide the native input and style a sibling using `peer-checked:` and `peer-focus-visible:`.**
```tsx
<label className="inline-flex items-center gap-2 cursor-pointer">
  <input type="checkbox" className="peer sr-only" />
  <span className="w-5 h-5 rounded-md border border-slate-300 grid place-items-center text-white text-xs
                   peer-checked:bg-indigo-600 peer-checked:border-indigo-600
                   peer-focus-visible:ring-2 peer-focus-visible:ring-indigo-500 peer-focus-visible:ring-offset-2
                   transition">✓</span>
  <span className="text-sm">Remember me</span>
</label>
```

## 4. Radio styling
**Same `peer` trick; use `rounded-full` and a dot via `peer-checked:` inner span.**
```tsx
<label className="inline-flex items-center gap-2 cursor-pointer">
  <input type="radio" name="plan" className="peer sr-only" />
  <span className="w-5 h-5 rounded-full border border-slate-300 grid place-items-center
                   peer-checked:border-indigo-600
                   peer-focus-visible:ring-2 peer-focus-visible:ring-indigo-500 peer-focus-visible:ring-offset-2">
    <span className="w-2.5 h-2.5 rounded-full bg-indigo-600 scale-0 peer-checked:scale-100 transition" />
  </span>
  <span className="text-sm">Pro</span>
</label>
```
> Tip: with a nested `peer-checked`, put `peer-checked:scale-100` on the outer wrapper and use `group`/`peer` state via a small CSS trick, or use Tailwind's `has-[:checked]:` on the wrapper.

## 5. Textarea styling
**Same as input + `min-h-*`, `resize-none` (or `resize-y`), and `leading-relaxed`.**
```tsx
<textarea rows={4} className="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 text-sm leading-relaxed resize-none
                              focus:outline-none focus:border-indigo-500 focus:ring-4 focus:ring-indigo-500/15" />
```

## 6. Placeholder styling
**Use `placeholder:text-{color}` to control placeholder color; add `placeholder-shown:` for state.**
```tsx
<input placeholder="you@example.com"
       className="placeholder:text-slate-400 placeholder:italic placeholder-shown:text-slate-400" />
```

## 7. Focus styling
**Prefer a ring over outline: `focus:outline-none focus:ring-4 focus:ring-indigo-500/15 focus:border-indigo-500`.**
```tsx
<input className="focus:outline-none focus:ring-4 focus:ring-indigo-500/15 focus:border-indigo-500" />
```

## 8. Error states
**Swap border + ring + background to rose; add a `role="alert"` message with `aria-describedby`.**
```tsx
<input aria-invalid className="border-rose-400 bg-rose-50/40 focus:border-rose-500 focus:ring-4 focus:ring-rose-500/15" />
<p role="alert" className="text-xs text-rose-600 mt-1">Email is required.</p>
```

## 9. Success states
**Same pattern with emerald; useful for validated fields.**
```tsx
<input className="border-emerald-400 focus:border-emerald-500 focus:ring-4 focus:ring-emerald-500/15" />
<p className="text-xs text-emerald-600 mt-1">✓ Looks good</p>
```

## 10. Disabled states
**Dim, lock cursor, and prevent hover changes.**
```tsx
<input disabled className="disabled:bg-slate-100 disabled:text-slate-500 disabled:cursor-not-allowed
                           disabled:hover:border-slate-300" />
```

## 11. Form layouts
**Stack related fields in a vertical form; group related controls in `fieldset` for a11y.**
```tsx
<form className="max-w-md space-y-5">
  <fieldset className="space-y-3">
    <legend className="text-sm font-medium text-slate-700">Shipping method</legend>
    {/* radios */}
  </fieldset>
  {/* fields */}
  <button type="submit" className="w-full py-3 rounded-xl bg-indigo-600 text-white font-medium">Save</button>
</form>
```

## 12. Responsive forms
**Stack fields on mobile, go 2-column on `sm`/`md`; keep actions full-width on small screens.**
```tsx
<form className="grid grid-cols-1 md:grid-cols-2 gap-4">
  <div className="md:col-span-2">{/* full-width field */}</div>
  <div>{/* half */}</div>
  <div>{/* half */}</div>
  <div className="md:col-span-2 flex flex-col sm:flex-row gap-3">
    <button className="flex-1 py-3 rounded-xl bg-indigo-600 text-white font-medium">Save</button>
    <button className="flex-1 py-3 rounded-xl border border-slate-300 font-medium">Cancel</button>
  </div>
</form>
```

---

## 🧠 Quick reference

| Need | Classes |
|---|---|
| Base input | `w-full px-3.5 py-2.5 rounded-xl border border-slate-300 text-sm` |
| Focus ring | `focus:outline-none focus:border-indigo-500 focus:ring-4 focus:ring-indigo-500/15` |
| Placeholder | `placeholder:text-slate-400` |
| Error | `border-rose-400 bg-rose-50/40 focus:ring-rose-500/15` |
| Success | `border-emerald-400 focus:ring-emerald-500/15` |
| Disabled | `disabled:bg-slate-100 disabled:cursor-not-allowed disabled:opacity-60` |
| Custom checkbox/radio | `peer sr-only` + styled sibling with `peer-checked:` |
| Custom select chevron | `appearance-none` + `bg-[url(...)]` + `bg-[right_0.75rem_center]` |
| Form layout | `space-y-5` (stack) or `grid grid-cols-1 md:grid-cols-2 gap-4` |
| Responsive actions | `flex flex-col sm:flex-row gap-3` + `flex-1` |

---

## ▶️ One-pager demo: every concept in one page

```tsx
// app/page.tsx
export default function Home() {
  return (
    <main className="min-h-screen bg-slate-50 text-slate-800 p-6 sm:p-10">
      <form
        className="max-w-2xl mx-auto bg-white rounded-2xl border border-slate-200 shadow-sm p-6 sm:p-8
                   grid grid-cols-1 md:grid-cols-2 gap-5"
      >
        <h1 className="md:col-span-2 text-2xl font-bold tracking-tight">
          Form Controls
        </h1>

        {/* ── 1. Input ── */}
        <div className="md:col-span-2 space-y-1.5">
          <label className="text-sm font-medium text-slate-700">Name</label>
          <input
            placeholder="Jane Doe"
            className="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 text-sm
                       placeholder:text-slate-400
                       transition-all duration-200
                       focus:outline-none focus:border-indigo-500 focus:ring-4 focus:ring-indigo-500/15"
          />
        </div>

        {/* ── 6. Placeholder ── */}
        <div className="md:col-span-2 space-y-1.5">
          <label className="text-sm font-medium text-slate-700">Email</label>
          <input
            type="email"
            placeholder="you@example.com"
            className="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 text-sm
                       placeholder:text-slate-400 placeholder:italic
                       focus:outline-none focus:border-indigo-500 focus:ring-4 focus:ring-indigo-500/15"
          />
        </div>

        {/* ── 2. Select with custom chevron ── */}
        <div className="space-y-1.5">
          <label className="text-sm font-medium text-slate-700">Country</label>
          <select
            className="w-full appearance-none px-3.5 py-2.5 pr-10 rounded-xl border border-slate-300 text-sm
                       focus:outline-none focus:border-indigo-500 focus:ring-4 focus:ring-indigo-500/15
                       bg-[url('data:image/svg+xml;utf8,<svg xmlns=%22http://www.w3.org/2000/svg%22 fill=%22none%22 stroke=%22%2364748b%22 stroke-width=%222%22 viewBox=%220 0 24 24%22><path d=%22M6 9l6 6 6-6%22/></svg>')]
                       bg-no-repeat bg-[length:1rem] bg-[right_0.75rem_center]"
          >
            <option>Pakistan</option>
            <option>United States</option>
            <option>Netherlands</option>
          </select>
        </div>

        {/* ── 3. Checkbox (peer) ── */}
        <div className="space-y-1.5">
          <span className="text-sm font-medium text-slate-700">Preferences</span>
          <label className="flex items-center gap-2 cursor-pointer">
            <input type="checkbox" className="peer sr-only" />
            <span className="w-5 h-5 rounded-md border border-slate-300 bg-white grid place-items-center
                             text-white text-xs transition
                             peer-checked:bg-indigo-600 peer-checked:border-indigo-600
                             peer-focus-visible:ring-2 peer-focus-visible:ring-indigo-500 peer-focus-visible:ring-offset-2">
              ✓
            </span>
            <span className="text-sm text-slate-700">Email me updates</span>
          </label>
        </div>

        {/* ── 4. Radio group (fieldset) ── */}
        <fieldset className="md:col-span-2 space-y-2">
          <legend className="text-sm font-medium text-slate-700 mb-1">Plan</legend>
          <div className="flex flex-wrap gap-4">
            {["Free", "Pro", "Team"].map((p, i) => (
              <label key={p} className="inline-flex items-center gap-2 cursor-pointer">
                <input type="radio" name="plan" defaultChecked={i === 1} className="peer sr-only" />
                <span className="w-5 h-5 rounded-full border border-slate-300 grid place-items-center
                                 peer-checked:border-indigo-600
                                 peer-focus-visible:ring-2 peer-focus-visible:ring-indigo-500 peer-focus-visible:ring-offset-2
                                 transition">
                  <span className="w-2.5 h-2.5 rounded-full bg-indigo-600
                                   scale-0 peer-checked:scale-100 transition-transform" />
                </span>
                <span className="text-sm">{p}</span>
              </label>
            ))}
          </div>
        </fieldset>

        {/* ── 5. Textarea ── */}
        <div className="md:col-span-2 space-y-1.5">
          <label className="text-sm font-medium text-slate-700">Bio</label>
          <textarea
            rows={4}
            placeholder="Tell us about yourself…"
            className="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 text-sm leading-relaxed resize-none
                       placeholder:text-slate-400
                       focus:outline-none focus:border-indigo-500 focus:ring-4 focus:ring-indigo-500/15"
          />
        </div>

        {/* ── 8. Error state ── */}
        <div className="space-y-1.5">
          <label className="text-sm font-medium text-slate-700">Email (error)</label>
          <input
            defaultValue="not-an-email"
            aria-invalid
            className="w-full px-3.5 py-2.5 rounded-xl border border-rose-400 bg-rose-50/40 text-sm
                       focus:outline-none focus:border-rose-500 focus:ring-4 focus:ring-rose-500/15"
          />
          <p role="alert" className="text-xs text-rose-600">Enter a valid email address.</p>
        </div>

        {/* ── 9. Success state ── */}
        <div className="space-y-1.5">
          <label className="text-sm font-medium text-slate-700">Username (valid)</label>
          <input
            defaultValue="jane_doe"
            className="w-full px-3.5 py-2.5 rounded-xl border border-emerald-400 text-sm
                       focus:outline-none focus:border-emerald-500 focus:ring-4 focus:ring-emerald-500/15"
          />
          <p className="text-xs text-emerald-600">✓ Looks good</p>
        </div>

        {/* ── 10. Disabled states ── */}
        <div className="space-y-1.5">
          <label className="text-sm font-medium text-slate-700">Disabled input</label>
          <input
            disabled
            defaultValue="Can't edit this"
            className="w-full px-3.5 py-2.5 rounded-xl border border-slate-200 bg-slate-100 text-slate-500 text-sm
                       cursor-not-allowed"
          />
        </div>

        <div className="space-y-1.5">
          <label className="text-sm font-medium text-slate-700">Disabled select</label>
          <select
            disabled
            className="w-full appearance-none px-3.5 py-2.5 pr-10 rounded-xl border border-slate-200 bg-slate-100 text-slate-500 text-sm
                       cursor-not-allowed"
          >
            <option>Locked</option>
          </select>
        </div>

        {/* ── 11 + 12. Responsive actions ── */}
        <div className="md:col-span-2 flex flex-col sm:flex-row gap-3 pt-2">
          <button
            type="submit"
            className="flex-1 py-3 rounded-xl bg-indigo-600 text-white font-medium
                       transition-all duration-200
                       hover:bg-indigo-700 hover:-translate-y-0.5
                       active:translate-y-0 active:scale-[.99]
                       focus:outline-none focus-visible:ring-2 focus-visible:ring-indigo-500 focus-visible:ring-offset-2"
          >
            Save changes
          </button>
          <button
            type="button"
            className="flex-1 py-3 rounded-xl border border-slate-300 text-slate-700 font-medium
                       transition-all duration-200
                       hover:bg-slate-50 hover:-translate-y-0.5
                       active:translate-y-0 active:scale-[.99]
                       focus:outline-none focus-visible:ring-2 focus-visible:ring-slate-500 focus-visible:ring-offset-2"
          >
            Cancel
          </button>
        </div>
      </form>
    </main>
  );
}
```

---

## ✅ Coverage checklist

| Concept | Where |
|---|---|
| Input styling | Base input with border/radius/padding |
| Select styling | `appearance-none` + custom chevron |
| Checkbox styling | `peer sr-only` + styled sibling |
| Radio styling | Same pattern + inner dot |
| Textarea styling | `rows`, `resize-none`, `leading-relaxed` |
| Placeholder styling | `placeholder:text-slate-400 placeholder:italic` |
| Focus styling | `focus:ring-4 focus:ring-indigo-500/15 focus:border-indigo-500` |
| Error states | Rose border + bg + `role="alert"` message |
| Success states | Emerald border + tick message |
| Disabled states | `disabled:` variants + `cursor-not-allowed` |
| Form layouts | `space-y-5` stack + `grid grid-cols-1 md:grid-cols-2` |
| Responsive forms | `md:col-span-2`, `flex-col sm:flex-row` actions |

---
