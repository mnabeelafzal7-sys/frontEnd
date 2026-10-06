# Component Architecture

## 1. Conditional classes
**Compose classes with a helper or ternary; keep logic out of JSX where possible.**
```tsx
// Simplest: ternary
<div className={active ? "bg-indigo-600" : "bg-slate-200"} />

// Multi-condition: clsx-style helper
const cn = (...c: (string | false | null | undefined)[]) => c.filter(Boolean).join(" ");
<div className={cn("base", active && "bg-indigo-600", disabled && "opacity-50")} />
```

## 2. Dynamic classes
**Never build class names by string concatenation — map them explicitly.**
```tsx
// ❌ Bad — Tailwind can't see dynamic strings at build time
<div className={`bg-${color}-500`} />

// ✅ Good — full class names appear literally
const bg = { red: "bg-red-500", blue: "bg-blue-500" }[color];
<div className={bg} />
```

## 3. Reusable components
**Extract a component when the same markup appears 2–3 times; accept props for variation.**
```tsx
export function Tag({ children }: { children: React.ReactNode }) {
  return <span className="px-2 py-1 rounded-full bg-slate-100 text-xs">{children}</span>;
}
```

## 4. Button component
**Props for `variant`, `size`, `loading`, `disabled`; spread the rest onto `<button>`.**
```tsx
"use client";
import { forwardRef, type ButtonHTMLAttributes } from "react";

type Variant = "primary" | "secondary" | "ghost" | "danger";
type Size = "sm" | "md" | "lg";

const sizes: Record<Size, string> = {
  sm: "text-xs px-3 py-1.5 rounded-lg",
  md: "text-sm px-4 py-2.5 rounded-xl",
  lg: "text-base px-5 py-3 rounded-xl",
};

const variants: Record<Variant, string> = {
  primary: "bg-indigo-600 text-white hover:bg-indigo-700",
  secondary: "bg-white text-slate-800 border border-slate-300 hover:bg-slate-50",
  ghost: "text-slate-700 hover:bg-slate-100",
  danger: "bg-rose-600 text-white hover:bg-rose-700",
};

type Props = ButtonHTMLAttributes<HTMLButtonElement> & {
  variant?: Variant;
  size?: Size;
  loading?: boolean;
};

export const Button = forwardRef<HTMLButtonElement, Props>(function Button(
  { variant = "primary", size = "md", loading, disabled, className = "", children, ...rest },
  ref
) {
  return (
    <button
      ref={ref}
      disabled={disabled || loading}
      className={[
        "inline-flex items-center justify-center gap-2 font-medium select-none",
        "transition-all duration-200",
        "hover:-translate-y-0.5 active:translate-y-0 active:scale-[.98]",
        "focus:outline-none focus-visible:ring-2 focus-visible:ring-indigo-500 focus-visible:ring-offset-2",
        "disabled:opacity-60 disabled:cursor-not-allowed disabled:hover:translate-y-0",
        sizes[size],
        variants[variant],
        className,
      ]
        .filter(Boolean)
        .join(" ")}
      {...rest}
    >
      {loading && <span className="w-4 h-4 rounded-full border-2 border-white/40 border-t-white animate-spin" />}
      {children}
    </button>
  );
});
```

## 5. Card component
**Optional header / footer slots; keep body as `children`.**
```tsx
export function Card({
  title, subtitle, actions, footer, children, className = "",
}: {
  title?: string; subtitle?: string; actions?: React.ReactNode;
  footer?: React.ReactNode; children?: React.ReactNode; className?: string;
}) {
  return (
    <div className={["rounded-2xl bg-white border border-slate-200 shadow-sm", className].join(" ")}>
      {(title || actions) && (
        <div className="flex items-start justify-between gap-3 p-5 border-b border-slate-200">
          <div className="min-w-0">
            {title && <h3 className="font-semibold text-slate-900 truncate">{title}</h3>}
            {subtitle && <p className="text-xs text-slate-500 truncate">{subtitle}</p>}
          </div>
          {actions && <div className="flex gap-2 shrink-0">{actions}</div>}
        </div>
      )}
      <div className="p-5">{children}</div>
      {footer && <div className="px-5 py-4 border-t border-slate-200">{footer}</div>}
    </div>
  );
}
```

