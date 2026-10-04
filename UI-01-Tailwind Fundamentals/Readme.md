# Tailwind Fundamentals

## 1. Install Tailwind CSS in a project
**Install Tailwind + its PostCSS plugin via npm.**
```bash
npm install -D tailwindcss postcss autoprefixer && npx tailwindcss init -p
```

## 2. Configure Tailwind CSS
**Define file paths in `tailwind.config.js` so Tailwind scans your templates.**
```js
// tailwind.config.js
module.exports = { content: ["./app/**/*.{ts,tsx}", "./components/**/*.{ts,tsx}"], theme: { extend: {} }, plugins: [] }
```

## 3. Understand utility-first CSS
**Style elements by composing small single-purpose classes instead of writing custom CSS.**
```tsx
<div className="p-4 bg-blue-500 text-white rounded">Hi</div>
```

## 4. Apply text colors
**Use `text-{color}-{shade}` to set text color.**
```tsx
<p className="text-red-500">Red text</p>
```

## 5. Apply background colors
**Use `bg-{color}-{shade}` to set background color.**
```tsx
<div className="bg-emerald-400">...</div>
```

## 6. Apply border colors
**Use `border-{color}-{shade}` along with a `border` width class.**
```tsx
<div className="border-2 border-blue-600">...</div>
```

## 7. Set font sizes
**Use `text-{size}` (xs, sm, base, lg, xl, 2xl…).**
```tsx
<h1 className="text-3xl">Title</h1>
```

## 8. Set font weights
**Use `font-{weight}` (thin, normal, medium, semibold, bold…).**
```tsx
<p className="font-semibold">Bold-ish</p>
```

## 9. Set line heights
**Use `leading-{size}` (tight, normal, relaxed, loose).**
```tsx
<p className="leading-relaxed">Comfortable text</p>
```

## 10. Set letter spacing
**Use `tracking-{size}` (tight, normal, wide, widest).**
```tsx
<h1 className="tracking-wide">Spaced</h1>
```

## 11. Set element width
**Use `w-{size}` (w-4, w-1/2, w-full, w-screen).**
```tsx
<div className="w-64">...</div>
```

## 12. Set element height
**Use `h-{size}` (h-8, h-1/2, h-full, h-screen).**
```tsx
<div className="h-40">...</div>
```

## 13. Set minimum/maximum width
**Use `min-w-{size}` and `max-w-{size}`.**
```tsx
<div className="min-w-32 max-w-md">...</div>
```

## 14. Set minimum/maximum height
**Use `min-h-{size}` and `max-h-{size}`.**
```tsx
<div className="min-h-16 max-h-96">...</div>
```

## 15. Apply padding
**Use `p-{size}`, `px-`, `py-`, `pt/pr/pb/pl-` for spacing inside.**
```tsx
<div className="px-4 py-2">...</div>
```

## 16. Apply margin
**Use `m-{size}`, `mx-`, `my-`, `mt/mr/mb/ml-` for spacing outside; `mx-auto` centers.**
```tsx
<div className="mt-4 mx-auto">...</div>
```

## 17. Understand spacing scale
**Spacing units are multiples of `0.25rem` (1 = 4px, 4 = 16px, 8 = 32px…).**
```tsx
<div className="p-4 mt-2 gap-6">...</div> {/* 16px, 8px, 24px */}
```

## 18. Use arbitrary values such as `w-[420px]`
**Wrap any custom value in square brackets to bypass the default scale.**
```tsx
<div className="w-[420px] h-[137px] bg-[#1da1f2]">...</div>
```

## 19. Combine multiple utilities correctly
**Stack classes in one `className`; later/conflicting ones follow CSS specificity (source order matters).**
```tsx
<button className="px-4 py-2 bg-blue-600 text-white text-sm font-medium rounded-md hover:bg-blue-700">
  Click
</button>
```
