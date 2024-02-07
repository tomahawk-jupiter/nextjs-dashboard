# Nextjs Dashboard - [A Tutorial](https://nextjs.org/learn)

These are my notes from following the tutorial.

## Table of Contents

- [Packages](#packages)
- [0. Things I Like and Learnt](#0-things-i-like-and-learnt)
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
  - [Why optimize images?](#why-optimize-images)
  - [The `<Image>` Component](#the-image-component)
  - [Adding the desktop and mobile hero images](#adding-the-desktop-and-mobile-hero-images)
- [4. Creating Layouts and Pages](#4-creating-layouts-and-pages)
  - [Nested Routing](#nested-routing)
  - [layout files](#layout-files)
- [5. Navigation Between Pages](#5-navigation-between-pages)
  - [Automatic code-splitting and prefetching](#automatic-code-splitting-and-prefetching)
  - [Pattern: Showing active links](#pattern-showing-active-links)
- [6. Setting Up Your Database](#6-setting-up-your-database)
  - [Create a Postgres database](#create-a-postgres-database)
  - [Seed your database with mock data](#seed-your-database-with-mock-data)
  - [Explore your database](#explore-your-database)
- [7. Fetching Data](#7-fetching-data)
  - [API Layer](#api-layer)
  - [Database queries](#database-queries)
  - [Server Components](#server-components)
  - [Using SQL](#using-sql)
  - [Fetching data for the dashboard overview page](#fetching-data-for-the-dashboard-overview-page)
  - [Request Waterfalls](#request-waterfalls)
  - [Parallel data fetching](#parallel-data-fetching)
- [8. Static and Dynamic Rendering](#8-static-and-dynamic-rendering)
  - [Static Rendering](#static-rendering)
  - [Dynamic Rendering](#dynamic-rendering)
  - [Making the dashboard dynamic](#making-the-dashboard-dynamic)
  - [Slow data fetch](#slow-data-fetch)
- [9. Streaming](#9-streaming)
  - [What is streaming](#what-is-streaming)
  - [Streaming a whole page with `loading.tsx`](#streaming-a-whole-page-with-loading-tsx)
  - [Loading skeleton](#loading-skeleton)
  - [Route groups](#route-groups)
  - [Streaming a component](#streaming-a-component)
  - [Grouping Components](#grouping-components)
  - [Deciding on where to place your Suspense boundaries](#deciding-on-where-to-place-your-suspense-boundaries)
- [10. Partial Prerendering (experimental feature)](#10-partial-prerendering-experimental-feature)
  - [Combining Static and Dynamic Content](#combining-static-and-dynamic-content)
  - [What is Partial Prerendering](#what-is-partial-prerendering)
  - [How does Partial Prerendering work?](#how-does-partial-prerendering-work)
- [Summary: Data Fetching Optimizing](#summary-data-fetching-optimizing)
- [11. Adding Search and Pagination](#11-adding-search-and-pagination)
  - [Why use URL Serach params](#why-use-url-serach-params)
  - [Adding the Search functionality](#adding-the-search-functionality)
  - [1. Capture users input](#1-capture-users-input)
  - [2. Update the URL with the search params](#2-update-the-url-with-the-search-params)
  - [3. Keeping the URL and input in sync](#3-keeping-the-url-and-input-in-sync)
  - [4. Updating the Table](#4-updating-the-table)
  - [Best practice: Debouncing](#best-practice-debouncing)
  - [Adding Pagination](#adding-pagination)
- [12. Mutating Data: Part 1](#12-mutating-data-part-1)
  - [What are Server Actions?](#what-are-server-actions)
  - [Using Server Actions](#using-server-actions)
  - [1. Create a new route and form](#1-create-a-new-route-and-form)
  - [2. Create a Server Action](#2-create-a-server-action)
  - [3. Extract the data from `formData`](#3-extract-the-data-from-formdata)
  - [4. Validate and prepare the data](#4-validate-and-prepare-the-data)
  - [5. Insert data into your database](#5-insert-data-into-your-database)
  - [6. Revalidate and redirect](#6-revalidate-and-redirect)
- [12. Mutating Data: Part 2 updating and deleting an invoice](#12-mutating-data-part-2-updating-and-deleting-an-invoice)
  - [UPDATE an invoice](#update-an-invoice)
  - [1. Create a Dynamic Route Segment with the invoice `id`](#1-create-a-dynamic-route-segment-with-the-invoice-id)
  - [2. Read the invoice `id` from page `params`](#2-read-the-invoice-id-from-page-params)
  - [3. Fetch the specific invoice](#3-fetch-the-specific-invoice)
  - [4. Pass the `id` to the Server Action](#4-pass-the-id-to-the-server-action)
  - [DELETE an invoice](#delete-an-invoice)
- [13. Handling Errors](#13-handling-errors)
  - [Adding `try/catch` to Server Actions](#adding-try-catch-to-server-actions)
  - [Handling all errors with `error.tsx`](#handling-all-errors-with-error-tsx)
  - [Handling 404 errors with the `notFound` function](#handling-404-errors-with-the-notfound-function)
- [14. Improving Accessibility & Form Validation](#14-improving-accessibility-form-validation)
  - [What is accessibility?](#what-is-accessibility)
  - [ESLint accessibility plugin](#eslint-accessibility-plugin)
  - [Improving form accessibility](#improving-form-accessibility)
  - [Client-Side validation](#client-side-validation)
  - [Server-Side validation](#server-side-validation)
  - [Challenge: add form validation to `edit-form.tsx`](#challenge-add-form-validation-to-edit-form-tsx)
- [15. Adding Authentication](#15-adding-authentication)
  - [Authentication vs Authorization](#authentication-vs-authorization)
  - [Create the login route](#create-the-login-route)
  - [Setting up NextAuth.js](#setting-up-nextauth-js)
  - [Protecting routes with Nextjs Middleware](#protecting-routes-with-nextjs-middleware)
  - [Adding the Credentials provider](#adding-the-credentials-provider)
  - [Adding the sign in functionality](#adding-the-sign-in-functionality)
  - [Updating the login form](#updating-the-login-form)
  - [Adding the logout functionality](#adding-the-logout-functionality)
- [16. Adding Metadata](#16-adding-metadata)
  - [Types of metadata](#types-of-metadata)
  - [Adding metadata](#adding-metadata)
  - [Add title and description](#add-title-and-description)
  - [metadata `title.template`](#metadata-titletemplate)

## Packages

- [clsx](https://www.npmjs.com/package/clsx): library to toggle class names
- [use-debounce](https://www.npmjs.com/package/use-debounce): stop too many requests happing by delaying
- [Zod](https://zod.dev/): Typescript first validation library

## 0. Things I Like and Learnt

File structure ideas. Eg. UI components in a folder then seperated by route. Buttons kept in a single file.

PostGres database with nextjs.

It has a great example of a filterable search and of pagination. The search uses debouncing to stop a request on every key stroke in the input.

It has bread crumbs example. Form with dynamic options.

Its got loading skeletons that use Reacts Suspense.

Route groups: folder name not part of route.

SearchParams vs Params: SearchParams are from URL query strings `invoice?id=123`. Params are from the route `invoice/123/`, also known as path variables or parameters.

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

By having a special name for page files, Nextjs allows you to colocate UI components, test files, and other related code with your routes. Only the `page` file will be publicly accessible. Eg. `/ui` and `/lib` folders are colocated inside the `/app` folder.

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

### Create a Postgres database

NOTE: there are other database intergrations available (including mongodb).

After deploying to vercel, click continue to dashboard. Then `Storage Tab -> Connect Store -> Create New -> Postgres -> Continue`. Keep the region as the default setting so its in the same region as application code.

Then navigate to the `.env.local` tab, click `Show secret` and `Copy Snippet`, reveal before copying them.

These are the Environment variables needed to connect to your database. Put them in a `.env` file and make sure that file name is in the `.gitignore` (IMPORTANT!).

Finally, run `npm i @vercel/postgres` in your terminal to install the [Vercel Postgres SDK](https://vercel.com/docs/storage/vercel-postgres/sdk).

### Seed your database with mock data

In `/scripts` folder provided in starter code theres a file called `seed.js`. This script will create and seed the `invoices`, `customers`, `user`, and `revenue` tables.

NOTE: this file is good to look at to see how to run queries on the database.

You can add a command in the package.json for running this seed script:

`"seed": "node -r dotenv/config ./scripts/seed.js"`

Explanation:

- `node`: Executes a JavaScript file using the Node.js runtime.
- `-r dotenv/config`: Preloads the dotenv module and configures it to read environment variables from a .env file.
- `./scripts/seed.js`: Specifies the path to the JavaScript file that should be executed.

This command can now be run with: `npm run seed`. If it works you'll see some messages in the terminal.

### Explore your database

You can look at your database in the `Data` tab (within the Storage main tab).

You can browse or run queries.

#### Running queries

You can type standard SQL commands, eg `DROP TABLE customers`, **be careful**, this command will delete the whole customer table.

Heres a query example (it just selects so its safe):

```sql
SELECT invoices.amount, customers.name
FROM invoices
JOIN customers ON invoices.customer_id = customers.id
WHERE invoices.amount = 666;
```

You will see the result.

## 7. Fetching Data

### API Layer

You will want to use an API if you want to keep something private from the client, like your database secrets.

Nextjs lets you create API endpoints using [Route Handlers](https://nextjs.org/docs/app/building-your-application/routing/route-handlers).

### Database queries

You need to interact with your database with SQL or use an ORM (object relational mapping) like [Prisma](https://www.prisma.io/). This is done in the API endpoints.

> **What is an ORM?**
>
> An ORM (Object-Relational Mapping) is a programming technique that allows developers to interact with a relational database using an object-oriented approach. It maps database tables to classes, rows to objects, and columns to object attributes, simplifying database operations in object-oriented programming languages. This abstraction enables developers to work with databases using familiar programming paradigms, reducing the need for writing complex SQL queries directly.

You don't need an API layer when using React Server Components because they won't expose secrets to the client.

### Server Components

By default Nextjs uses React server components, you have to explicitly say when you want to use a client component.

The benefits to Server Components are:

- They support promises so you can use `async/await` syntax without having to use `useEffect`, `useState` or data fetching libraries.
- You can keep expensive data fetches and logic on the server and send result to client.
- Don't need an API layer.

### Using SQL

This tutorial will use SQL (not an ORM) to write queries using the Vercel Postgres SDK. Why?

- SQL is industry standard and is what an ORM uses under the hood.
- It will help to understand the fundamentals of relational databases.
- SQL is versatile, you can fetch and manipulate data.
- Vercel Postgres SDK provides protection against SQL injections (IMPORTANT SECURITY).

Look at `/app/lib/data.ts`. This is where the data queries are kept for this application. You can import them where needed.

The `sql` function from `@vercel/postgres` is used to run queries on the database. It can be used in any Server Component, but for this tutorial its all kept together.

### Fetching data for the dashboard overview page

`/app/dashboard/page.tsx`

- This page is an `async` component, this allows the use of `await` to fetch data.
- Thre are 3 components which receive data: `<Card>`, `<RevenueChart>` and `<LatestInvoices>`.

#### RevenueChart

The data is fetched with `const revenue = await fetchRevenue();` and passed as a prop to the `<RevenueChart>` which creates a simple but pleasant looking data viz using just plain javascript and tailwind.

#### LatestInvoices

Its better, when dealing with potentially large data, to sort/filter using SQL queries rather than fetching it all and using javascript.

In this case, we select the last 5 invoices. This is the query from `/app/lib/data.ts`

```ts
// Fetch the last 5 invoices, sorted by date
const data = await sql<LatestInvoiceRaw>`
  SELECT invoices.amount, customers.name, customers.image_url, customers.email
  FROM invoices
  JOIN customers ON invoices.customer_id = customers.id
  ORDER BY invoices.date DESC
  LIMIT 5`;
```

The data is passed to the `<LatestInvoices>` UI component.

#### Card

There are 4 `<Card>` components that display different data.

There are two things to be aware of in our app so far:

1. The data requests are unintentionally blocking each other, creating a request waterfall
2. By default, Nextjs **prerenders** routes to improve permormance, this is called **Static Rendering**. If the data changes, this won't show up in our dashboard. This is covered in next chapter.

### Request Waterfalls

A **waterfall** refers to a sequence of network requests that depend on the completion of previous requests. In the case of data fetching, each request can only begin once previous one has returned data.

This isn't necessarily bad, you may want waterfalls because you want a condition to be satisfied before you make the next request. Eg. you might need to fetch some data to use in a query for the next request, like a list of friend ids from a user profile which is then used to get the friend profiles.

Sometimes though, you don't want this behaviour as it can impact performance.

### Parallel data fetching

Waterfalls can be avoided by making requests in parallel.

JavaScript has the `Promise.all()` or `Promise.allSettled()` functions for this purpose.

There is an example of this in `/app/lib/data.js` in the `fetchCardData()` function.

Using native javaScript means it can be used in any library or framework.

There is a disadvantage though, what if one of the requests is slower than all the others?

## 8. Static and Dynamic Rendering

### Static Rendering

Data fetching and rendering happens on the server at build time when you deploy or when you [revalidate](https://nextjs.org/docs/app/building-your-application/data-fetching/fetching-caching-and-revalidating#revalidating-data).

The result is then cached and this is what is served to users. The benefits are:

- Faster websites
- Reduced Server Load: the server doesn't have to dynamically generate content for each user request
- SEO: prerendered content is easier for search engine crawlers to index

Static rendering is good for UI with no data or data that is shared across users, like a blog post or product page. Its not so good for personalized dashboards or anything that regularly updates.

### Dynamic Rendering

This is the opposite of Static rendering. The content is rendered on the server for each user at request time. The benefits are:

- Real-time data: data that changes frequently
- User-specific content: personalized content like dashboards and profiles, and data that updates on user interaction
- Request-time information: info that can only be known at request time, like cookies or URL search params

### Making the dashboard dynamic

By default `@vercel/postgres` doesn't set its own caching semantics. This allows the framework to set its own static and dynamic behaviour.

Theres a Nextjs API called `unstable_noStore`, it can be used in your Server Components or data fetching functions to opt out of static rendering.

In `/app/lib/data.ts`, import it and call it at the top (inside) of your data fetching functions:

```ts
import { unstable_noStore as noStore } from 'next/cache';

export async function fetchRevenue() {
  // Add noStore() here to prevent the response from being cached.
  // This is equivalent to in fetch(..., {cache: 'no-store'}).
  noStore();

  // ...
}
```

NOTE: `unstable_noStore` is an experimental API and may change. There is a stable one [Segment Config Option](https://nextjs.org/docs/app/api-reference/file-conventions/route-segment-config) `export const dynamic = "force-dynamic"`. You put that at the top of the file.

### Slow data fetch

Now the other problem. What if one of the data requests is slower than the others?

You can simulate a slow request by putting the following before the sql database query in the `fetchRevenue` function in `data.ts`:

```ts
console.log('Fetching revenue data...');
await new Promise((resolve) => setTimeout(resolve, 3000));
```

This illustrates a common problem developers have to solve:

With dynamic rendering, your application is only as fast as your slowest data fetch.

## 9. Streaming

### What is streaming

Its a data transfer technique that allows you to break down a route into smaller "chunks" and progressively stream them from the server to the client as they become ready.

By streaming, you can prevent slow data requests from blocking your whole page. The user can see and interact with parts of the page without waiting for all the data to load.

Streaming works well with React's component model, as each component can be considered a chunk.

There are two ways to implement streaming in Nextjs:

1. At the page level, with the `loading.tsx` file
2. For specific components, with `<Suspense>`

### Streaming a whole page with `loading.tsx`

In `/app/dashboard` create a file called `loading.tsx`.

What this does:

1. `loading.tsx` is a special Nextjs file built on stop of `Suspense`. It allows you to create a fallback UI to show while the page is loading
2. Since the `<SideNav>` is static, its shown immediately and can be interacted with
3. The user doesn't have to wait for the page to finish loading before navigating away, this is called `interuptable navigation`

### Loading skeleton

This is a simplified version of the UI used as a placeholder (or fallback) to indicate to the user that content is loading.

Any UI you embed into `loading.tsx` will be embedded as part of the static file and sent first. Then the rest of the dynamic content will be streamed from the server to the client.

Since this file is a level higher than `/invoices/page.tsx` and` /customers/page.tsx`, it will apply to those pages too. We don't want that so...

### Route groups

You can make the `loading.tsx` apply to only the page on the same level by putting it in a folder together with the page. You use parenthesis when naming the folder, this will stop it from affecting the URL route.

So you have `/dashboard/(overview)/loading.tsx` and `/dashboard/(overview)/page.tsx`.

This is called a route group. Its a way to organize files into logical groups without affecting the URL structure.

You can also use route groups to separate your application into sections to keep it organized eg. (marketing) routes and (shop) routes, or by teams for larger applications.

### Streaming a component

So far we stream a whole page. We can be mor granular and stream specific components using React Suspense.

**Suspense** allows you to defer rendering parts of your app until some codition is met (eg. data is loaded).

You can wrap your **dynamic components** in Suspense, then pass it a fallback component to show while it loads.

We can demo this with our intentionally slowed down request that is slowing down our page load.

To do this we need to move the data fetch to the component rather than fetching in the page and passing it to the component as a prop.

The data fetch function is `fetchRevenue` and the component is `revenue-chart.tsx`.

Then in `dashboard/(overview)/page.tsx` wrap the `<RevenueChart>` with `<Suspense>` imported from `'react'`. Pass your component skeleton to Suspense as a prop.

```tsx
import { Suspense } from 'react';
import { RevenueChartSkeleton } from '@/app/ui/skeletons';
```

```tsx
<Suspense fallback={<RevenueChartSkeleton />}>
  <RevenueChart /> {/* the data is fetched in this component */}
</Suspense>
```

Now if you refresh the page, the other components will load in and the skeleton is shown for the one with the delay until its ready.

Now do the same for `<LatestInvoices />`, I also added an artificial delay in the fetch function.

### Grouping Components

Now for the `<Card />` components, we don't want to individually load those in because these will lead to a _popping_ effect as they load in which can be visually jarring.

Instead we put the individual card components together into a component called `<CardWrapper>` (the file is called `cards.tsx`).

Then we can wrap this with the `<Suspense>` and pass a skeleton for the cards.

We treat the cards and one thing in terms of loading them in.

This is useful when we want to load things in at the same time.

### Deciding on where to place your Suspense boundaries

This depends on a few things:

1. How you want the user to experience the page as it streams
2. What content to prioritize
3. If the components rely on data fetching

Its generally good practice to move your data fetches down to the components that need it, then wrap those components in Suspense.

But you can also do it in sections or as a whole page, whatever you think is best.

## 10. Partial Prerendering (experimental feature)

NOTE: introduced in Nextjs 14. May change.

### Combining Static and Dynamic Content

Currently, if you call a dynamic function inside your route, eg. `noStore()`, `cookies()`, etc, your entire route becomes dynamic.

This is how most apps are built today. You choose between static or dynamic rendering for your entire app or for a specific route.

However, most routes are not fully static or dynamic.

In our dashboard the SideNav can be static because it doesn't rely on any data and is not personalized to the user. The rest of the dashboard relies on data so is dynamic.

### What is Partial Prerendering

It combines static and dynamic in the same route. NOTE: Its currently experimental.

- A static route shell is served, for a fast initial load.
- The shell leaves holes where dynamic content will load in asynchronously.
- The async holes are streamed in parellel, reducing overal load time of the page.

Partial Prerendering may become the default for web apps in the future because it has the best of both.

### How does Partial Prerendering work?

It leverages **Reacts Concurrent APIs** and uses **Suspense** to defer rendering parts of your app unitil some condition is met.

The fallback is embedded into the initial static file along with other static content. At build/revalidation the static parts are prerendered and the rest is postponed until the user requests the route.

Note that wrapping a component in Suspense doesn't make the component itself dynamic, we used the `unstable_noStore` to achieve that, rather Suspense is used as a boundary between the static and dynamic parts of your route.

Partial Prerendering doesn't require any changes to your code, as long as your using Suspense to wrap dynamic parts, Nextjs will know which parts of a route are static and dynamic.

NOTE: learn more about how to configure [Partial Prerendering (experimental) documentation](https://nextjs.org/docs/app/api-reference/next-config-js/partial-prerendering).

Remember, its experimental and not ready for production.

## Summary: Data Fetching Optimizing

To recap, you've done a few things to optimize data fetching in your application, you've:

1. Created a database in the same region as your application code to reduce latency between your server and database.
1. Fetched data on the server with React Server Components. This allows you to keep expensive data fetches and logic on the server, reduces the client-side JavaScript bundle, and prevents your database secrets from being exposed to the client.
1. Used SQL to only fetch the data you needed, reducing the amount of data transferred for each request and the amount of JavaScript needed to transform the data in-memory.
1. Parallelize data fetching with JavaScript - where it made sense to do so.
1. Implemented Streaming to prevent slow data requests from blocking your whole page, and to allow the user to start interacting with the UI without waiting for everything to load.
1. Move data fetching down to the components that need it, thus isolating which parts of your routes should be dynamic in preparation for Partial Prerendering.

## 11. Adding Search and Pagination

We will move onto the `/invoices` page to learn how to use Nextjs APIs:

- `searchParams`
- `usePathname`
- `useRouter`

Your search functionality will span the client and the server. When a user searches for an invoice on the client, the URL params will be updated, data will be fetched on the server, and the table will re-render on the server with the new data.

### Why use URL Serach params

Using this pattern has some benefits:

- **Bookmarkable and Shareable URLs**: Since the search parameters are in the URL, users can bookmark the current state of the application, including their search queries and filters, for future reference or sharing.
- **Server-Side Rendering and Initial Load**: URL parameters can be directly consumed on the server to render the initial state, making it easier to handle server rendering.
- **Analytics and Tracking**: Having search queries and filters directly in the URL makes it easier to track user behavior without requiring additional client-side logic.

### Adding the Search functionality

The hooks we'll use:

- `useSearchParams` - Allows you to access the parameters of the current URL. For example, the search params for this URL /dashboard/invoices?page=1&query=pending would look like this: {page: '1', query: 'pending'}.
- `usePathname` - Lets you read the current URL's pathname. For example, for the route /dashboard/invoices, usePathname would return '/dashboard/invoices'.
- `useRouter` - Enables navigation between routes within client components programmatically. There are multiple methods you can use.

Here's a quick overview of the implementation steps:

1. Capture the user's input.
2. Update the URL with the search params.
3. Keep the URL in sync with the input field.
4. Update the table to reflect the search query.

### 1. Capture users input

In `/app/ui/search.tsx`, `use client` makes it a client component so you can use event listeners and hooks.

There is an input element and witch onChange listener. We don't need to use `useState` to handle the input state because we'll be storing it in the URL.

### 2. Update the URL with the search params

The hook `useSearchParams` is used together with the `URLSearchParams` Web API that provides utility methods for manipulating thr URL query parameters (ie. it helps write the query string).

Create a new `URLSearchParams` instance and pass it a variable that has `useSearchParams()` assigned to it. Do that inside the onChange handler function.

The `params` instance you created has a method `.set()` and `.delete()` for adding removing params to/from the query string.

Now we have the query string, we can use the Nextjs `useRouter` and `usePathname` hooks to update the URL.

use the `replace` method from useRouter `const { replace } = useRouter()`, `pathname` is the current path, in this case its `/dashboard/invoices`.

Use it to create the URL with the query:

```tsx
replace(`${pathname}?${params.toString}`);
```

This is all done in the onChange handler.

The URL is updated without reloading the page, thanks to Nextjs client-side navigation from [5. Navigation Between Pages](#5-navigation-between-pages).

You will see the URL change as you type in the input element.

### 3. Keeping the URL and input in sync

To ensure the input field is in sync with the URL and will be populated when sharing, you can pass a defaultValue to input by reading from searchParams:

`defaultValue={searchParams.get('query')?.toString()}` this is an attribute of the input element.

> **Why we don't need `useState`**
>
> `defaultValue` vs. `value` / Controlled vs. Uncontrolled
>
> If you're using state to manage the value of an input, you'd use the value attribute to make it a controlled component. This means React would manage the input's state.
>
> However, since you're not using state, you can use defaultValue. This means the native input will manage its own state. This is okay since you're saving the search query to the URL instead of state.

### 4. Updating the Table

Nextjs page files/components can accept props to get the URL [file conventions page.js](https://nextjs.org/docs/app/api-reference/file-conventions/page).

We use a prop `{ searchParams }` to get the parameters out of the URL query string. We can then pass them to our components, in this case to the `<Table>`.

Table is a `Server Component` so we can call one of our database query functions directly inside this component and pass the values from the query string to that function `fetchFilteredInvoices`.

Now the Table that shows invoices will be filterable, it filters as you type. The SQL `ILIKE` is used to achieve this.

NOTE: this is querying the database with every keystroke, we tackle that with debouncing (next section).

> **When to use the `useSearchParams()` hook vs. the `searchParams` prop?**
>
> You might have noticed you used two different ways to extract search params. Whether you use one or the other depends on whether you're working on the client or the server.
>
> - `<Search>` is a Client Component, so you used the useSearchParams() hook to access the params from the client.
> - `<Table>` is a Server Component that fetches its own data, so you can pass the searchParams prop from the page to the component.
>
> As a general rule, if you want to read the params from the client, use the useSearchParams() hook as this avoids having to go back to the server.

### Best practice: Debouncing

**Debouncing** is a programming practice that limits the rate at which a function can fire. In our case, you only want to query the database when the user has stopped typing.

How Debouncing Works:

1. **Trigger Event**: When an event that should be debounced (like a keystroke in the search box) occurs, a timer starts.
2. **Wait**: If a new event occurs before the timer expires, the timer is reset.
3. **Execution**: If the timer reaches the end of its countdown, the debounced function is executed.

You can implement debouncing in a few ways, including manually creating your own debouncing function.

We'll keep it simple and use a library called `use-debounce`.

We use it in the `app/ui/search.tsx`, we wrap our handleSearch with the debounce function. This will make it so that the code will only run after the user stopped typing for 300ms. The timer is reset when user presses another key.

This will reduce the number of requests sent to the database, saving resources.

### Adding Pagination

We have a `<Pagination>` component in `/invoices/page.tsx`.

We fetch the data in the `page` because its a Server component and pass it to `Pagination` which is a client component.

We use `fetchInvoicesPages()` which takes the query string value. It then queries the database and works out how many pages are needed. It does this by looking at the `ITEMS_PER_PAGE` variable, which is also used in the `fetchFilteredInvoices` function.

This will give the number of pages needed to display the data, which we pass to `<Pagination >`.

We'll use `usePathname` and `useSearchParams` similar to how we did in the search section previously. We'll write a function `createPageURL`.

```tsx
const createPageURL = (pageNumber: number | string) => {
  const params = new URLSearchParams(searchParams);
  params.set('page', pageNumber.toString());
  return `${pathname}?${params.toString()}`;
};
```

The page number in the URL needs to be set to 1 when the user types in the search (this is done in `search.tsx`), otherwise it will stay on the last number selected which will stop it working properly.

## 12. Mutating Data: Part 1

### What are Server Actions?

React Server Actions allow you to run asynchronous code directly on the server, this eliminates the need to create API endpoints to mutate your data.

You write async functions that execute on the server and can be invoked from your Client or Server Components.

Server actions offer an effective security solution, protecting against different types of attacks, securing your data, and ensuring authorized access. Server Actions achieve this through techniques like POST requests, encrypted closures, strict input checks, error message hashing, and host restrictions, all working together to significantly enhance your app's safety.

#### Using forms with Server Actions

In React you can use the `action` attribute in the `<form>` element to invoke actions.

The action will automatically recieve the native `formData` object.

An advantage of invoking a Server Action within a Server Component is progressive enhancement - forms work even if JavaScript is disabled on the client.

Nextjs integrates Server Actions with Nextjs [caching](https://nextjs.org/docs/app/building-your-application/caching).

When a form is submitted through a Server Action, you can use APIs like `revalidatePath` and `revalidateTag`.

### Using Server Actions

We'll add the ability to create a new invoice in our application. These are the steps:

1. Create a form to capture the user's input.
2. Create a Server Action and invoke it from the form.
3. Inside your Server Action, extract the data from the formData object.
4. Validate and prepare the data to be inserted into your database.
5. Insert the data and handle any errors.
6. Revalidate the cache and redirect the user back to invoices page.

### 1. Create a new route and form

This file/route: `/app/dashboard/invoices/create/page.tsx`, will be used to create new invoices.

Clicking the `Create Invoice` button on the `/invoices` page goes to this page.

Its a Server Component that contains a `<Breadcrumbs>` component and a `<Form>`, both from `ui/invoices/`.

The form has a `<select>` which uses the list of customers as options.

### 2. Create a Server Action

Our Server Action will be called when the form is submitted.

We'll write it in `/lib/actions.ts`. Put `'use server'` at the top and this will mark all functions exported from this file as Server Functions.

These functions can then be imported into Client or Server components.

```ts
'use server';

export async function createInvoice(formData: FormData) {}
```

NOTE: You can also write Server Actions directly inside Server Components by adding `'use server'` inside the action. In this project, we'll keep them together in their own file.

This `createInvoice` action/function can now be imported into the `create-form` file/component. Call this functionin the forms `action` attribute: `<form action={createInvoice}>`.

> **Good to know**
>
> In HTML, you'd pass a URL to the `action` attribute for where to submit the form, usually an API endpoint.
>
> In React, the `action` attribute is considered a special prop, React builds on top of it to allow actions to be invoked.
>
> Behind the scenes, Server Actions create a `POST` API endpoint. This is why you don't need to create API endpoints manually when using Server Actions.

### 3. Extract the data from `formData`

[FormData MDN docs](https://developer.mozilla.org/en-US/docs/Web/API/FormData/append)

We want to shape our formData into an object to make it easier to work with.

In `actions.ts`, extract the values of formData. Theres a `.get(name)` method:

```js
const rawFormData = {
  customerId: formData.get('customerId'),
  amount: formData.get('amount'),
  status: formData.get('status'),
};
```

TIP: If you're working with forms that have many fields, you may want to consider using the `entries()`
method with JavaScript's `Object.fromEntries()`. For example:

```js
const rawFormData = Object.fromEntries(formData.entries());
```

### 4. Validate and prepare the data

Before sending the form data to our the database, we should ensure it's in the correct format and the correct types (because its coming from client).

`/app/lib/definitions.ts` has a type definition for an `Invoice`.

#### Type validation and coercion

We use a TypeScript-first validation library called `zod`.

We use `zod` to define a schema that matches the shape of our form object. We do this in `/app/lib/actions.ts`.

The schema will validate our data. We can set our schema to coerce data to the type we want.

NOTE: even though the input element for `amount` was a number type, it will be sent as a string. This is normal for data from web forms.

NOTE: it's best to store money values in cents/pents in the database to eliminate JavaScript floating-point errors.

#### Creating new dates

Create a new date with the format "YYYY-MM-DD" for the invoice's creation date:

```js
const date = new Date().toISOString().split('T')[0];
```

NOTE: the `T` splits the date and time parts, we keep just the date.

### 5. Insert data into your database

We can create an SQL query to insert the new invoice into our database. We can do this right inside our Server Action.

NOTE: not yet handling errors, we do that later.

### 6. Revalidate and redirect

Nextjs has a [Client-side Router Cache](https://nextjs.org/docs/app/building-your-application/caching#router-cache) that stores the route segments in the user's browser for a time. Along with `prefetching`, this cache ensures quick navigation between routes while reducing the number of requests made to the server.

Since we are updating the data displayed in the `invoices` route, we need to clear this cache and trigger a new request to the server using `revalidatePath`.

```js
import { revalidatePath } from 'next/cache';
revalidatePath('/dashboard/invoices');
```

We put this after the database query that adds the new invoice. Fresh data will be fetched from the server.

After that, we redirect the user back to the invoices page, otherwise it would remain on the create invoice page.

```js
redirect('/dashboard/invoices');
```

You should be able to add new invoices now.

## 12. Mutating Data: Part 2 updating and deleting an invoice

### UPDATE an invoice

This will be similar to creating an invoice except we need to pass the invoice `id`.

These are the steps you'll take to update an invoice:

1. Create a new dynamic route segment with the invoice id.
2. Read the invoice id from the page params.
3. Fetch the specific invoice from your database.
4. Pre-populate the form with the invoice data.
5. Update the invoice data in your database.

### 1. Create a Dynamic Route Segment with the invoice `id`

You can create dynamic route segments by wrapping a folder's name in square brackets. For example, `[id]`, `[post]` or `[slug]`.

Example in `/ui/invoices/[id]/edit/page.tsx`.

In `/ui/invoices/table.tsx`, there is a button component `<UpdateInvoice>` that receives an invoice id.

This button is a Nextjs `<Link>` component. Use the invoice id in the href, giving a URL for an individual invoice page.

```jsx
href={`/dashboard/invoices/${id}/edit`}
```

### 2. Read the invoice `id` from page `params`

In `/ui/invoices/[id]/edit/page.tsx`, there is a `<Form>` from `edit-form.tsx`. It needs some data so it can populate the form elements with `defaultValue`'s, as its an edit form.

In addition to `searchParams` (which is for query string data), page components also accept a prop called `params`, which is for path variables/parameters.

```tsx
export default async function Page({ params }: { params: { id: string } }) {
  const id = params.id;
  // ...
}
```

### 3. Fetch the specific invoice

There are functions for fetching the data we need from the database.

```tsx
import { fetchInvoiceById, fetchCustomers } from '@/app/lib/data';
```

We can fetch in parallel.

```tsx
const [invoice, customers] = await Promise.all([
  fetchInvoiceById(id),
  fetchCustomers(),
]);
```

NOTE: `UUIDs` used for ids instead of incrementing keys, to eliminate the risk of id collision.

### 4. Pass the `id` to the Server Action

You want to pass the `id` to the Server Action so you can update the right record in the database.

You cannot pass `id` as an argument:

```tsx
// Passing an id as argument won't work
<form action={updateInvoice(id)}>
```

Instead you use JS `bind`. This will ensure that values passed to the Server Action are encoded.

The invoice id is attached to the `updateInvoice` action. This is done in `edit-form.tsx`.

```ts
const updateInvoiceWithId = updateInvoice.bind(null, invoice.id);
```

NOTE: a hidden input in the form will also work `<input type="hidden">` but this will expose the value in the HTML source which is not good for sensitive data like ids.

The server action is added to `/app/lib/actions.ts` and is called `updateInvoice`.

It receives the formData and the id that was bound to the action.

This is what it does:

1. Extracting the data from formData.
2. Validating the types with Zod.
3. Converting the amount to cents.
4. Passing the variables to your SQL query.
5. Calling revalidatePath to clear the client cache and make a new server request.
6. Calling redirect to redirect the user to the invoice's page.

### DELETE an invoice

To use a Server Action on the delete button, wrap it with a `<form>` element. In `/ui/invoices/buttons.tsx`.

Import the `deleteInvoice` action and `bind` the `id` to it. The id is passed as a prop to the button.

The action uses the id in an `sql` query to delete an invoice from the database.

Then `revalidatePath(/dashboard/invoices)` is called. This will trigger a new server request. We don't need to call `redirect` here because the action is being called in the path that is being revalidated.

Further reading: [security with Server Actions](https://nextjs.org/blog/security-nextjs-server-components-actions)

## 13. Handling Errors

### Adding `try/catch` to Server Actions

We add `try/catch` to server actions, put the database queries inside them.

`redirect()` must be called after the try/catch.

We want to show errors to users.

### Handling all errors with `error.tsx`

The `error.tsx` file can be used to define a UI boundary for a route segment.

It serves as a catch-all for unexpected errors and allows you to display a fallback UI to your users.

See `/dashboard/invoices/error.tsx`.

Notice that:

- Its a `use client` component
- It accepts two props
  - `error`: a native javascript `Error` object
  - `reset`: this is a function to reset the error boundary. When executed it will try to re-render the route segment.

### Handling 404 errors with the `notFound` function

While the `error.tsx` is useful for a catch-all, `noteFound` can be used when you try to fetch a resource that doesn't exist.

For example try to search for a fake invoice UUI `http://localhost:3000/dashboard/invoices/2e94d1ed-d220-449f-9f11-f0bbceed9645/edit`.

The `error.tsx` page will kick in because the example is a child route of `/invoices` where the `error.tsx` is defined.

We can use `notFound` to be more specific. Do this in `/dashboard/invoices/[id]/edit/page.tsx`.

```tsx
import { notFound } from 'next/navigation';
```

Check to see if the `invoice` is empty, this is the result of the `fetchInvoiceById` request. If its empty, call `notFound()`.

Create a file `not-found.tsx` inside the `edit` folder.

This will be the page shown when `notFound()` in executed.

NOTE: `noteFound` takes precedence over `error.tsx`.

Further reading: [error handling](https://nextjs.org/docs/app/building-your-application/routing/error-handling)

## 14. Improving Accessibility & Form Validation

### What is accessibility?

Web apps that everyone can use, ie. people with disabilities.

Recomended course for further reading [Learn Accessibility](https://web.dev/learn/accessibility/)

### ESLint accessibility plugin

By default, Next.js includes the eslint-plugin-jsx-a11y
plugin to help catch accessibility issues early.

Add `"lint": "next lint"` in the scripts section of `package.json`.

Use it with `npm run lint` to see lint warnings.

NOTE: `next lint` runs as part of the build process when you deploy to Vercel and shows in logs. Run it locally first to catch them before you deploy.

### Improving form accessibility

There are three things we already are doing to improve form accessibility:

- Semantic HTML: eg. using the correct elements instead of just using div
- Labelling: Using `<label>` and `htmlFor`
- Focus Outline: Fields are properly styled to show an outline when they are in focus, ie. when tabbing through elements.

### Client-Side validation

The simplest way to do this is with the input validation built into the browser. Add the `required` attribute to the input and select elements, this will stop empty fields being sent to server and give the user a message.

There are other input validation attributes too.

### Server-Side validation

Validating forms on the server means you can:

- Make sure data is in the expected format before sending it to your database
- Reduce risk of malicious users bypassing client-side validation
- Have one source of truth for what is considered valid data

We start in `create-form.tsx`.

We import `useFormState` hook from `react-dom`. Since this is a hook, we need to turn our form into a Client Component `use client`.

`useFormState`:

- Takes two arguments: `(action, initialState)`.
- Returns two values: `[state, dispatch]` - the form state, and a dispatch function (similar to useReducer)

```tsx
const initialState = { message: null, errors: {} };
const [state, dispatch] = useFormState(createInvoice, initialState);
```

`createInvoice` is the action we pass to it and it returns `dispatch` which we use in the form action: `<form action={dispatch}>` instead of `createInvoice` directly.

In `action.ts` file, use `zod` to validate the form data.

```ts
const FormSchema = z.object({
  id: z.string(),
  customerId: z.string({
    invalid_type_error: 'Please select a customer.',
  }),
  amount: z.coerce
    .number()
    .gt(0, { message: 'Please enter an amount greater thatn $0' }),
  status: z.enum(['pending', 'paid'], {
    invalid_type_error: 'Please select an invoice status.',
  }),
  date: z.string(),
});
```

Error messages can be included. Eg.

- `customerId` must be a string, so cant be empty, and we add an error message.
- `amount` we add a condition where the value must be greater than 0.

Next, update `createInvoice` action

```ts
// This is temporary until @types/react-dom is updated
export type State = {
  errors?: {
    customerId?: string[];
    amount?: string[];
    status?: string[];
  };
  message?: string | null;
};

export async function createInvoice(prevState: State, formData: FormData) {
  // ...
}
```

- `formData` - same as before.
- `prevState` - contains the state passed from the useFormState hook. You won't be using it in the action in this example, but it's a required prop.

Change zod `parse()` to `safeParse()`. This will return `success` or `error` field. This will help handle validation more gracefully without having to put this logic inside the `try/catch` block.

Before sending the info to the database, check if the form fields were validated correctly with a conditional.

if `validateFields` fails, return errors and message.

```ts
// Before //
// const { customerId, amount, status } = CreateInvoice.parse({
//   customerId: formData.get('customerId'),
//   amount: formData.get('amount'),
//   status: formData.get('status'),
// });

const validatedFields = CreateInvoice.safeParse({
  customerId: formData.get('customerId'),
  amount: formData.get('amount'),
  status: formData.get('status'),
});

// If form validation fails, return errors early. Otherwise, continue.
if (!validatedFields.success) {
  return {
    errors: validatedFields.error.flatten().fieldErrors,
    message: 'Missing Fields. Failed to Create Invoice.',
  };
}

// Prepare data for insertion into the database
const { customerId, amount, status } = validatedFields.data;
```

#### Display form errors

We can display the errors in the form component `create-form.tsx`. Access the errors using the form `state`.

```tsx
<select
  aria-describedby="customer-error"
  // ...
>

<div id="customer-error" aria-live="polite" aria-atomic="true">
  {state.errors?.customerId &&
    state.errors.customerId.map((error: string) => (
      <p className="mt-2 text-sm text-red-500" key={error}>
        {error}
      </p>
    ))}
</div>
```

Aria label explanation:

- `aria-describedby="customer-error"` this establishes a relationship between the `select` element and the error message container. Screen readers will read this description when user interacts with the select box.
- `id="customer-error"` this id uniquely identifies the html element that holds the error message so it can establish relationship with the `aria-describedby`.
- `aria-live="polite"` politely notifies user of error, when user corrects content/error, they are notified.

### Challenge: add form validation to `edit-form.tsx`

If you'd like to challenge yourself, take the knowledge you've learned in this chapter and add form validation to the edit-form.tsx component.

You'll need to:

- Add `useFormState` to your `edit-form.tsx` component.
- Edit the `updateInvoice` action to handle validation errors from Zod.
- Display the errors in your component, and add aria labels to improve accessibility.

[See solution](https://nextjs.org/learn/dashboard-app/improving-accessibility#practice-adding-aria-labels)

## 15. Adding Authentication

https://nextjs.org/learn/dashboard-app/adding-authentication

- Email: user@nextmail.com
- Password: 123456

### Authentication vs Authorization

Authentication is about making sure the user is who they say they are, eg. with a username & password.

Authorization is the next step, deciding what parts of the application they are allowed to use.

### Create the login route

`/app/login/page.tsx`

This contains the `<LoginForm />`

### Setting up NextAuth.js

[NextAuth.js](https://authjs.dev/reference/nextjs)

Using this abstracts away much of the complexity involved in managing sessions, sign in/out, etc.

#### 1. Install

`npm install next-auth@beta`

The `beta` version is compatible with Nextjs 14.

#### 2. Generate secret key

This is used to encrypt cookies, ensuring security of user sessions.

`openssl rand -base64 32`

#### 3. Add key to .env

`AUTH_SECRET=your-secret-key`

NOTE: this env var needs to be added to Vercel for production version to work.

#### 4. authConfig: pages option

Create an `auth.config.ts` file at the root of our project that exports an `authConfig` object. This object will contain the configuration options for NextAuth.js. For now, it will only contain the `pages` option:

```ts
import type { NextAuthConfig } from 'next-auth';

export const authConfig = {
  pages: {
    signIn: '/login',
  },
};
```

The `pages` option specifies the route for custom sign-in, sign-out, and error pages. Its not required, but by adding `singIn: '/login'` to the `pages` option, the user will be redirected to our custom login page, rather than the NextAuth.js default page.

### Protecting routes with Nextjs Middleware

[nextjs middleware](https://nextjs.org/docs/app/building-your-application/routing/middleware)

The logic to protect routes. In this case, it protects the dashboard routes unless they are logged in.

This is added to the `authConfig.ts`:

```ts
import type { NextAuthConfig } from 'next-auth';

export const authConfig = {
  pages: {
    signIn: '/login',
  },
  callbacks: {
    authorized({ auth, request: { nextUrl } }) {
      const isLoggedIn = !!auth?.user;
      const isOnDashboard = nextUrl.pathname.startsWith('/dashboard');
      if (isOnDashboard) {
        if (isLoggedIn) return true;
        return false; // Redirect unauthenticated users to login page
      } else if (isLoggedIn) {
        return Response.redirect(new URL('/dashboard', nextUrl));
      }
      return true;
    },
  },
  providers: [], // Add providers with an empty array for now
} satisfies NextAuthConfig;
```

Explanation:

The `authorized` callback is used to verify if the request is authorized to access a page via Nextjs middleware.

It is called before a request is completed and it receives an object with the `auth` and `request` properties.

The `auth` property contains the user's session, and the `request` property contains the incoming request.

The `providers` options is an array where you list different login options. For now its an emtpy array to satisfy the config. We'll add to it in `Adding the Credentials provider` section.

#### Import authConfig object into Middleware file

Do this in the root of your project. Create `middleware.ts` with:

```ts
import NextAuth from 'next-auth';
import { authConfig } from './auth.config';

export default NextAuth(authConfig).auth;

export const config = {
  // https://nextjs.org/docs/app/building-your-application/routing/middleware#matcher
  matcher: ['/((?!api|_next/static|_next/image|.*\\.png$).*)'],
};
```

Here you're initializing NextAuthjs with the `authConfig` object and exporting the `auth` property.

Also we're using the `matcher` option from Middleware to specify that it should run on specific paths.

The advantage of employing Middleware for this task is that the protected routes will not even start rendering until the Middleware verifies the authentication, enhancing both security and performance of your application.

#### Password hashing

`bcrypt` is used to hash passwords before storing in the database. This adds some security if the user's data is exposed.

In `seed.js` file, it is used to hash user's password. We will use it again in this chapter to compare the saved password with the entered password.

We need a seperate file to use `bcrypt` because it relies on Nodejs APIs not available in Nextjs Middleware.

Create `auth.ts` (in root of project) that spreads your `authConfig` object:

```ts
import NextAuth from 'next-auth';
import { authConfig } from './auth.config';

export const { auth, signIn, signOut } = NextAuth({
  ...authConfig,
});
```

### Adding the Credentials provider

Add the `providers` option for NextAuthjs. Its an array where you list different login options such as Google or GitHub.

We will focus on [Credentials provider](https://authjs.dev/getting-started/providers/credentials-tutorial).

This is username/password.

```ts
// auth.ts
import NextAuth from 'next-auth';
import { authConfig } from './auth.config';
import Credentials from 'next-auth/providers/credentials';

export const { auth, signIn, signOut } = NextAuth({
  ...authConfig,
  providers: [Credentials({})],
});
```

NOTE: its generally recommended to use alternate providers such as OAuth or email. Username/password has inherent security risks and additionl complexity. eg. forgotton password.

- [OAuth](https://authjs.dev/getting-started/providers/oauth-tutorial)
- [Email](https://authjs.dev/getting-started/providers/email-tutorial)
- [NextAuthjs docs](https://authjs.dev/getting-started/providers)

Email is where a link is sent to users email and they click on it to sign up automatically. This is good to include in addition to OAuth in case they lose access to their OAuth account.

### Adding the sign in functionality

All the following is in `auth.ts`.

You can use `authorize` function to handle the authentication logic.

Similar to Server Actions, you can use `zod` to validate the email and password before checking if the user exists in the database.

After validating the credentials, create a new `getUser` function that queries the user from the database.

Then, call `bcrypt.compare` to check if the passwords match.

NOTE: the salt used when originally hashing the password in part of the hashed password, bcrypt handles this for you so you don't need to add the salt when using `.compare`.

If they match return the user, otherwise return `null` to prevent user from logging in.

### Updating the login form

You need to connect the auth logic with your login form.

Create a new action in `actions.ts` file. Call it `authenticate`. It should import the `signIn` function from `auth.ts`:

```ts
import { signIn } from '@/auth';
import { AuthError } from 'next-auth';

// ...

export async function authenticate(
  prevState: string | undefined,
  formData: FormData,
) {
  try {
    await signIn('credentials', formData);
  } catch (error) {
    if (error instanceof AuthError) {
      switch (error.type) {
        case 'CredentialsSignin':
          return 'Invalid credentials.';
        default:
          return 'Something went wrong.';
      }
    }
    throw error;
  }
}
```

If there's a `CredentialsSignin` error, you want to show an appropriate error message.

You can learn about NextAuthjs errors in the [documentation](https://errors.authjs.dev/).

Finally, in the `login-form.tsx` component, you can use React's `useFormDatate` to call the server action and handle form errors, and use `useFormStatus` to handle the pending state of the form.

```tsx
import { useFormState, useFormStatus } from 'react-dom';
import { authenticate } from '@/app/lib/actions';

export default function LoginForm() {
  const [errorMessage, dispatch] = useFormState(authenticate, undefined);

  return (
    <form action={dispatch} className="space-y-3">

    {/* ... */}

      <LoginButton />
      <div
        className="flex h-8 items-end space-x-1"
        aria-live="polite"
        aria-atomic="true"
      >
        {errorMessage && (
          <>
            <ExclamationCircleIcon className="h-5 w-5 text-red-500" />
            <p className="text-sm text-red-500">{errorMessage}</p>
          </>
        )}
      </div>
    </form>
  )
```

### Adding the logout functionality

To add the logout functionality to `<SideNav />`, call the `signOut` function from `auth.ts` in your `<form>` element.

In `/ui/dashboard/sidenav.tsx`:

```
import { signOut } from '@/auth';

// ..

<form
  action={async () => {
    'use server';
    await signOut();
  }}
>

// ..
```

#### Try it out

Now the `/dashboard` route will be unaccessible unless logged in. It will take you to the `/login` page.

- Email: user@nextmail.com
- Password: 123456

## 16. Adding Metadata

Metadata is information is crucial for search engines and other systems that need to understand your webpage's content better.

### Types of metadata

Title, description and keywords are common types.

- Title: the title shown in the browser tab.
- Description: brief overview of a webpage, often displayed in the search engine results.
- Keywords: helps search engines index the page.

#### Favicon

Small icon displayed in address bar or tab.

```html
<link rel="icon" href="path/to/favicon.ico" />
```

#### Open Graph Metadata

This metadata enhances the way a webpage is represented when shared on social media platforms, providing information such as the title, description, and preview image.

```html
<meta property="og:title" content="Title Here" />
<meta property="og:description" content="Description Here" />
<meta property="og:image" content="image_url_here" />
```

### Adding metadata

Nextjs has a Metadata API. There are two ways to add metadata:

#### 1. Config-based

Export a [static metadata object](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#metadata-object) or a dynamic [generateMetadata function](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#generatemetadata-function)

#### 2. File-based

Nextjs has a range of special files that are specifically used for metadata purposes:

- `favicon.ico`, `apple-icon.jpg` and `icon.jpg`: For favicons and icons
- `opengraph-image.jpg` and `twitter-image.jpg`: For social media images
- `robots.txt`: instructions for search engine crawling
- `sitemap.xml`: Info about the websites structure

NOTE: these files go in the root level of `/app` folder?

Whichever way you use, nextjs will automatically generate the relevant `<head>` elements for your pages.

NOTE: You can create dynamic OG images using the [ImageResponse](https://nextjs.org/docs/app/api-reference/functions/image-response) constructor.

### Add title and description

[metadata object docs](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#metadata-fields)

You can put metadata in any `layout.js` or `page.js` file.

Metadata in `layout.js` will be inherited by any page that uses it.

Metadata in nested pages will override the metadata in the parent.

#### Example

In `/app/layout.tsx`:

```tsx
import { Metadata } from 'next';

export const metadata: Metadata = {
  title: 'Acme Dashboard',
  description: 'The official Next.js Course Dashboard, built with App Router.',
  metadataBase: new URL('https://next-learn-dashboard.vercel.sh'),
};

export default function RootLayout() {
  // ...
}
```

NOTE: [`metadataBase`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#metadatabase) is a convenience option to set a base URL prefix for `metadata` fields that require a fully qualified URL. It has a default value.

And in `/app/dashboard/invoices/page.tsx`:

```tsx
import { Metadata } from 'next';

export const metadata: Metadata = {
  title: 'Invoices | Acme Dashboard',
};
```

This title will be used, ie. it overrides the layout metadata title.

Theres a better way to add the title using...

### metadata `title.template`

We are repeating the title of the application on every page eg. `Acme Dashboard` and `Invoices | Acme Dashboard`.

This might be used for the company/brand name for the website.

If we wanted to change the app title `Acme Dashboard`, we would currently have to do this on every page.

We can use the `template` field in the metadata object:

```tsx
import { Metadata } from 'next';

export const metadata: Metadata = {
  title: {
    template: '%s | Acme Dashboard',
    default: 'Acme Dashboard',
  },
  description: 'The official Next.js Learn Dashboard built with App Router.',
  metadataBase: new URL('https://next-learn-dashboard.vercel.sh'),
};
```

The `%s` in the template will be replaced with the specific page title.

QUESTION: can `title.template` be nested? Eg. to achieve breadcrumb style page names. Or is that too much anyway?

#### Practice: Adding metadata

Now that you've learned about metadata, practice by adding titles to your other pages:

1. `/login` page.
2. `/dashboard/` page.
3. `/dashboard/customers` page.
4. `/dashboard/invoices/create` page.
5. `/dashboard/invoices/[id]/edit` page.

[Page Top](#table-of-contents)