## 6. Modal component
**Portal-free modal using `fixed inset-0` + backdrop + escape key.**
```tsx
"use client";
import { useEffect } from "react";

export function Modal({
  open, onClose, title, children, footer,
}: {
  open: boolean; onClose: () => void; title: string;
  children: React.ReactNode; footer?: React.ReactNode;
}) {
  useEffect(() => {
    if (!open) return;
    const onKey = (e: KeyboardEvent) => e.key === "Escape" && onClose();
    document.addEventListener("keydown", onKey);
    document.body.style.overflow = "hidden";
    return () => {
      document.removeEventListener("keydown", onKey);
      document.body.style.overflow = "";
    };
  }, [open, onClose]);

  if (!open) return null;

  return (
    <div className="fixed inset-0 z-50 grid place-items-center p-4">
      <div className="absolute inset-0 bg-black/50 backdrop-blur-sm" onClick={onClose} aria-hidden />
      <div role="dialog" aria-modal="true" aria-label={title}
           className="relative z-10 w-full max-w-lg rounded-2xl bg-white shadow-2xl border border-slate-200
                      max-h-[90vh] overflow-y-auto">
        <div className="flex items-center justify-between px-5 py-4 border-b border-slate-200">
          <h3 className="font-semibold">{title}</h3>
          <button onClick={onClose} aria-label="Close"
                  className="p-1.5 rounded-lg hover:bg-slate-100 focus:outline-none focus-visible:ring-2 focus-visible:ring-indigo-500">
            ✕
          </button>
        </div>
        <div className="p-5">{children}</div>
        {footer && <div className="px-5 py-4 border-t border-slate-200 flex justify-end gap-3">{footer}</div>}
      </div>
    </div>
  );
}
```

## 7. Navbar component
**Sticky + backdrop blur; children handle the internals.**
```tsx
export function Navbar({
  brand, links, actions,
}: {
  brand: React.ReactNode;
  links: { label: string; href: string }[];
  actions?: React.ReactNode;
}) {
  return (
    <header className="sticky top-0 z-50 bg-white/80 backdrop-blur border-b border-slate-200">
      <nav className="max-w-7xl mx-auto flex items-center justify-between h-14 px-4 sm:px-6">
        <a href="/" className="font-bold tracking-tight">{brand}</a>
        <ul className="hidden md:flex items-center gap-6 text-sm text-slate-600">
          {links.map((l) => (
            <li key={l.href}>
              <a href={l.href} className="hover:text-indigo-600 transition-colors">{l.label}</a>
            </li>
          ))}
        </ul>
        {actions && <div className="flex items-center gap-2">{actions}</div>}
      </nav>
    </header>
  );
}
```

## 8. Sidebar component
**Sticky, hidden on mobile; sections + items via props.**
```tsx
export function Sidebar({
  sections,
}: {
  sections: { title: string; items: { label: string; href: string }[] }[];
}) {
  return (
    <aside className="hidden lg:block w-60 shrink-0">
      <nav className="sticky top-20 space-y-6 text-sm">
        {sections.map((s) => (
          <div key={s.title}>
            <h4 className="text-xs font-semibold uppercase tracking-wider text-slate-500 mb-2 px-3">
              {s.title}
            </h4>
            <ul className="space-y-1">
              {s.items.map((item) => (
                <li key={item.href}>
                  <a href={item.href}
                     className="block px-3 py-2 rounded-lg text-slate-700 hover:bg-white hover:shadow-sm transition">
                    {item.label}
                  </a>
                </li>
              ))}
            </ul>
          </div>
        ))}
      </nav>
    </aside>
  );
}
```

