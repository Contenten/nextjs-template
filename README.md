# nextjs template

I have already created a nextjs template with shadcn,and picked up some basic functionality of the website of https://ui.shadcn.com

Such as: 
- design and layout
- Dark mode
- `⌘ K`
- mdx with contentlayer

Since the template was not clean, I decided to make a new one from scratch for sharing and deploy it to multiple platforms with SSG.

## create project and migrate codebase from https://github.com/shadcn-ui/ui

clone the website repo of shadcn for reference

```sh
git clone https://github.com/shadcn-ui/ui --depth 1
```

create-next-app

```sh
npx create-next-app@latest
```

## deploy to multi platforms with SSG

To make same code deployed in these three platforms below, I have done some compat logic in `next.config.js` with environment variable

### cloudflare pages

Build command

```sh
npx tsx --tsconfig ./tsconfig.scripts.json ./src/scripts/build-registry.mts && npx next build
```

**Environment Variable**

- NODE_VERSION=20.18.0
- PLATFORM=cloudflare pages


### github pages

rename `src/components/icons.tsx` to another name, e.g. `src/components/my-icons.tsx`

**Environment Variable**

`PLATFORM=github pages` has been written in `yml` file of github workflow


### vercel

Build command

```sh
tsx --tsconfig ./tsconfig.scripts.json ./src/scripts/build-registry.mts && next build
```

**Environment Variable**

PLATFORM=vercel

## branch management

- main branch is for the basic functionalities of the website, and share reusable code cross projects derived from this template.Furthermore, this branch is used for synchronizing the design system with shadcn-ui.

- dynamic-config branch is for the dynamic configuration, especially for routes and metadata. For example, I will use doc page to display the blog post, the route should not be named as `/docs/[slug]`, but `/blogs/[slug]` instead for clarity.
