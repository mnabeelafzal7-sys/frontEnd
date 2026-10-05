# Typography Mastery

## 1. Font family
**Use `font-sans`, `font-serif`, or `font-mono` to set the font stack.**
```tsx
<p className="font-sans">Sans</p>
<p className="font-serif">Serif</p>
<p className="font-mono">Mono</p>
```

## 2. Font size
**Use `text-{size}` (xs, sm, base, lg, xl, 2xl … 9xl).**
```tsx
<p className="text-sm">small</p>
<p className="text-3xl">big</p>
```

## 3. Font weight
**Use `font-{weight}` (thin, light, normal, medium, semibold, bold, extrabold, black).**
```tsx
<p className="font-semibold">Semibold</p>
```

## 4. Line height
**Use `leading-{size}` (none, tight, snug, normal, relaxed, loose, or `leading-6`).**
```tsx
<p className="leading-relaxed">Comfortable reading</p>
```

## 5. Letter spacing
**Use `tracking-{size}` (tighter, tight, normal, wide, wider, widest).**
```tsx
<h1 className="tracking-tight">Tight heading</h1>
```

## 6. Text alignment
**Use `text-left`, `text-center`, `text-right`, `text-justify`, `text-start`, `text-end`.**
```tsx
<p className="text-center">Centered</p>
```

## 7. Text decoration
**Use `underline`, `overline`, `line-through`, `no-underline`, plus color/thickness/offset.**
```tsx
<a className="underline decoration-indigo-500 decoration-2 underline-offset-4">Link</a>
```

## 8. Text transformation
**Use `uppercase`, `lowercase`, `capitalize`, `normal-case`.**
```tsx
<p className="uppercase tracking-wide">NEW</p>
```

## 9. Text truncation
**Use `truncate` for one-line ellipsis (needs a width constraint).**
```tsx
<p className="truncate w-40">A very long sentence that will be cut off…</p>
```

## 10. line-clamp
**Use `line-clamp-{n}` to limit visible lines with an ellipsis.**
```tsx
<p className="line-clamp-2">Long text limited to two lines before ellipsis appears…</p>
```

## 11. Gradient text
**Combine `bg-gradient-to-r`, `bg-clip-text`, `text-transparent`.**
```tsx
<h1 className="bg-gradient-to-r from-indigo-600 to-purple-600 bg-clip-text text-transparent">
  Gradient
</h1>
```

## 12. Responsive typography
**Scale size/leading/tracking across breakpoints.**
```tsx
<h1 className="text-2xl sm:text-3xl md:text-4xl lg:text-5xl font-bold leading-tight tracking-tight">
  Title
</h1>
```

## 13. Custom Google Fonts
**Load via `next/font/google`, expose as a CSS variable, then extend Tailwind.**
```tsx
// app/layout.tsx
import { Inter, Playfair_Display } from "next/font/google";

const inter = Inter({ subsets: ["latin"], variable: "--font-inter" });
const playfair = Playfair_Display({ subsets: ["latin"], variable: "--font-playfair" });

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en" className={`${inter.variable} ${playfair.variable}`}>
      <body className="font-sans">{children}</body>
    </html>
  );
}
```

```ts
// tailwind.config.ts
import type { Config } from "tailwindcss";

const config: Config = {
  content: ["./app/**/*.{ts,tsx}"],
  theme: {
    extend: {
      fontFamily: {
        sans: ["var(--font-inter)", "system-ui", "sans-serif"],
        display: ["var(--font-playfair)", "serif"],
      },
    },
  },
  plugins: [],
};

export default config;
```

```tsx
<h1 className="font-display text-4xl">Playfair heading</h1>
```

## 14. Heading hierarchy
**Use semantic tags (`h1`–`h6`) and scale them with consistent Tailwind classes.**
```tsx
<h1 className="text-4xl font-bold tracking-tight">H1</h1>
<h2 className="text-3xl font-semibold tracking-tight">H2</h2>
<h3 className="text-2xl font-semibold">H3</h3>
<h4 className="text-xl font-medium">H4</h4>
<h5 className="text-lg font-medium">H5</h5>
<h6 className="text-base font-medium uppercase tracking-wide text-slate-500">H6</h6>
```

---

## 🧠 Quick reference table

| Need | Classes |
|---|---|
| Body text | `text-base font-normal leading-relaxed` |
| Article heading | `text-3xl font-bold tracking-tight leading-tight` |
| Eyebrow label | `text-xs font-semibold uppercase tracking-widest text-indigo-600` |
| Quote | `text-xl italic leading-relaxed text-slate-700` |
| Code | `font-mono text-sm bg-slate-100 px-1 rounded` |
| Link | `text-indigo-600 underline underline-offset-4 hover:no-underline` |
| Truncate | `truncate` |
| Clamp | `line-clamp-2` |
| Gradient headline | `bg-gradient-to-r from-indigo-600 to-pink-600 bg-clip-text text-transparent` |

---

## ▶️ One-pager demo: typography showcase