## 9. Form components
**Small `Field` wrapper + `Input` / `Select` / `Textarea` sharing the same styling contract.**
```tsx
export function Field({ label, error, hint, children }: {
  label: string; error?: string; hint?: string; children: React.ReactNode;
}) {
  return (
    <div className="space-y-1.5">
      <label className="text-sm font-medium text-slate-700">{label}</label>
      {children}
      {error ? <p role="alert" className="text-xs text-rose-600">{error}</p>
             : hint ? <p className="text-xs text-slate-500">{hint}</p> : null}
    </div>
  );
}

const base =
  "w-full px-3.5 py-2.5 rounded-xl border text-sm bg-white placeholder:text-slate-400 " +
  "transition-all duration-200 focus:outline-none " +
  "focus:border-indigo-500 focus:ring-4 focus:ring-indigo-500/15 " +
  "disabled:bg-slate-100 disabled:cursor-not-allowed";

export const Input = (props: React.InputHTMLAttributes<HTMLInputElement>) => (
  <input {...props} className={[base, props.className].filter(Boolean).join(" ")} />
);
export const Textarea = (props: React.TextareaHTMLAttributes<HTMLTextAreaElement>) => (
  <textarea {...props} className={[base, "resize-none", props.className].filter(Boolean).join(" ")} />
);
export const Select = (props: React.SelectHTMLAttributes<HTMLSelectElement>) => (
  <select {...props} className={[base, "appearance-none", props.className].filter(Boolean).join(" ")} />
);
```

## 10. Badge component
**Semantic `tone` maps to full class strings.**
```tsx
const tones = {
  neutral: "bg-slate-100 text-slate-700 border-slate-200",
  success: "bg-emerald-50 text-emerald-700 border-emerald-200",
  warning: "bg-amber-50 text-amber-700 border-amber-200",
  danger:  "bg-rose-50 text-rose-700 border-rose-200",
  brand:   "bg-indigo-50 text-indigo-700 border-indigo-200",
} as const;

export function Badge({
  tone = "neutral", children,
}: { tone?: keyof typeof tones; children: React.ReactNode }) {
  return (
    <span className={`inline-flex items-center gap-1.5 text-xs font-medium px-2.5 py-1 rounded-full border ${tones[tone]}`}>
      {children}
    </span>
  );
}
```

## 11. Alert component
**Similar tone mapping + an icon + optional dismiss.**
```tsx
const tones = {
  info:    { cls: "bg-blue-50 text-blue-800 border-blue-200", icon: "ℹ️" },
  success: { cls: "bg-emerald-50 text-emerald-800 border-emerald-200", icon: "✅" },
  warning: { cls: "bg-amber-50 text-amber-800 border-amber-200", icon: "⚠️" },
  danger:  { cls: "bg-rose-50 text-rose-800 border-rose-200", icon: "✕" },
} as const;

export function Alert({
  tone = "info", title, children,
}: { tone?: keyof typeof tones; title?: string; children?: React.ReactNode }) {
  const { cls, icon } = tones[tone];
  return (
    <div role="alert" className={`flex items-start gap-3 rounded-xl border p-4 text-sm ${cls}`}>
      <span aria-hidden>{icon}</span>
      <div className="flex-1">
        {title && <p className="font-medium">{title}</p>}
        {children && <div className="mt-0.5">{children}</div>}
      </div>
    </div>
  );
}
```

## 12. Loading component
**Skeletons or spinners — pick per use case.**
```tsx
export function Spinner({ size = "md" }: { size?: "sm" | "md" | "lg" }) {
  const s = { sm: "w-4 h-4 border-2", md: "w-6 h-6 border-2", lg: "w-10 h-10 border-4" }[size];
  return (
    <span
      role="status"
      aria-label="Loading"
      className={`inline-block rounded-full border-slate-300 border-t-indigo-600 animate-spin ${s}`}
    />
  );
}

export function Skeleton({ className = "" }: { className?: string }) {
  return (
    <div
      aria-hidden
      className={`animate-pulse rounded-lg bg-slate-200 ${className}`}
    />
  );
}
```

