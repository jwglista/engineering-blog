# John's Engineering Blog 🚀

![Typescript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white)
![Astro](https://img.shields.io/badge/Astro-FF5D01?style=for-the-badge&logo=astro&logoColor=white)
![TailwindCSS](https://img.shields.io/badge/TailwindCSS-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)
[![Conventional Commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-%23FE5196?logo=conventionalcommits&logoColor=white&style=for-the-badge)](https://conventionalcommits.org)

A personal blog site to record my findings, thoughts, and experiences around all things related to software engineering, architecture, and building software using AI.

This blog is built with [Astro](https://astro.build/), a modern static site generator with excellent performance and developer experience. Read [the blog posts](./src/data/blog/) for articles on engineering topics.

## ✨ Features

- ⚡ Super fast performance with Astro
- 📱 Responsive design (mobile to desktop)
- ♿ Accessible (Keyboard/VoiceOver support)
- 🔍 SEO-friendly with dynamic OG image generation
- 🌓 Light & dark mode toggle
- 🔎 Fuzzy search across all posts
- 📝 Draft posts & pagination support
- 📡 Sitemap & RSS feed
- 🎨 Customizable TypeScript-based configuration
- 📐 Type-safe Markdown for blog posts

## 📚 Getting Started

### Prerequisites

- Node.js 18+ 
- pnpm (or npm/yarn)

### Installation & Development

```bash
# Install dependencies
pnpm install

# Start development server
pnpm dev
```

The site will be available at `http://localhost:3000`

### Building for Production

```bash
# Build the static site
pnpm build

# Preview the production build locally
pnpm preview
```

## 📝 Writing Blog Posts

Blog posts are stored in `src/data/blog/` as Markdown files. Each post should include front matter with:

```yaml
---
title: "Your Post Title"
description: "Brief description of the post"
pubDatetime: 2026-02-22T10:00:00Z
author: "John Glista"
featured: false
draft: false
tags:
  - engineering
  - software-architecture
---
```

See [src/data/blog/adding-new-post.md](src/data/blog/adding-new-post.md) for detailed instructions.

## 🚀 Project Structure

```bash
/
├── public/              # Static assets
├── src/
│   ├── assets/         # Images and icons
│   ├── components/     # Reusable Astro components
│   ├── data/
│   │   └── blog/       # Blog posts (markdown files)
│   ├── layouts/        # Page templates
│   ├── pages/          # Routes (auto-generated from file structure)
│   ├── scripts/        # Client-side scripts
│   ├── styles/         # Global CSS and typography
│   ├── utils/          # Utility functions
│   ├── config.ts       # Blog configuration
│   ├── constants.ts    # App constants
│   └── content.config.ts # Content management config
├── astro.config.ts     # Astro configuration
└── tsconfig.json       # TypeScript configuration
```

## 💻 Tech Stack

| Category | Technology |
|----------|-----------|
| **Framework** | [Astro](https://astro.build/) |
| **Language** | [TypeScript](https://www.typescriptlang.org/) |
| **Styling** | [TailwindCSS](https://tailwindcss.com/) |
| **Search** | [Pagefind](https://pagefind.app/) |
| **Icons** | [Tabler Icons](https://tabler-icons.io/) |
| **Code Formatting** | [Prettier](https://prettier.io/) |
| **Linting** | [ESLint](https://eslint.org) |
| **Git Commits** | [Commitizen](http://commitizen.github.io/cz-cli/) |

## 🚢 Deployment

This blog can be deployed to any static site host. Popular options include:

- [Cloudflare Pages](https://pages.cloudflare.com/)
- [Vercel](https://vercel.com/)
- [Netlify](https://netlify.com/)
- [GitHub Pages](https://pages.github.com/)

The build is fully static with no server-side dependencies, making it easy to deploy anywhere.

## 📄 License

This project is based on the [AstroPaper](https://github.com/satnaing/astro-paper) theme by [Sat Naing](https://satnaing.dev).

```bash
# pnpm
pnpm create astro@latest --template satnaing/astro-paper

# npm
npm create astro@latest -- --template satnaing/astro-paper

# yarn
yarn create astro --template satnaing/astro-paper

# bun
bun create astro@latest -- --template satnaing/astro-paper
```

Then start the project by running the following commands:

```bash
# install dependencies if you haven't done so in the previous step.
pnpm install

# start running the project
pnpm run dev
```

As an alternative approach, if you have Docker installed, you can use Docker to run this project locally. Here's how:

```bash
# Build the Docker image
docker build -t astropaper .

# Run the Docker container
docker run -p 4321:80 astropaper
```

## Google Site Verification (optional)

You can easily add your [Google Site Verification HTML tag](https://support.google.com/webmasters/answer/9008080#meta_tag_verification&zippy=%2Chtml-tag) in AstroPaper using an environment variable. This step is optional. If you don't add the following environment variable, the google-site-verification tag won't appear in the HTML `<head>` section.

```bash
# in your environment variable file (.env)
PUBLIC_GOOGLE_SITE_VERIFICATION=your-google-site-verification-value
```

> See [this discussion](https://github.com/satnaing/astro-paper/discussions/334#discussioncomment-10139247) for adding AstroPaper to the Google Search Console.

## 🧞 Commands

All commands are run from the root of the project, from a terminal:

> **_Note!_** For `Docker` commands we must have it [installed](https://docs.docker.com/engine/install/) in your machine.

| Command                              | Action                                                                                                                           |
| :----------------------------------- | :------------------------------------------------------------------------------------------------------------------------------- |
| `pnpm install`                       | Installs dependencies                                                                                                            |
| `pnpm run dev`                       | Starts local dev server at `localhost:4321`                                                                                      |
| `pnpm run build`                     | Build your production site to `./dist/`                                                                                          |
| `pnpm run preview`                   | Preview your build locally, before deploying                                                                                     |
| `pnpm run format:check`              | Check code format with Prettier                                                                                                  |
| `pnpm run format`                    | Format codes with Prettier                                                                                                       |
| `pnpm run sync`                      | Generates TypeScript types for all Astro modules. [Learn more](https://docs.astro.build/en/reference/cli-reference/#astro-sync). |
| `pnpm run lint`                      | Lint with ESLint                                                                                                                 |
| `docker compose up -d`               | Run AstroPaper on docker, You can access with the same hostname and port informed on `dev` command.                              |
| `docker compose run app npm install` | You can run any command above into the docker container.                                                                         |
| `docker build -t astropaper .`       | Build Docker image for AstroPaper.                                                                                               |
| `docker run -p 4321:80 astropaper`   | Run AstroPaper on Docker. The website will be accessible at `http://localhost:4321`.                                             |

> **_Warning!_** Windows PowerShell users may need to install the [concurrently package](https://www.npmjs.com/package/concurrently) if they want to [run diagnostics](https://docs.astro.build/en/reference/cli-reference/#astro-check) during development (`astro check --watch & astro dev`). For more info, see [this issue](https://github.com/satnaing/astro-paper/issues/113).

## ✨ Feedback & Suggestions

If you have any suggestions/feedback, you can contact me via [my email](mailto:contact@satnaing.dev). Alternatively, feel free to open an issue if you find bugs or want to request new features.

## 📜 License

Licensed under the MIT License, Copyright © 2025

---

Made with 🤍 by [Sat Naing](https://satnaing.dev) 👨🏻‍💻 and [contributors](https://github.com/satnaing/astro-paper/graphs/contributors).
