# Backgrounds, Images & Overlays

## 1. Background images
**Use `bg-[url('...')]` for arbitrary URLs or extend `theme.backgroundImage` for named ones.**
```tsx
<div className="bg-[url('/hero.jpg')]">...</div>
```

## 2. Background positioning
**Use `bg-center`, `bg-top`, `bg-bottom`, `bg-left`, `bg-right`, or `bg-[position]`.**
```tsx
<div className="bg-center bg-no-repeat">...</div>
```

## 3. Background sizing
**Use `bg-auto`, `bg-cover`, `bg-contain`, or `bg-[length:200px_100px]`.**
```tsx
<div className="bg-cover bg-center">...</div>
```

## 4. bg-cover
**Scales image to cover the container, cropping overflow — best for full-bleed heroes.**
```tsx
<div className="bg-cover bg-center h-96">...</div>
```

## 5. bg-contain
**Scales image to fit entirely inside the container — best for logos / illustrations.**
```tsx
<div className="bg-contain bg-no-repeat bg-center h-40">...</div>
```

## 6. Background gradients
**Use `bg-gradient-to-{dir}` with `from-*`, `via-*`, `to-*`.**
```tsx
<div className="bg-gradient-to-br from-indigo-500 via-purple-500 to-pink-500">...</div>
```

## 7. Background overlays
**Stack a translucent color layer over an image using `absolute inset-0` + `bg-black/40`.**
```tsx
<div className="relative">
  <img src="/hero.jpg" className="w-full h-96 object-cover" />
  <div className="absolute inset-0 bg-black/40" />
</div>
```

## 8. Object positioning
**Use `object-center`, `object-top`, `object-bottom`, `object-left`, `object-right`, `object-[x_y]`.**
```tsx
<img className="object-cover object-top h-64 w-full" />
```

## 9. Object fit
**Use `object-cover`, `object-contain`, `object-fill`, `object-none`, `object-scale-down`.**
```tsx
<img className="object-cover w-full h-48 rounded-xl" />
```

## 10. Image aspect ratios
**Use `aspect-square`, `aspect-video`, `aspect-[4/3]` to lock proportions.**
```tsx
<img className="aspect-video w-full object-cover rounded-xl" />
```

## 11. Image cards
**Combine `overflow-hidden` + `rounded-*` + `object-cover` + hover scale.**
```tsx
<div className="rounded-2xl overflow-hidden shadow-sm group">
  <img className="w-full h-48 object-cover group-hover:scale-105 transition duration-500" />
  <div className="p-4"><h3 className="font-semibold">Title</h3></div>
</div>
```

## 12. Hero image overlays
**Full-bleed bg image + gradient overlay + centered text.**
```tsx
<section className="relative bg-[url('/hero.jpg')] bg-cover bg-center">
  <div className="absolute inset-0 bg-gradient-to-t from-black/70 via-black/30 to-transparent" />
  <div className="relative max-w-3xl mx-auto px-6 py-24 text-white text-center">
    <h1 className="text-4xl sm:text-5xl font-bold">Ship faster</h1>
    <p className="mt-4 text-white/80">Everything you need to build in one place.</p>
  </div>
</section>
```

---

## 🧠 Quick reference

| Need | Classes |
|---|---|
| Full-bleed hero bg | `bg-[url(...)] bg-cover bg-center` |
| Logo / illustration | `bg-contain bg-no-repeat bg-center` |
| Dark image overlay | `relative` + `absolute inset-0 bg-black/40` |
| Gradient overlay | `absolute inset-0 bg-gradient-to-t from-black/70 to-transparent` |
| Circular avatar | `w-12 h-12 rounded-full object-cover` |
| 16:9 media | `aspect-video w-full object-cover` |
| Card thumbnail | `h-48 w-full object-cover group-hover:scale-105` |
| Center crop portrait | `object-cover object-top` |
| Split hero | `grid lg:grid-cols-2` + `object-cover h-full` |

