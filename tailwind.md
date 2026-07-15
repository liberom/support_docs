# Tailwind CSS v4

Tailwind CSS is a utility-first CSS framework that provides low-level utility classes to build custom designs directly in your HTML. Version 4 introduces a completely new high-performance engine built in Rust, CSS-first configuration using the `@theme` directive, native CSS cascade layers, and simplified installation. It offers a vast collection of pre-designed utility classes for spacing, colors, typography, flexbox, grid, animations, and more, allowing developers to rapidly prototype and build production-ready interfaces without writing custom CSS.

The framework is designed around the concept of design tokens stored as CSS custom properties (theme variables), which generate corresponding utility classes. This approach enables real-time customization, seamless theming, and excellent developer experience with automatic class detection and tree-shaking of unused styles. Tailwind CSS v4 works with any modern build tool through official plugins for Vite, PostCSS, and a standalone CLI.

## Installation with Vite

The most seamless way to integrate Tailwind CSS v4 with modern frameworks like React, Vue, SvelteKit, Laravel, Nuxt, and SolidJS using the official Vite plugin.

```bash
# Create a new Vite project
npm create vite@latest my-project
cd my-project

# Install Tailwind CSS and the Vite plugin
npm install tailwindcss @tailwindcss/vite
```

```javascript
// vite.config.ts
import { defineConfig } from 'vite'
import tailwindcss from '@tailwindcss/vite'

export default defineConfig({
  plugins: [
    tailwindcss(),
  ],
})
```

```css
/* app.css */
@import "tailwindcss";
```

```html
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link href="/src/style.css" rel="stylesheet">
</head>
<body>
  <h1 class="text-3xl font-bold underline">
    Hello world!
  </h1>
</body>
</html>
```

## Theme Variables and Customization

Theme variables are special CSS variables defined using the `@theme` directive that generate utility classes. Define custom design tokens to extend or override the default theme.

```css
/* app.css */
@import "tailwindcss";

/* Extend the default theme with custom values */
@theme {
  /* Custom colors create utilities like bg-mint-500, text-mint-500 */
  --color-mint-500: oklch(0.72 0.11 178);
  --color-brand-primary: #3b82f6;

  /* Custom fonts create utilities like font-poppins */
  --font-poppins: Poppins, sans-serif;

  /* Custom breakpoints create variants like 3xl:* */
  --breakpoint-3xl: 120rem;

  /* Custom spacing affects all spacing utilities */
  --spacing: 0.25rem;

  /* Custom shadows create utilities like shadow-soft */
  --shadow-soft: 0 4px 20px rgba(0, 0, 0, 0.08);

  /* Custom animations with keyframes */
  --animate-wiggle: wiggle 1s ease-in-out infinite;

  @keyframes wiggle {
    0%, 100% { transform: rotate(-3deg); }
    50% { transform: rotate(3deg); }
  }
}

/* Override entire namespace with custom-only values */
@theme {
  --color-*: initial;
  --color-white: #fff;
  --color-primary: #3f3cbb;
  --color-secondary: #121063;
}
```

```html
<!-- Using custom theme utilities -->
<div class="bg-mint-500 font-poppins shadow-soft">
  <h1 class="text-brand-primary">Custom themed content</h1>
  <div class="animate-wiggle">Animated element</div>
</div>

<!-- Using theme variables in arbitrary values -->
<div class="bg-[var(--color-mint-500)] p-[var(--spacing)]">
  Using CSS variables directly
</div>
```

## Background Colors

Utilities for controlling an element's background color using the `bg-{color}` pattern with opacity modifiers.

```html
<!-- Basic background colors -->
<button class="bg-blue-500">Blue button</button>
<button class="bg-cyan-500">Cyan button</button>
<button class="bg-pink-500">Pink button</button>

<!-- With opacity modifier (0-100) -->
<button class="bg-sky-500/100">100% opacity</button>
<button class="bg-sky-500/75">75% opacity</button>
<button class="bg-sky-500/50">50% opacity</button>

<!-- Hover state -->
<button class="bg-indigo-500 hover:bg-fuchsia-500">
  Hover to change color
</button>

<!-- Responsive background colors -->
<div class="bg-blue-500 md:bg-green-500 lg:bg-purple-500">
  Changes color at breakpoints
</div>

<!-- Arbitrary values -->
<div class="bg-[#50d71e]">Custom hex color</div>
<div class="bg-[rgb(255,100,50)]">Custom RGB</div>
<div class="bg-(--my-custom-color)">CSS variable reference</div>
```