```tsx
// app/page.tsx
export default function Home() {
  return (
    <main className="min-h-screen bg-white text-slate-800">
      <article className="max-w-3xl mx-auto px-4 sm:px-6 lg:px-8 py-12 sm:py-16 space-y-8">

        {/* Eyebrow + gradient H1 */}
        <header className="space-y-3">
          <p className="text-xs font-semibold uppercase tracking-widest text-indigo-600">
            Typography
          </p>
          <h1 className="text-3xl sm:text-4xl md:text-5xl font-bold tracking-tight leading-tight">
            Master{" "}
            <span className="bg-gradient-to-r from-indigo-600 to-pink-600 bg-clip-text text-transparent">
              typography
            </span>{" "}
            with Tailwind
          </h1>
          <p className="text-base sm:text-lg text-slate-600 leading-relaxed max-w-2xl">
            Everything from font stacks to gradient headlines — no custom CSS required.
          </p>
        </header>

        {/* Heading hierarchy */}
        <section className="space-y-3">
          <h2 className="text-2xl sm:text-3xl font-semibold tracking-tight">Heading hierarchy</h2>
          <h3 className="text-xl font-semibold">H3 heading</h3>
          <h4 className="text-lg font-medium">H4 heading</h4>
          <h5 className="text-base font-medium">H5 heading</h5>
          <h6 className="text-sm font-medium uppercase tracking-wide text-slate-500">H6 heading</h6>
        </section>

        {/* Families */}
        <section className="space-y-2">
          <h2 className="text-2xl font-semibold tracking-tight">Font families</h2>
          <p className="font-sans">Sans — the default UI font.</p>
          <p className="font-serif">Serif — good for editorial text.</p>
          <p className="font-mono text-sm bg-slate-100 inline-block px-2 py-1 rounded">mono — code</p>
        </section>

        {/* Weights + sizes */}
        <section className="space-y-2">
          <h2 className="text-2xl font-semibold tracking-tight">Weights & sizes</h2>
          <p className="text-sm font-light">light · text-sm</p>
          <p className="text-base font-normal">normal · text-base</p>
          <p className="text-lg font-medium">medium · text-lg</p>
          <p className="text-xl font-semibold">semibold · text-xl</p>
          <p className="text-2xl font-bold">bold · text-2xl</p>
          <p className="text-3xl font-black tracking-tight">black · text-3xl</p>
        </section>

        {/* Leading + tracking */}
        <section className="space-y-3">
          <h2 className="text-2xl font-semibold tracking-tight">Leading & tracking</h2>
          <p className="leading-tight">leading-tight — tight lines for headings.</p>
          <p className="leading-relaxed">leading-relaxed — comfortable for body copy.</p>
          <p className="tracking-tight font-semibold">tracking-tight</p>
          <p className="tracking-widest text-xs uppercase text-slate-500">tracking-widest</p>
        </section>

        {/* Alignment + transformation */}
        <section className="space-y-2">
          <h2 className="text-2xl font-semibold tracking-tight">Alignment & transformation</h2>
          <p className="text-left">Left aligned</p>
          <p className="text-center">Centered</p>
          <p className="text-right">Right aligned</p>
          <p className="text-justify text-sm text-slate-600">
            Justified text spreads evenly across the line for a clean editorial look.
          </p>
          <p className="uppercase tracking-wide text-sm">uppercase text</p>
          <p className="capitalize">capitalize every word</p>
          <p className="lowercase">LOWERCASE TEXT</p>
        </section>

        {/* Decoration */}
        <section className="space-y-2">
          <h2 className="text-2xl font-semibold tracking-tight">Decoration</h2>
          <p><a href="#" className="text-indigo-600 underline underline-offset-4 hover:no-underline">Underline link</a></p>
          <p><span className="line-through text-slate-500">strikethrough</span></p>
          <p>
            <a href="#" className="font-medium text-indigo-600 decoration-indigo-400 decoration-2 underline underline-offset-4">
              Thick colored underline
            </a>
          </p>
        </section>

        {/* Truncation */}
        <section className="space-y-3">
          <h2 className="text-2xl font-semibold tracking-tight">Truncation & line-clamp</h2>
          <p className="truncate w-56 bg-slate-50 px-3 py-2 rounded">
            This is a very long line that will be truncated with an ellipsis.
          </p>
          <p className="line-clamp-2 bg-slate-50 p-3 rounded text-slate-700">
            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris.
          </p>
          <p className="line-clamp-3 bg-slate-50 p-3 rounded text-slate-700">
            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
          </p>
        </section>

        {/* Quote */}
        <blockquote className="border-l-4 border-indigo-500 pl-4 italic text-lg leading-relaxed text-slate-700">
          "Typography is the craft of endowing human language with a durable visual form."
        </blockquote>

      </article>
    </main>
  );
}
```

---

## ✅ Coverage checklist

| Concept | Where in demo |
|---|---|
| Font family | `font-sans`, `font-serif`, `font-mono` |
| Font size | `text-sm` → `text-3xl` scale |
| Font weight | `font-light` → `font-black` |
| Line height | `leading-tight`, `leading-relaxed` |
| Letter spacing | `tracking-tight`, `tracking-widest` |
| Text alignment | left/center/right/justify |
| Text decoration | underline, offset, thickness, line-through |
| Text transformation | uppercase, capitalize, lowercase |
| Truncation | `truncate w-56` |
| line-clamp | `line-clamp-2`, `line-clamp-3` |
| Gradient text | hero `bg-clip-text text-transparent` |
| Responsive typography | `text-3xl sm:text-4xl md:text-5xl` |
| Custom Google Fonts | `next/font/google` + `fontFamily` extend |
| Heading hierarchy | `h1`–`h6` with consistent scale |

---

## 🚀 Suggested next extensions

1. **Fluid typography with `clamp()`** — one class, smooth scaling: `text-[clamp(1.5rem,4vw,3rem)]`.
2. **`@tailwindcss/typography` plugin** — `prose` classes for long-form articles.
3. **Custom text-shadow utilities** — via `theme.extend.textShadow`.
4. **Variable font weights** — animate weight on hover for hero headings.
5. **Headless CMS integration** — render headings dynamically with a `<Heading>` component that maps level → Tailwind classes.

Want me to fold this into your GitHub profile repo as a `/typography` route with a README section that mirrors the reference table above?