---

## ▶️ One-pager demo: every concept in one page

```tsx
// app/page.tsx
export default function Home() {
  return (
    <main className="min-h-screen bg-slate-50 text-slate-800">

      {/* ── 12. Hero image overlay (bg-image + gradient) ── */}
      <section
        className="relative bg-[url('https://picsum.photos/seed/hero/1600/900')] bg-cover bg-center"
      >
        {/* Gradient overlay */}
        <div className="absolute inset-0 bg-gradient-to-t from-black/80 via-black/40 to-black/10" />

        <div className="relative max-w-5xl mx-auto px-6 py-24 sm:py-32 text-center text-white">
          <span className="inline-block text-xs font-semibold uppercase tracking-widest bg-white/10 border border-white/20 px-3 py-1 rounded-full backdrop-blur">
            Hero overlay
          </span>
          <h1 className="mt-4 text-4xl sm:text-6xl font-bold tracking-tight leading-tight">
            Build beautiful<br /> backgrounds & images
          </h1>
          <p className="mt-5 text-base sm:text-lg text-white/80 max-w-2xl mx-auto leading-relaxed">
            From full-bleed hero images to perfectly cropped thumbnails — all with Tailwind utilities.
          </p>
          <div className="mt-8 flex flex-col sm:flex-row gap-3 justify-center">
            <button className="px-6 py-3 rounded-lg bg-white text-slate-900 font-medium hover:bg-slate-100 transition">
              Get Started
            </button>
            <button className="px-6 py-3 rounded-lg border border-white/40 text-white font-medium hover:bg-white/10 transition backdrop-blur">
              Learn more
            </button>
          </div>
        </div>
      </section>

      <div className="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 py-12 space-y-14">

        {/* ── 1 + 2 + 3 + 4. bg-cover vs bg-contain ── */}
        <section>
          <h2 className="text-xl font-semibold mb-4">Background sizing</h2>
          <div className="grid grid-cols-1 md:grid-cols-2 gap-4">

            {/* bg-cover — fills container */}
            <div className="relative rounded-2xl overflow-hidden h-56">
              <div className="absolute inset-0 bg-[url('https://picsum.photos/seed/a/800/600')] bg-cover bg-center" />
              <div className="absolute inset-0 bg-black/30" />
              <div className="relative h-full grid place-items-center text-white">
                <div className="text-center">
                  <p className="font-semibold">bg-cover</p>
                  <p className="text-xs text-white/80 mt-1">Fills, crops overflow</p>
                </div>
              </div>
            </div>

            {/* bg-contain — fits entirely, letterboxed */}
            <div className="rounded-2xl border border-slate-200 bg-white h-56 grid place-items-center
                            bg-[url('https://picsum.photos/seed/b/400/400')] bg-contain bg-no-repeat bg-center">
              <div className="bg-white/80 backdrop-blur px-3 py-1 rounded-full text-xs font-medium">
                bg-contain
              </div>
            </div>
          </div>
        </section>

        {/* ── 6. Gradient backgrounds ── */}
        <section>
          <h2 className="text-xl font-semibold mb-4">Gradient backgrounds</h2>
          <div className="grid grid-cols-1 sm:grid-cols-3 gap-4">
            <div className="rounded-2xl h-32 bg-gradient-to-r from-indigo-500 to-purple-600
                            flex items-center justify-center text-white text-sm font-medium">
              to-r
            </div>
            <div className="rounded-2xl h-32 bg-gradient-to-br from-rose-500 via-amber-400 to-emerald-500
                            flex items-center justify-center text-white text-sm font-medium">
              via (3-stop)
            </div>
            <div className="rounded-2xl h-32 bg-gradient-to-t from-slate-900 to-slate-100
                            flex items-center justify-center text-white text-sm font-medium">
              to-t
            </div>
          </div>
        </section>

        {/* ── 8 + 9. Object fit & positioning ── */}
        <section>
          <h2 className="text-xl font-semibold mb-4">Object fit & positioning</h2>
          <div className="grid grid-cols-2 sm:grid-cols-4 gap-4 text-xs text-center">
            <div>
              <img
                src="https://picsum.photos/seed/p1/600/600"
                alt="cover"
                className="w-full h-32 object-cover rounded-xl"
              />
              <p className="mt-2 text-slate-600">object-cover</p>
            </div>
            <div>
              <img
                src="https://picsum.photos/seed/p2/600/600"
                alt="contain"
                className="w-full h-32 object-contain bg-slate-200 rounded-xl"
              />
              <p className="mt-2 text-slate-600">object-contain</p>
            </div>
            <div>
              <img
                src="https://picsum.photos/seed/p3/600/300"
                alt="top"
                className="w-full h-32 object-cover object-top rounded-xl"
              />
              <p className="mt-2 text-slate-600">object-top</p>
            </div>
            <div>
              <img
                src="https://picsum.photos/seed/p4/600/300"
                alt="bottom"
                className="w-full h-32 object-cover object-bottom rounded-xl"
              />
              <p className="mt-2 text-slate-600">object-bottom</p>
            </div>
          </div>
        </section>

        {/* ── 10. Aspect ratios ── */}
        <section>
          <h2 className="text-xl font-semibold mb-4">Aspect ratios</h2>
          <div className="grid grid-cols-1 sm:grid-cols-3 gap-4">
            <div>
              <img
                src="https://picsum.photos/seed/r1/600/600"
                alt="square"
                className="w-full aspect-square object-cover rounded-2xl"
              />
              <p className="mt-2 text-xs text-center text-slate-600">aspect-square</p>
            </div>
            <div>
              <img
                src="https://picsum.photos/seed/r2/800/450"
                alt="video"
                className="w-full aspect-video object-cover rounded-2xl"
              />
              <p className="mt-2 text-xs text-center text-slate-600">aspect-video (16:9)</p>
            </div>
            <div>
              <img
                src="https://picsum.photos/seed/r3/800/600"
                alt="4/3"
                className="w-full aspect-[4/3] object-cover rounded-2xl"
              />
              <p className="mt-2 text-xs text-center text-slate-600">aspect-[4/3]</p>
            </div>
          </div>
        </section>

        {/* ── 11. Image cards ── */}
        <section>
          <h2 className="text-xl font-semibold mb-4">Image cards</h2>
          <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-5">
            {[1, 2, 3].map((n) => (
              <a
                key={n}
                href="#"
                className="group block rounded-2xl overflow-hidden bg-white border border-slate-200 shadow-sm
                           hover:shadow-lg hover:-translate-y-1 transition-all duration-300"
              >
                {/* Image with overlay + zoom on hover */}
                <div className="relative aspect-video overflow-hidden">
                  <img
                    src={`https://picsum.photos/seed/card${n}/800/450`}
                    alt=""
                    className="w-full h-full object-cover group-hover:scale-110 transition-transform duration-500"
                  />
                  {/* Badge overlay */}
                  <span className="absolute top-3 left-3 bg-white/90 backdrop-blur text-slate-800
                                   text-xs font-semibold px-2 py-1 rounded-full">
                    New
                  </span>
                  {/* Bottom gradient overlay */}
                  <div className="absolute inset-x-0 bottom-0 h-24
                                  bg-gradient-to-t from-black/70 to-transparent" />
                  <p className="absolute bottom-3 left-3 right-3 text-white font-medium text-sm">
                    Card title {n}
                  </p>
                </div>
                {/* Body */}
                <div className="p-4">
                  <p className="text-sm text-slate-600 leading-relaxed">
                    Short description of this image card.
                  </p>
                </div>
              </a>
            ))}
          </div>
        </section>

        {/* ── 7. Background overlay (colored) ── */}
        <section>
          <h2 className="text-xl font-semibold mb-4">Background overlays</h2>
          <div className="grid grid-cols-1 sm:grid-cols-3 gap-4">
            {[
              { label: "bg-black/40", overlay: "bg-black/40" },
              { label: "bg-white/60", overlay: "bg-white/60" },
              { label: "bg-indigo-600/50", overlay: "bg-indigo-600/50" },
            ].map((o) => (
              <div key={o.label} className="relative rounded-2xl overflow-hidden h-40">
                <img
                  src="https://picsum.photos/seed/ov/800/400"
                  alt=""
                  className="absolute inset-0 w-full h-full object-cover"
                />
                <div className={`absolute inset-0 ${o.overlay}`} />
                <div className="relative h-full grid place-items-center text-white font-medium text-sm">
                  {o.label}
                </div>
              </div>
            ))}
          </div>
        </section>

        {/* ── 12b. Split hero (image + content side-by-side) ── */}
        <section className="rounded-3xl overflow-hidden bg-white border border-slate-200 shadow-sm">
          <div className="grid grid-cols-1 md:grid-cols-2">
            <div className="p-8 sm:p-10 flex flex-col justify-center space-y-4">
              <span className="text-xs font-semibold uppercase tracking-widest text-indigo-600">
                Split hero
              </span>
              <h3 className="text-2xl sm:text-3xl font-bold tracking-tight">
                Text on one side, image on the other
              </h3>
              <p className="text-slate-600 leading-relaxed text-sm sm:text-base">
                Perfect for feature highlights. The image uses object-cover so it
                always fills its half without stretching.
              </p>
              <button className="self-start px-5 py-2.5 rounded-lg bg-indigo-600 text-white text-sm font-medium hover:bg-indigo-700 transition">
                Learn more
              </button>
            </div>
            <div className="relative min-h-[240px]">
              <img
                src="https://picsum.photos/seed/split/900/700"
                alt=""
                className="absolute inset-0 w-full h-full object-cover"
              />
            </div>
          </div>
        </section>

      </div>
    </main>
  );
}
```

---

## 🎨 Named background images (optional config)

If you use the same background repeatedly, register it in `tailwind.config.ts`:

```ts
theme: {
  extend: {
    backgroundImage: {
      "hero": "url('/hero.jpg')",
      "grid-pattern":
        "linear-gradient(rgba(15,23,42,.06) 1px, transparent 1px), linear-gradient(90deg, rgba(15,23,42,.06) 1px, transparent 1px)",
    },
    backgroundSize: {
      "grid": "32px 32px",
    },
  },
}
```

```tsx
<div className="bg-hero bg-cover bg-center">…</div>
<div className="bg-grid-pattern bg-grid">…</div>   {/* subtle grid pattern */}
```

---

## ✅ Coverage checklist

| Concept | Where |
|---|---|
| Background images | `bg-[url(...)]` used in hero + tiles |
| Background positioning | `bg-center`, `bg-top`, `bg-bottom` |
| Background sizing | `bg-cover`, `bg-contain` side-by-side |
| `bg-cover` | Hero + image cards |
| `bg-contain` | Illustration tile |
| Background gradients | Full 3-tile demo (2-stop, 3-stop, vertical) |
| Background overlays | Black / white / tinted overlays over same image |
| Object positioning | `object-top` vs `object-bottom` |
| Object fit | `object-cover` vs `object-contain` |
| Image aspect ratios | `aspect-square`, `aspect-video`, `aspect-[4/3]` |
| Image cards | Hover zoom + gradient overlay + badge |
| Hero image overlays | Top hero section with gradient overlay |

---
6. **Dark overlay accessibility** — ensure text over image meets WCAG AA (use `bg-black/60+`).

Want me to fold this into your GitHub profile repo as a `/backgrounds` route with a README section mirroring the quick-reference table above?