## Gradients

Create linear, radial, and conic gradients using background image utilities with color stops.

```html
<!-- Linear gradients with direction -->
<div class="bg-linear-to-r from-cyan-500 to-blue-500">Left to right</div>
<div class="bg-linear-to-t from-sky-500 to-indigo-500">Bottom to top</div>
<div class="bg-linear-to-bl from-violet-500 to-fuchsia-500">To bottom-left</div>
<div class="bg-linear-65 from-purple-500 to-pink-500">65 degree angle</div>

<!-- Three-color gradient with via -->
<div class="bg-gradient-to-r from-indigo-500 via-purple-500 to-pink-500">
  Three color stops
</div>

<!-- Gradient stop positions -->
<div class="bg-gradient-to-r from-indigo-500 from-10% via-sky-500 via-30% to-emerald-500 to-90%">
  Custom stop positions
</div>

<!-- Radial gradients -->
<div class="bg-radial from-pink-400 from-40% to-fuchsia-700">Basic radial</div>
<div class="bg-radial-[at_50%_75%] from-sky-200 via-blue-400 to-indigo-900">
  Positioned radial gradient
</div>

<!-- Conic gradients -->
<div class="bg-conic from-blue-600 to-sky-400 to-50%">Basic conic</div>
<div class="bg-conic-180 from-indigo-600 via-indigo-50 to-indigo-600">
  180 degree start angle
</div>

<!-- Interpolation modes -->
<div class="bg-linear-to-r/srgb from-indigo-500 to-teal-400">sRGB</div>
<div class="bg-linear-to-r/oklch from-indigo-500 to-teal-400">OKLCH</div>
<div class="bg-linear-to-r/longer from-indigo-500 to-teal-400">Longer hue</div>
```

## Spacing (Padding and Margin)

Spacing utilities use a multiplier system based on `--spacing` theme variable (default 0.25rem = 4px per unit).

```html
<!-- Padding on all sides: p-{n} where value = n * 0.25rem -->
<div class="p-4">1rem (16px) padding all sides</div>
<div class="p-8">2rem (32px) padding all sides</div>

<!-- Directional padding -->
<div class="pt-6">padding-top: 1.5rem</div>
<div class="pr-4">padding-right: 1rem</div>
<div class="pb-8">padding-bottom: 2rem</div>
<div class="pl-2">padding-left: 0.5rem</div>

<!-- Horizontal and vertical padding -->
<div class="px-8">2rem horizontal padding</div>
<div class="py-4">1rem vertical padding</div>

<!-- Logical properties (RTL support) -->
<div class="ps-8">padding-inline-start: 2rem</div>
<div class="pe-4">padding-inline-end: 1rem</div>

<!-- Margin utilities follow same pattern -->
<div class="m-4">margin all sides</div>
<div class="mx-auto">center horizontally</div>
<div class="mt-8 mb-4">top and bottom margin</div>
<div class="-mt-4">negative margin (overlaps)</div>

<!-- Space between children -->
<div class="space-x-4">Horizontal space between children</div>
<div class="space-y-2">Vertical space between children</div>

<!-- Arbitrary values -->
<div class="p-[5px]">Custom 5px padding</div>
<div class="m-[2.5rem]">Custom 2.5rem margin</div>
```

## Width and Height

Set element dimensions using fixed values, percentages, viewport units, or content-based sizing.

```html
<!-- Fixed width based on spacing scale -->
<div class="w-24">6rem (96px)</div>
<div class="w-48">12rem (192px)</div>
<div class="w-64">16rem (256px)</div>
<div class="w-96">24rem (384px)</div>

<!-- Percentage widths -->
<div class="w-1/2">50%</div>
<div class="w-2/3">66.67%</div>
<div class="w-3/4">75%</div>
<div class="w-full">100%</div>

<!-- Container scale widths -->
<div class="w-xs">20rem (320px)</div>
<div class="w-sm">24rem (384px)</div>
<div class="w-md">28rem (448px)</div>
<div class="w-lg">32rem (512px)</div>
<div class="w-xl">36rem (576px)</div>

<!-- Viewport-based -->
<div class="w-screen">100vw</div>
<div class="w-dvw">100dvw (dynamic viewport)</div>
<div class="w-svw">100svw (small viewport)</div>

<!-- Content-based -->
<div class="w-min">min-content</div>
<div class="w-max">max-content</div>
<div class="w-fit">fit-content</div>

<!-- Height utilities (same patterns) -->
<div class="h-64">Fixed height</div>
<div class="h-full">100% height</div>
<div class="h-screen">100vh</div>
<div class="min-h-screen">Minimum full viewport height</div>

<!-- Set both width and height simultaneously -->
<div class="size-16">4rem width and height</div>
<div class="size-24">6rem width and height</div>
<div class="size-full">100% width and height</div>

<!-- Responsive -->
<div class="w-full md:w-1/2 lg:w-1/3">
  Responsive width
</div>
```

