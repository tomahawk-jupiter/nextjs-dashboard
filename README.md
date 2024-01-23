# Nextjs Dashboard - [A Tutorial](https://nextjs.org/learn)

## Table of Contents

- [1. Getting Started](#1-getting-started)
  - [Run Project](#run-project)
  - [Project folder structure](#project-folder-structure)
- [2. CSS Styling](#2-css-styling)
  - [Global Styles](#global-styles)
  - [Tailwind](#tailwind)
  - [CSS Modules](#css-modules)
  - [Using `clsx` library to toggle class names](#using-clsx-library-to-toggle-class-names)
- [3. Optimizing Fonts and Images](#3-optimizing-fonts-and-images)
  - [Adding a Primary Font](#adding-a-primary-font)
  - [Add another font](#add-another-font)
  - [Why optimize images?](#why-optimize-images-)
  - [The `<Image>` Component](#the-image-component)
  - [Adding the desktop and mobile hero images](#adding-the-desktop-and-mobile-hero-images)
- [4. Creating Layouts and Pages](#4-creating-layouts-and-pages)
  - [Nested Routing](#nested-routing)
  - [layout files](#layout-files)
- [5. Navigation Between Pages](#5-navigation-between-pages)
  - [Automatic code-splitting and prefetching](#automatic-code-splitting-and-prefetching)
  - [Pattern: Showing active links](#pattern-showing-active-links)
- [6. Setting Up Your Database](#6-setting-up-your-database)

## 1. Getting Started

### Run Project

```sh
npm i # might not be needed
npm run dev
```

### Project folder structure

- `/app`: Contains all the routes, components, and logic for your application, this is where you'll be mostly working from.
- `/app/lib`: Contains functions used in your application, such as reusable utility functions and data fetching functions.
- `/app/ui`: Contains all the UI components for your application, such as cards, tables, and forms. To save time, we've pre-styled these components for you.
- `/public`: Contains all the static assets for your application, such as images.
- `/scripts`: Contains a seeding script that you'll use to populate your database in a later chapter.
- Config Files: You'll also notice config files such as next.config.js at the root of your application. Most of these files are created and pre-configured when you start a new project using create-next-app. You will not need to modify them in this course.

## 2. CSS Styling

There are three common ways to style a nextjs project:

1. Global stylesheet
2. TailwindCSS
3. CSS Modules

NOTE: you can use Tailwind and CSS Modules in the same project.

### Global Styles

The global style sheet is in `app/ui/global.css`. Its best to import it into the top level component of your project, which is `app/layout.tsx`.

### Tailwind

The `global.css` file contains `tailwind` directives:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

These are needed to make tailwindCSS work (if using). When creating a new nextjs project, it will ask if you want to use tailwind.

### CSS Modules

CSS Modules are another way you can style with. You create a `myfile.module.css` file and you can create styled classes that you can add to your components elements.

`home.module.css`

```css
.shape {
  color: blue;
  /* other styles... */
}
```

`page.tsx`

```tsx
import styles from '@/app/home.module.css';

<div className={styles.shape}></div>;
```

### Using `clsx` library to toggle class names

Use it to conditionally apply a style based on the state of a prop passed to the component. It is useful for when there are multiple conditions/styles.

```tsx
import clsx from 'clsx';

export default function InvoiceStatus({ status }: { status: string }) {
  return (
    <span
      className={clsx(
        'inline-flex items-center rounded-full px-2 py-1 text-sm',
        {
          'bg-gray-100 text-gray-500': status === 'pending',
          'bg-green-500 text-white': status === 'paid',
        },
      )}
    >
    // ...
)}
```

## 3. Optimizing Fonts and Images

Fonts loading can cause content shift because the fallback/system font is used until the specified font is loaded via a network request.

Nextjs optimizes fonts when you use `next/font` module. It downloads fonts at build time and hosts them with your other static assets (no additional network requests).

### Adding a Primary Font

Create a file called `fonts.ts` to keep your fonts in. Put it in `/app/ui`. Fonts are imported from the `next/font/google` module.

**`/app/ui/fonts.ts`**

```ts
import { Inter } from 'next/font/google';

export const inter = Inter({ subsets: ['latin'] });
```

**`/app/layout.ts`**

```tsx
import '@/app/ui/global.css';
import { inter } from '@/app/ui/fonts';

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body className={`${inter.className} antialiased`}>{children}</body>
    </html>
  );
}
```

Adding it to the body element makes this font the default project wide. Tailwind `antialiased` will smooth out the font (it blends the text and background pixels), it's not necessary but looks nice.

### Add another font

Look at google fonts site to see what is possible for each font, ie. font weights. You can add like so.

```ts
export const lusitana = Lusitana({
  weight: ['400', '700'],
  subsets: ['latin'],
});
```

You can apply this font just like before, but on single elements where you want it instead of on the body element.

### Why optimize images?

Nextjs can serve static assets, like images, under the `public` folder.

With regular html you would do:

```html
<img src="/hero.png" />
```

But this means you'd have to manually:

- Ensure your image is responsive on different screen sizes.
- Specify image sizes for different devices.
- Prevent layout shift as the images load.
- Lazy load images that are outside the user's viewport.

Image Optimization is a large topic, it could be considered a specialization in itself. The `next/image` component optimizes iamges for you.

### The `<Image>` Component

The `<Image>` Component is an extension of the HTML `<img>` tag, and comes with automatic image optimization, such as:

- Preventing layout shift automatically when images are loading.
- Resizing images to avoid shipping large images to devices with a smaller viewport.
- Lazy loading images by default (images load as they enter the viewport).
- Serving images in modern formats, like WebP and AVIF, when the browser supports it.

### Adding the desktop and mobile hero images

```tsx
import Image from 'next/image';

<Image
  src="/hero-desktop.png"
  width={1000}
  height={760}
  className="hidden md:block"
  alt="Screenshots of the dashboard project showing desktop version"
/>;
```

You don't include `/public/` in the file path for assets in the `public` folder.

Set the `width` and `height` to prevent layout shift, should be an aspect ratio identical to the source image.

Notice the class `hidden` to remove the image from the DOM and `md:block` which will show the image on desktop screens (`md:` is a medium breakpoint).

And the mobile Image:

```tsx
<Image
  src="/hero-mobile.png"
  width={560}
  height={620}
  className="block md:hidden"
  alt="Screenshot of the dashboard project showing mobile version"
/>
```

## 4. Creating Layouts and Pages

### Nested Routing

In NextJS any folder nested in the `app` folder that contains a `page.tsx` file will be accessible in your application. `page.tsx` is a special file that exports a React component.

Eg. `/app/page.tsx` will be the base level page of your application ie. `www.yoursite.com/`. And a nested route `/app/dashboard/page.tsx` will be served for route `www.yoursite.com/dashboard`.

Each folder/route can also have its own `layout.tsx` file. The layout will be applied to every page nested in the route. They are useful for menus.

By having a special name for page files, Nestjs allows you to colocate UI components, test files, and other related code with your routes. Only the `page` file will be publicly accessible. Eg. `/ui` and `/lib` folders are colocated inside the `/app` folder.

### layout files

It takes pages or another layout component as props. The benefit to using layouts in Nextjs is that on navigation, only the page components update, the layout won't re-render. This is called [partial rendering](https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#3-partial-rendering).

**Root layout** is required and is shared by all pages. Use it to modify your `<html>` and `<body>` tags, and add metadata.

## 5. Navigation Between Pages

Traditionally `<a>` elements are used for navigation. This will result in a full page refresh.

Nextjs has the `<Link>` element that allows for client-side navigation with javascript.

### Automatic code-splitting and prefetching

Nextjs will code split your app by route segments. This is different to traditional React single page applications where the browser loads all the code on initial load.

Splitting code by routes means that pages become isolacted and if a page throws an error, the rest of the app will still work.

In production, Nextjs will prefetch the code for routes in Link elements in the background so when user clicks it will already be ready.

### Pattern: Showing active links

A common UI pattern is to show an active link for the current page. To so this you need to get the user's current path from the URL.

There is a hook called `usePathname()` for this purpose. This can only be used in `client components`, put `'use client';` at the top of of the file (this is a React directive).

The `clsx` library can be used to conditionally apply classnames for styling.

## 6. Setting Up Your Database

We will use `@vercel/postgres` which is a PostgresSQL database.

First, push project to github. Then deploy using vercel (theres a free hobby plan).