## 13. Responsive component architecture
**Keep every component mobile-first; add breakpoints at the call site, not deep inside.**
```tsx
// Container component: purely layout, no colors or content
export function Stack({
  direction = "col",
  gap = 4,
  className = "",
  children,
}: {
  direction?: "col" | "row" | "col-to-row";
  gap?: 2 | 3 | 4 | 6 | 8;
  className?: string;
  children: React.ReactNode;
}) {
  const dir =
    direction === "row"
      ? "flex-row"
      : direction === "col"
        ? "flex-col"
        : "flex-col md:flex-row"; // col-to-row
  return (
    <div className={`flex ${dir} gap-${gap} ${className}`}>{children}</div>
  );
}
```
> Note: `gap-${gap}` won't work dynamically in production. Use a map:
```tsx
const gapCls = { 2: "gap-2", 3: "gap-3", 4: "gap-4", 6: "gap-6", 8: "gap-8" } as const;
```

---

## 🧠 Architecture principles

| Principle | Do | Don't |
|---|---|---|
| **Class composition** | `cn()` helper or explicit maps | String concatenation with variables |
| **Variants** | Typed `variant`/`size`/`tone` props | Multiple boolean flags |
| **Slot API** | `header`, `footer`, `actions` props | Passing massive JSX blobs as `children` |
| **Styling entry** | One `className` prop merged last | Rewriting classes inside children |
| **Responsiveness** | Layout primitives (`Stack`, `Grid`) | Breakpoint logic inside every card |
| **Accessibility** | Correct roles, `aria-*`, focus rings | Removing focus outlines |
| **Theming** | Semantic tokens (`bg-surface`, `text-ink`) | Raw Tailwind shades everywhere |

---

## ▶️ One-pager demo: all components together