## Flexbox

Create flexible layouts with flexbox utilities for direction, alignment, wrapping, and item sizing.

```html
<!-- Basic flex container -->
<div class="flex">
  <div>Item 1</div>
  <div>Item 2</div>
  <div>Item 3</div>
</div>

<!-- Flex direction -->
<div class="flex flex-row">Horizontal (default)</div>
<div class="flex flex-col">Vertical</div>
<div class="flex flex-row-reverse">Reverse horizontal</div>
<div class="flex flex-col-reverse">Reverse vertical</div>

<!-- Flex wrapping -->
<div class="flex flex-wrap">Wrap items</div>
<div class="flex flex-nowrap">No wrap (default)</div>

<!-- Justify content (main axis) -->
<div class="flex justify-start">Start</div>
<div class="flex justify-center">Center</div>
<div class="flex justify-end">End</div>
<div class="flex justify-between">Space between</div>
<div class="flex justify-around">Space around</div>
<div class="flex justify-evenly">Space evenly</div>

<!-- Align items (cross axis) -->
<div class="flex items-start">Align start</div>
<div class="flex items-center">Align center</div>
<div class="flex items-end">Align end</div>
<div class="flex items-stretch">Stretch (default)</div>
<div class="flex items-baseline">Baseline</div>

<!-- Gap between items -->
<div class="flex gap-4">1rem gap</div>
<div class="flex gap-x-4 gap-y-2">Different x/y gaps</div>

<!-- Flex item sizing -->
<div class="flex">
  <div class="flex-none w-14">Fixed, no grow/shrink</div>
  <div class="flex-1">Grow to fill space</div>
  <div class="flex-1">Grow equally</div>
</div>

<div class="flex">
  <div class="flex-initial w-64">Shrink but don't grow</div>
  <div class="flex-auto">Grow/shrink with initial size</div>
</div>

<!-- Self alignment -->
<div class="flex items-start h-24">
  <div class="self-start">Top</div>
  <div class="self-center">Center</div>
  <div class="self-end">Bottom</div>
  <div class="self-stretch">Stretch</div>
</div>
```

## CSS Grid

Create two-dimensional layouts with grid utilities for columns, rows, gaps, and item placement.

```html
<!-- Basic grid with columns -->
<div class="grid grid-cols-3 gap-4">
  <div>1</div>
  <div>2</div>
  <div>3</div>
  <div>4</div>
  <div>5</div>
  <div>6</div>
</div>

<!-- Different column counts -->
<div class="grid grid-cols-1">1 column</div>
<div class="grid grid-cols-2">2 columns</div>
<div class="grid grid-cols-4">4 columns</div>
<div class="grid grid-cols-12">12 column grid</div>

<!-- Subgrid -->
<div class="grid grid-cols-4 gap-4">
  <div>01</div>
  <div>02</div>
  <div class="col-span-3 grid grid-cols-subgrid gap-4">
    <div class="col-start-2">Subgrid item</div>
  </div>
</div>

<!-- Grid rows -->
<div class="grid grid-rows-3 grid-flow-col">
  Flows into columns, 3 rows
</div>

<!-- Spanning columns/rows -->
<div class="grid grid-cols-6 gap-4">
  <div class="col-span-2">Spans 2 columns</div>
  <div class="col-span-4">Spans 4 columns</div>
  <div class="col-span-full">Spans all columns</div>
</div>

<!-- Column/row start and end -->
<div class="grid grid-cols-6">
  <div class="col-start-2 col-end-5">Columns 2-4</div>
  <div class="col-start-1 col-span-2">Start at 1, span 2</div>
</div>

<!-- Grid placement -->
<div class="grid grid-cols-3 gap-4">
  <div class="justify-self-start">Start</div>
  <div class="justify-self-center">Center</div>
  <div class="justify-self-end">End</div>
</div>

<!-- Responsive grid -->
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
  <div>Responsive grid item</div>
  <div>Responsive grid item</div>
  <div>Responsive grid item</div>
  <div>Responsive grid item</div>
</div>

<!-- Custom column definitions -->
<div class="grid grid-cols-[200px_1fr_100px] gap-4">
  <div>200px</div>
  <div>Flexible</div>
  <div>100px</div>
</div>
```

