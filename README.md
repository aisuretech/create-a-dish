# Create A Dish AI Recipe Generator and Culinary Learning Platform

Create A Dish is a React and TypeScript web app for home cooks, food learners, and recipe explorers who want personalized meal ideas and practical cooking guidance.

It combines AI-assisted recipe generation, popular recipe discovery, cocktail browsing, and SEO-ready learning pages (dietary guides, global cuisine, kitchen toolkit, and culinary glossary) using React Router, Material UI, and static pre-rendering scripts.

## Live Demo
- Production: https://createadish.com

<!-- Use absolute production URLs for README images (https://...), not relative paths. -->
![Create A Dish homepage preview](https://althistai.aisuretech.com/images/recipe-da7f7a56.png)

## Why This Project Is Discoverable on GitHub
- Targets clear search intent with keywords like AI recipe generator, meal planning app, dietary guide, and cocktail explorer in page metadata and route content.
- Ships pre-rendered static HTML and sitemap generation, improving crawlability for SPA routes and popular recipe pages.
- Organizes educational content into dedicated routes for major diets and cooking references, increasing long-tail topic coverage.
- Uses a practical, reproducible build workflow (prebuild, build, postbuild) that developers can run locally and in CI.

## Table of Contents
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Quick Start](#quick-start)
- [Project Structure](#project-structure)
- [Environment Variables](#environment-variables)
- [Architecture](#architecture)
- [Learning Modules](#learning-modules)
- [Deployment](#deployment)
- [SEO and Performance](#seo-and-performance)
- [Screenshots](#screenshots)
- [Use Cases](#use-cases)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [FAQ](#faq)
- [Suggested GitHub Topics](#suggested-github-topics)
- [Links](#links)
- [License](#license)

## Features

### For Learners
- Generate personalized recipes by selecting meal type, cuisine, ingredients, dietary preferences, and cooking methods.
- Explore 12 dietary guide pages (Mediterranean, Keto, Vegan, Low-FODMAP, and more) with SEO-focused educational content.
- Browse a curated cocktail dataset with category, alcoholic type, and ingredient-based exploration.
- Discover cooking references through kitchen toolkit, global cuisine, and culinary glossary pages.

### For Developers
- TypeScript React SPA architecture with context-based state management and modular hooks.
- API-integrated recipe generation, recipe retrieval, ratings support, and popular recipe prefetch pipeline.
- SEO automation with prebuild data fetching, route-level metadata injection, static page generation, and sitemap output.
- Vercel-ready deployment setup with build command and rewrite rules for SPA routing.

## Tech Stack
- Frontend: React 19, TypeScript, React Router, Material UI, Emotion, React Helmet Async
- Runtime/Platform: Node.js with Create React App tooling, Vercel deployment target
- Analytics and Monitoring: Web Vitals reporting (no dedicated third-party analytics SDK configured in this repository)
- Testing: Jest + React Testing Library (@testing-library/react, jest-dom, user-event)
- PWA: Web App Manifest, theme metadata, static assets, robots.txt, sitemap.xml

## Quick Start

### Prerequisites
- Node.js 18+ and npm
- Access to recipe API endpoints (or defaults for local testing)

### Install and Run
```bash
npm install
npm start
```

Open http://localhost:3000

### Build and Validate
```bash
npm run build:static
npm test -- --watchAll=false
```

## Project Structure
```text
createadishcom/
├── src/
│   ├── screens/                # Route screens (landing, composer, recipe, resource pages)
│   ├── screens/diets/          # 12 dietary sub-pages
│   ├── hooks/                  # Auth, cocktails, rating hooks
│   ├── context/                # Recipe state and mode context
│   ├── utils/                  # API integration utilities
│   └── components/             # Shared UI components
├── scripts/
│   ├── prebuildFetchData.js    # Fetches popular recipes before build
│   ├── generateStaticPages.js  # Injects SEO metadata and writes static route HTML
│   └── generateSitemap.js      # Generates sitemap.xml from static and recipe routes
├── public/
│   ├── data/                   # Cocktail dataset for client-side explorer
│   ├── prebuild-data/          # Generated prebuild JSON
│   └── sitemap.xml             # Generated sitemap for local/public serving
├── build/                      # Production build output (including prerendered routes)
├── docs/                       # Documentation and SEO implementation notes
└── package.json                # Scripts and dependencies
```

## Environment Variables
Create a .env file in the project root:

```env
REACT_APP_API_BASE_URL=your-base-url
REACT_APP_AUTH0_DOMAIN=your-auth0-domain
REACT_APP_AUTH0_CLIENT_ID=your-auth0-client-id
```

## Architecture
Client-side routing and UI state run in React, while recipe generation and popularity data are fetched from configurable API endpoints. Build-time scripts prefetch popular recipes, inject SEO metadata into prerendered HTML files, and generate sitemap.xml for deployment.

1. User interactions in landing/composer screens update category selections in RecipeContext.
2. API utility methods call generate/get/popular endpoints using REACT_APP_API_BASE_URL.
3. Results and mode state drive recipe, popular, and cook-mode experiences in route screens.
4. Prebuild and postbuild scripts create metadata-rich static pages for key routes and popular recipes.
5. Vercel serves the built SPA with rewrites while search engines index prerendered HTML and sitemap entries.

```text
[Browser UI: React + MUI]
        |
        v
[RecipeContext + Hooks] -----> [Cocktail JSON dataset in /public/data]
        |
        v
[API Utilities in src/utils/MockAPI.ts]
        |
        v
[Recipe API (generate/get/popular/rating)]

Build pipeline:
npm run prebuild -> npm run build -> npm run postbuild
        |
        v
[Prebuild data + prerendered HTML + sitemap.xml in build/]
        |
        v
[Vercel deployment at createadish.com]
```

## Learning Modules
- Dietary Guide hub with 12 diet-specific pages covering common nutrition patterns.
- Kitchen Toolkit guide for essential home-cooking equipment.
- Global Cuisine page introducing international flavor and technique references.
- Culinary Glossary page for cooking terms and methods used in recipes.

## Deployment
Recommended deployment target: Vercel

```bash
npm run build:static
npx vercel --prod
```

Production URL:
- https://createadish.com

## SEO and Performance
- Route-level metadata is managed with React Helmet Async for title, description, canonical, Open Graph, and Twitter cards.
- Postbuild static generation writes metadata-rich HTML files for key pages and popular recipe routes.
- Sitemap generation includes static and dynamic recipe routes to support indexing coverage.
- Structured data (Schema.org Recipe JSON-LD) is emitted for generated recipe pages.
- Cocktail data is served as a static JSON asset for predictable client load behavior.
- Build process separates data prefetch and prerendering for repeatable CI/CD deployment.

## Screenshots
<!-- Use absolute production URLs for all screenshot images (https://...), not ./assets paths. -->

| Feature | Preview |
|--------|--------|
| Spicy Thai Pork Noodle Delight | ![](https://althistai.aisuretech.com/images/recipe-dddcc8f3.png) |
| Zesty Chicken Tortilla Skillet | ![](https://althistai.aisuretech.com/images/recipe-57dcd072.png) |

## Use Cases
- Home cooks generating meal ideas from available ingredients and dietary constraints.
- Food bloggers researching popular recipes and sharing SEO-friendly links.
- Nutrition-focused learners comparing dietary patterns in one navigation flow.
- Developers studying SPA SEO pre-rendering patterns for React Router projects.

## Roadmap
- [ ] Add complete educational content to all guide placeholders and diet detail sections.
- [ ] Expand automated tests for route rendering, API error handling, and context flows.
- [ ] Add richer recipe structured data fields (nutrition, cook time, ratings) where API data is available.
- [ ] Introduce optional server-side or edge rendering for selected high-value landing routes.

## Contributing
Contributions are welcome.

1. Fork the repository
2. Create a feature branch: git checkout -b feature/your-feature
3. Commit your changes
4. Push to your branch
5. Open a pull request

## FAQ

### Is this a full backend plus frontend recipe platform?
This repository is frontend-first and consumes recipe endpoints via REACT_APP_API_BASE_URL. The backend API is expected to run separately.

### How do I generate SEO-friendly static pages for deployment?
Run npm run build:static. This executes prebuild data fetch, CRA build, static page generation, and sitemap generation.

### Can I run the app without Auth0 credentials?
Yes. Auth0 environment values have fallbacks, so core browsing works, but authenticated profile flows require valid Auth0 settings.

### Where does the drinks data come from?
The cocktail explorer reads from a bundled JSON dataset at /data/cocktails_A-Z.json served from the public assets.

## Suggested GitHub Topics
Add these in repository settings for discoverability:
- ai-recipe-generator
- react-typescript
- meal-planning
- cooking-app
- dietary-guides
- spa-seo
- prerendering
- vercel

## Links
- GitHub Organization: https://github.com/aisuretech/
- Website: https://createadish.com
- Contact: info@AISureTech.com

## License
Proprietary (all rights reserved unless a separate LICENSE file is added)