```tsx
// app/page.tsx
"use client";
import { useState } from "react";

// ── Local helpers (paste in as needed) ──
const cn = (...c: (string | false | null | undefined)[]) => c.filter(Boolean).join(" ");

const gapCls = { 2: "gap-2", 3: "gap-3", 4: "gap-4", 6: "gap-6", 8: "gap-8" } as const;

function Stack({
  direction = "col", gap = 4, className = "", children,
}: { direction?: "col" | "row" | "col-to-row"; gap?: keyof typeof gapCls; className?: string; children: React.ReactNode }) {
  const dir = direction === "row" ? "flex-row" : direction === "col" ? "flex-col" : "flex-col md:flex-row";
  return <div className={cn("flex", dir, gapCls[gap], className)}>{children}</div>;
}

export default function Home() {
  const [open, setOpen] = useState(false);
  const [loading, setLoading] = useState(false);

  async function fakeSave() {
    setLoading(true);
    await new Promise((r) => setTimeout(r, 1200));
    setLoading(false);
    setOpen(false);
  }

  return (
    <div className="min-h-screen bg-slate-50 text-slate-800">

      {/* Navbar */}
      <header className="sticky top-0 z-40 bg-white/80 backdrop-blur border-b border-slate-200">
        <nav className="max-w-5xl mx-auto flex items-center justify-between h-14 px-4 sm:px-6">
          <span className="font-bold tracking-tight">◆ Library</span>
          <Stack direction="row" gap={2}>
            <button className="px-3 py-1.5 rounded-lg text-sm text-slate-600 hover:bg-slate-100 transition">Docs</button>
            <button onClick={() => setOpen(true)}
                    className="px-3 py-1.5 rounded-lg text-sm bg-indigo-600 text-white hover:bg-indigo-700
                               focus:outline-none focus-visible:ring-2 focus-visible:ring-indigo-500 focus-visible:ring-offset-2 transition">
              Open modal
            </button>
          </Stack>
        </nav>
      </header>

      <main className="max-w-5xl mx-auto px-4 sm:px-6 py-10 space-y-10">

        {/* Alert demo */}
        <div className="flex items-start gap-3 rounded-xl border border-blue-200 bg-blue-50 text-blue-800 p-4 text-sm">
          <span aria-hidden>ℹ️</span>
          <div>
            <p className="font-medium">Everything is a component.</p>
            <p className="text-xs text-blue-700 mt-0.5">Buttons, cards, modals, badges, alerts, loaders.</p>
          </div>
        </div>

        {/* Buttons row */}
        <Stack direction="row" gap={3} className="flex-wrap">
          <button className="px-4 py-2.5 rounded-xl bg-indigo-600 text-white text-sm font-medium hover:bg-indigo-700 transition">Primary</button>
          <button className="px-4 py-2.5 rounded-xl bg-white text-slate-800 border border-slate-300 text-sm font-medium hover:bg-slate-50 transition">Secondary</button>
          <button className="px-4 py-2.5 rounded-xl text-slate-700 text-sm font-medium hover:bg-slate-100 transition">Ghost</button>
          <button className="px-4 py-2.5 rounded-xl bg-rose-600 text-white text-sm font-medium hover:bg-rose-700 transition">Danger</button>
          <button
            className="px-4 py-2.5 rounded-xl bg-indigo-600 text-white text-sm font-medium hover:bg-indigo-700 transition inline-flex items-center gap-2 disabled:opacity-60 disabled:cursor-not-allowed"
            onClick={() => setOpen(true)}
          >
            Open modal
          </button>
        </Stack>

        {/* Cards grid */}
        <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-5">
          {[1, 2, 3].map((n) => (
            <div key={n} className="rounded-2xl bg-white border border-slate-200 shadow-sm">
              <div className="flex items-start justify-between gap-3 p-5 border-b border-slate-200">
                <div>
                  <h3 className="font-semibold">Card {n}</h3>
                  <p className="text-xs text-slate-500">Reusable slot API</p>
                </div>
                <span className="inline-flex items-center text-xs font-medium px-2.5 py-1 rounded-full border bg-emerald-50 text-emerald-700 border-emerald-200">
                  Active
                </span>
              </div>
              <div className="p-5 text-sm text-slate-600">
                Reusable Card component with header, body, and footer.
              </div>
              <div className="px-5 py-4 border-t border-slate-200 flex justify-end gap-2">
                <button className="px-3 py-1.5 rounded-lg border border-slate-300 text-xs font-medium hover:bg-slate-50">
                  Cancel
                </button>
                <button className="px-3 py-1.5 rounded-lg bg-indigo-600 text-white text-xs font-medium hover:bg-indigo-700">
                  Save
                </button>
              </div>
            </div>
          ))}
        </div>

        {/* Badges */}
        <Stack direction="row" gap={2} className="flex-wrap">
          {[
            ["Neutral", "bg-slate-100 text-slate-700 border-slate-200"],
            ["Success", "bg-emerald-50 text-emerald-700 border-emerald-200"],
            ["Warning", "bg-amber-50 text-amber-700 border-amber-200"],
            ["Danger", "bg-rose-50 text-rose-700 border-rose-200"],
            ["Brand", "bg-indigo-50 text-indigo-700 border-indigo-200"],
          ].map(([label, cls]) => (
            <span key={label} className={`inline-flex items-center text-xs font-medium px-2.5 py-1 rounded-full border ${cls}`}>
              {label}
            </span>
          ))}
        </Stack>

        {/* Loading demo */}
        <div className="rounded-2xl bg-white border border-slate-200 shadow-sm p-5 space-y-4">
          <h3 className="font-semibold">Loading</h3>
          <div className="flex items-center gap-4">
            <span className="inline-block w-4 h-4 rounded-full border-2 border-slate-300 border-t-indigo-600 animate-spin" />
            <span className="inline-block w-6 h-6 rounded-full border-2 border-slate-300 border-t-indigo-600 animate-spin" />
            <span className="inline-block w-10 h-10 rounded-full border-4 border-slate-300 border-t-indigo-600 animate-spin" />
          </div>
          <div className="space-y-2">
            <div className="animate-pulse rounded-lg bg-slate-200 h-4 w-2/3" />
            <div className="animate-pulse rounded-lg bg-slate-200 h-4 w-1/2" />
            <div className="animate-pulse rounded-lg bg-slate-200 h-4 w-3/4" />
          </div>
        </div>

        {/* Alerts row */}
        <div className="space-y-3">
          {[
            ["info", "Info", "bg-blue-50 text-blue-800 border-blue-200", "ℹ️"],
            ["success", "Success", "bg-emerald-50 text-emerald-800 border-emerald-200", "✅"],
            ["warning", "Warning", "bg-amber-50 text-amber-800 border-amber-200", "⚠️"],
            ["danger", "Error", "bg-rose-50 text-rose-800 border-rose-200", "✕"],
          ].map(([, title, cls, icon]) => (
            <div key={title} className={`flex items-start gap-3 rounded-xl border p-4 text-sm ${cls}`}>
              <span aria-hidden>{icon}</span>
              <div>
                <p className="font-medium">{title}</p>
                <p className="text-xs opacity-80 mt-0.5">This is a reusable {String(title).toLowerCase()} alert.</p>
              </div>
            </div>
          ))}
        </div>
      </main>

      {/* Modal */}
      {open && (
        <div className="fixed inset-0 z-50 grid place-items-center p-4">
          <div className="absolute inset-0 bg-black/50 backdrop-blur-sm" onClick={() => !loading && setOpen(false)} aria-hidden />
          <div role="dialog" aria-modal="true" aria-label="New item"
               className="relative z-10 w-full max-w-md rounded-2xl bg-white shadow-2xl border border-slate-200">
            <div className="flex items-center justify-between px-5 py-4 border-b border-slate-200">
              <h3 className="font-semibold">New item</h3>
              <button onClick={() => !loading && setOpen(false)} aria-label="Close"
                      disabled={loading}
                      className="p-1.5 rounded-lg hover:bg-slate-100 focus:outline-none focus-visible:ring-2 focus-visible:ring-indigo-500 disabled:opacity-50">
                ✕
              </button>
            </div>
            <div className="p-5 space-y-4">
              <div className="space-y-1.5">
                <label className="text-sm font-medium text-slate-700">Name</label>
                <input
                  disabled={loading}
                  placeholder="My project"
                  className="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 text-sm
                             placeholder:text-slate-400 focus:outline-none focus:border-indigo-500 focus:ring-4 focus:ring-indigo-500/15
                             disabled:bg-slate-100 disabled:cursor-not-allowed"
                />
              </div>
            </div>
            <div className="px-5 py-4 border-t border-slate-200 flex justify-end gap-3">
              <button
                disabled={loading}
                onClick={() => setOpen(false)}
                className="px-4 py-2 rounded-lg border border-slate-300 text-sm font-medium hover:bg-slate-50 disabled:opacity-50"
              >
                Cancel
              </button>
              <button
                disabled={loading}
                onClick={fakeSave}
                className="px-4 py-2 rounded-lg bg-indigo-600 text-white text-sm font-medium hover:bg-indigo-700
                           disabled:opacity-60 disabled:cursor-not-allowed inline-flex items-center gap-2"
              >
                {loading && <span className="w-4 h-4 rounded-full border-2 border-white/40 border-t-white animate-spin" />}
                {loading ? "Saving…" : "Save"}
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

## ✅ Coverage checklist

| Concept | Where |
|---|---|
| Conditional classes | `cn()` helper + ternaries in Modal / buttons |
| Dynamic classes | Explicit maps — no `bg-${color}` patterns |
| Reusable components | `Button`, `Card`, `Modal`, `Badge`, `Alert`, `Spinner`, `Skeleton`, `Stack` |
| Button component | Variants + sizes + loading + disabled |
| Card component | Header / body / footer slots |
| Modal component | Escape, backdrop, scroll lock, footer slot |
| Navbar component | Sticky + backdrop blur + actions slot |
| Sidebar component | Sticky + sectioned nav (in earlier dashboard builds) |
| Form components | `Field`, `Input`, `Select`, `Textarea` sharing base styles |
| Badge component | `tone` prop maps to full class strings |
| Alert component | `tone` prop + icon + optional title |
| Loading component | `Spinner` + `Skeleton` |
| Responsive component architecture | `Stack` primitive with `col-to-row` direction |

---