## Typography

Control font size, weight, family, line height, letter spacing, and text styling.

```html
<!-- Font size with automatic line-height -->
<p class="text-xs">0.75rem (12px)</p>
<p class="text-sm">0.875rem (14px)</p>
<p class="text-base">1rem (16px)</p>
<p class="text-lg">1.125rem (18px)</p>
<p class="text-xl">1.25rem (20px)</p>
<p class="text-2xl">1.5rem (24px)</p>
<p class="text-3xl">1.875rem (30px)</p>
<p class="text-4xl">2.25rem (36px)</p>

<!-- Font size with custom line-height -->
<p class="text-sm/6">14px font, 1.5rem line-height</p>
<p class="text-sm/7">14px font, 1.75rem line-height</p>
<p class="text-lg/8">18px font, 2rem line-height</p>

<!-- Font weight -->
<p class="font-thin">100</p>
<p class="font-light">300</p>
<p class="font-normal">400</p>
<p class="font-medium">500</p>
<p class="font-semibold">600</p>
<p class="font-bold">700</p>
<p class="font-extrabold">800</p>
<p class="font-black">900</p>

<!-- Font family -->
<p class="font-sans">System sans-serif</p>
<p class="font-serif">Serif font</p>
<p class="font-mono">Monospace font</p>

<!-- Text color with opacity -->
<p class="text-gray-900">Dark text</p>
<p class="text-blue-500">Blue text</p>
<p class="text-red-500/75">Red with 75% opacity</p>

<!-- Text alignment -->
<p class="text-left">Left aligned</p>
<p class="text-center">Center aligned</p>
<p class="text-right">Right aligned</p>
<p class="text-justify">Justified text</p>

<!-- Letter and word spacing -->
<p class="tracking-tighter">-0.05em</p>
<p class="tracking-tight">-0.025em</p>
<p class="tracking-normal">0</p>
<p class="tracking-wide">0.025em</p>
<p class="tracking-wider">0.05em</p>

<!-- Line height -->
<p class="leading-tight">1.25</p>
<p class="leading-normal">1.5</p>
<p class="leading-loose">2</p>

<!-- Text decoration -->
<p class="underline">Underlined</p>
<p class="line-through">Strikethrough</p>
<p class="no-underline">No decoration</p>

<!-- Text transform -->
<p class="uppercase">UPPERCASE</p>
<p class="lowercase">lowercase</p>
<p class="capitalize">Capitalize Each Word</p>
<p class="normal-case">Normal case</p>

<!-- Text overflow -->
<p class="truncate">Truncate with ellipsis...</p>
<p class="text-ellipsis overflow-hidden">Ellipsis overflow</p>
```

## Box Shadow

Apply shadows, rings, and inset shadows with color and opacity control.

```html
<!-- Outer shadows -->
<div class="shadow-2xs">Tiny shadow</div>
<div class="shadow-xs">Extra small shadow</div>
<div class="shadow-sm">Small shadow</div>
<div class="shadow-md">Medium shadow</div>
<div class="shadow-lg">Large shadow</div>
<div class="shadow-xl">Extra large shadow</div>
<div class="shadow-2xl">2XL shadow</div>
<div class="shadow-none">No shadow</div>

<!-- Shadow with opacity modifier -->
<div class="shadow-xl">Default opacity (~10%)</div>
<div class="shadow-xl/20">20% opacity</div>
<div class="shadow-xl/50">50% opacity</div>

<!-- Colored shadows -->
<button class="bg-cyan-500 shadow-lg shadow-cyan-500/50">
  Cyan glow
</button>
<button class="bg-blue-500 shadow-lg shadow-blue-500/50">
  Blue glow
</button>
<button class="bg-indigo-500 shadow-lg shadow-indigo-500/50">
  Indigo glow
</button>

<!-- Inset shadows -->
<div class="inset-shadow-2xs">Tiny inset</div>
<div class="inset-shadow-xs">Extra small inset</div>
<div class="inset-shadow-sm">Small inset</div>
<div class="inset-shadow-sm inset-shadow-indigo-500">Colored inset</div>

<!-- Ring (solid shadow) -->
<button class="ring">1px ring</button>
<button class="ring-2">2px ring</button>
<button class="ring-4">4px ring</button>
<button class="ring-2 ring-blue-500">Colored ring</button>
<button class="ring-2 ring-blue-500/50">50% opacity ring</button>

<!-- Inset ring -->
<button class="inset-ring">1px inset ring</button>
<button class="inset-ring-2 inset-ring-blue-500">Colored inset ring</button>

<!-- Focus ring pattern -->
<input class="focus:ring-2 focus:ring-blue-500 focus:outline-none"
       type="text" placeholder="Focus to see ring">

<!-- Combining shadows -->
<div class="shadow-lg inset-shadow-sm ring-1 ring-black/5">
  Multiple shadow effects
</div>
```

## Transitions and Animations

Add smooth transitions and CSS animations with timing control.

```html
<!-- Basic transition -->
<button class="transition hover:bg-indigo-500 hover:scale-110">
  Hover me
</button>

<!-- Transition specific properties -->
<div class="transition-colors hover:bg-blue-500">Colors only</div>
<div class="transition-opacity hover:opacity-50">Opacity only</div>
<div class="transition-shadow hover:shadow-lg">Shadow only</div>
<div class="transition-transform hover:scale-110">Transform only</div>
<div class="transition-all hover:bg-blue-500 hover:scale-110">All properties</div>

<!-- Transition timing -->
<div class="transition duration-150">150ms (default)</div>
<div class="transition duration-300">300ms</div>
<div class="transition duration-500">500ms</div>
<div class="transition duration-1000">1000ms</div>

<!-- Transition delay -->
<div class="transition delay-150">150ms delay</div>
<div class="transition delay-300">300ms delay</div>

<!-- Easing functions -->
<div class="transition ease-linear">Linear</div>
<div class="transition ease-in">Ease in</div>
<div class="transition ease-out">Ease out</div>
<div class="transition ease-in-out">Ease in-out</div>

<!-- Full transition example -->
<button class="bg-blue-500 transition delay-150 duration-300 ease-in-out
               hover:-translate-y-1 hover:scale-110 hover:bg-indigo-500">
  Save Changes
</button>

<!-- Built-in animations -->
<svg class="animate-spin h-5 w-5">Loading spinner</svg>
<span class="animate-ping">Notification ping</span>
<div class="animate-pulse">Skeleton loader</div>
<svg class="animate-bounce">Scroll indicator</svg>

<!-- Reduced motion support -->
<button class="motion-safe:animate-spin">
  Respects prefers-reduced-motion
</button>
<button class="motion-reduce:transition-none motion-reduce:hover:transform-none">
  Disabled animation for reduced motion preference
</button>

<!-- Custom animation with theme -->
<!--
@theme {
  --animate-wiggle: wiggle 1s ease-in-out infinite;
  @keyframes wiggle {
    0%, 100% { transform: rotate(-3deg); }
    50% { transform: rotate(3deg); }
  }
}
-->
<div class="animate-wiggle">Custom wiggle animation</div>
```

## Responsive Design

Apply styles conditionally at different viewport breakpoints using variant prefixes.

```html
<!-- Default breakpoints: sm(640px), md(768px), lg(1024px), xl(1280px), 2xl(1536px) -->

<!-- Mobile-first approach: styles apply at breakpoint and up -->
<div class="w-full md:w-1/2 lg:w-1/3">
  Full width on mobile, half on tablet, third on desktop
</div>

<!-- Responsive grid -->
<div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4">
  <div>Responsive grid item</div>
</div>

<!-- Responsive typography -->
<h1 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl">
  Scales with viewport
</h1>

<!-- Responsive spacing -->
<div class="p-4 sm:p-6 md:p-8 lg:p-12">
  Increasing padding at larger screens
</div>

<!-- Responsive flexbox -->
<div class="flex flex-col sm:flex-row">
  <div>Stacks on mobile, rows on tablet+</div>
</div>

<!-- Hide/show at breakpoints -->
<div class="hidden md:block">Hidden on mobile, visible on tablet+</div>
<div class="block md:hidden">Visible on mobile, hidden on tablet+</div>

<!-- Max-width variants (style applies below breakpoint) -->
<div class="max-sm:text-center">Centered only on small screens</div>
<div class="max-md:flex-col">Column layout only below medium</div>

<!-- Range variants -->
<div class="sm:max-lg:bg-blue-500">Blue only between sm and lg</div>

<!-- Custom breakpoint in theme -->
<!--
@theme {
  --breakpoint-3xl: 120rem;
}
-->
<div class="3xl:grid-cols-6">6 columns at 120rem+</div>
```

## Dark Mode

Apply different styles based on dark mode preference or class-based toggling.

```html
<!-- Automatic dark mode (follows system preference) -->
<div class="bg-white dark:bg-gray-900">
  <p class="text-gray-900 dark:text-gray-100">
    Adapts to system preference
  </p>
</div>

<!-- Common dark mode patterns -->
<div class="bg-white dark:bg-slate-800
            text-slate-900 dark:text-slate-100
            border-gray-200 dark:border-gray-700">
  Card with dark mode support
</div>

<!-- Dark mode with opacity -->
<div class="bg-black/5 dark:bg-white/10">
  Subtle backgrounds
</div>

<!-- Dark mode hover states -->
<button class="bg-gray-100 hover:bg-gray-200
               dark:bg-gray-800 dark:hover:bg-gray-700">
  Button with dark hover
</button>

<!-- Dark mode shadows -->
<div class="shadow-lg dark:shadow-gray-900/50">
  Shadow adapts to dark mode
</div>

<!-- Dark mode rings -->
<button class="ring-gray-300 dark:ring-gray-600">
  Ring color for dark mode
</button>

<!-- Gradient in dark mode -->
<div class="bg-gradient-to-r from-blue-500 to-purple-500
            dark:from-blue-600 dark:to-purple-600">
  Gradient adjusts for dark mode
</div>

<!-- Images in dark mode -->
<img class="dark:brightness-90 dark:contrast-125" src="..." alt="...">
```

## State Variants

Apply styles conditionally based on element state like hover, focus, active, and more.

```html
<!-- Hover state -->
<button class="bg-blue-500 hover:bg-blue-700">Hover me</button>

<!-- Focus state -->
<input class="border focus:border-blue-500 focus:ring-2 focus:ring-blue-500
              focus:outline-none" type="text">

<!-- Focus-visible (keyboard focus only) -->
<button class="focus-visible:ring-2 focus-visible:ring-blue-500">
  Shows ring only on keyboard focus
</button>

<!-- Active state (while pressing) -->
<button class="bg-blue-500 active:bg-blue-800">Click and hold</button>

<!-- Disabled state -->
<button class="bg-blue-500 disabled:bg-gray-300 disabled:cursor-not-allowed" disabled>
  Disabled button
</button>

<!-- Group hover (parent hover affects children) -->
<div class="group">
  <p class="group-hover:text-blue-500">Changes when parent hovered</p>
  <span class="group-hover:underline">Also changes</span>
</div>

<!-- Peer states (sibling affects sibling) -->
<input type="checkbox" class="peer" id="toggle">
<p class="peer-checked:text-blue-500">Changes when checkbox checked</p>

<!-- First/last child -->
<ul>
  <li class="first:pt-0 last:pb-0 py-4">List item</li>
</ul>

<!-- Odd/even rows -->
<tr class="odd:bg-gray-100 even:bg-white">Table row</tr>

<!-- Form validation states -->
<input class="invalid:border-red-500 valid:border-green-500"
       type="email" required>

<!-- Required field indicator -->
<input class="required:border-red-300" type="text" required>

<!-- Placeholder shown -->
<input class="placeholder-shown:border-gray-300" placeholder="Enter text">

<!-- Empty state -->
<div class="empty:hidden">Shows only if has content</div>

<!-- Before/after pseudo-elements -->
<div class="before:content-['*'] before:text-red-500">Required field</div>
<div class="after:content-['_↗'] after:text-blue-500">External link</div>

<!-- Selection styling -->
<p class="selection:bg-blue-500 selection:text-white">
  Select this text
</p>
```

Tailwind CSS v4 is ideal for rapidly building custom user interfaces without leaving your HTML. Its utility-first approach enables consistent design systems, fast prototyping, and production-ready code with minimal CSS. The framework excels in component-based architectures (React, Vue, Svelte) where utility classes can be composed and reused through component abstractions. Dark mode, responsive design, and state variants work together seamlessly to create adaptive experiences.

The CSS-first configuration in v4 using `@theme` makes customization straightforward and keeps all styling concerns in CSS. Design tokens defined as theme variables automatically generate utility classes, enabling teams to maintain consistent spacing, colors, typography, and more across large codebases. The new engine built in Rust provides exceptional build performance, while official plugins for Vite, PostCSS, and CLI ensure integration with any modern development workflow.
