A solid frontend file structure should optimize for:

* **Scalability** — easy to grow from small to large apps
* **Separation of concerns** — logic, styles, assets, and UI organized clearly
* **Feature ownership** — related files grouped together
* **Maintainability** — predictable locations for files
* **Tool compatibility** — works well with bundlers/frameworks later

A modern best-practice structure for a vanilla frontend web application looks like this:

```text
project-root/
│
├── public/                     # Static files served directly
│   ├── favicon.ico
│   ├── robots.txt
│   └── manifest.json
│
├── src/                        # Main application source
│   │
│   ├── assets/                 # Shared static assets
│   │   ├── images/
│   │   ├── icons/
│   │   ├── fonts/
│   │   └── videos/
│   │
│   ├── components/             # Reusable UI components
│   │   ├── navbar/
│   │   │   ├── navbar.js
│   │   │   ├── navbar.css
│   │   │   └── navbar.html
│   │   │
│   │   └── button/
│   │       ├── button.js
│   │       └── button.css
│   │
│   ├── pages/                  # Page-level views
│   │   ├── home/
│   │   │   ├── home.js
│   │   │   ├── home.css
│   │   │   └── home.html
│   │   │
│   │   └── about/
│   │       ├── about.js
│   │       ├── about.css
│   │       └── about.html
│   │
│   ├── styles/                 # Global styles
│   │   ├── base/
│   │   │   ├── reset.css
│   │   │   ├── typography.css
│   │   │   └── variables.css
│   │   │
│   │   ├── layout/
│   │   │   ├── grid.css
│   │   │   └── containers.css
│   │   │
│   │   └── main.css
│   │
│   ├── scripts/                # Shared JS utilities/services
│   │   ├── api/
│   │   ├── utils/
│   │   ├── helpers/
│   │   └── config/
│   │
│   ├── data/                   # Static JSON/mock data
│   │
│   ├── index.html              # Main HTML entry
│   └── main.js                 # App bootstrap
│
├── tests/                      # Unit/integration tests
│
├── .gitignore
├── package.json
├── README.md
└── vite.config.js              # or webpack.config.js
```

## Recommended Principles

### 1. Group by Feature, Not File Type

Instead of:

```text
js/
css/
html/
```

prefer:

```text
components/navbar/
components/modal/
```

This keeps everything related together.

Good:

```text
modal/
├── modal.js
├── modal.css
└── modal.html
```

This scales much better.

---

### 2. Separate Global vs Local Styles

Use:

* `styles/` → global design system
* component CSS → local component styling

Example:

```text
styles/
├── variables.css
├── reset.css
└── theme.css
```

Avoid giant monolithic CSS files.

---

### 3. Keep Assets Organized by Type

```text
assets/
├── images/
├── icons/
├── fonts/
└── videos/
```

For large apps:

```text
assets/images/auth/
assets/images/dashboard/
```

---

### 4. Use Consistent Naming

Common conventions:

```text
kebab-case   → files/folders
PascalCase   → JS classes/components (frameworks)
camelCase    → variables/functions
```

Examples:

```text
user-profile.js
shopping-cart.css
```

---

### 5. Keep Entry Points Minimal

Your `main.js` should mainly initialize the app:

```js
import './styles/main.css';
import { initRouter } from './scripts/router.js';

initRouter();
```

Avoid putting business logic directly in bootstrap files.

---

## Small Project Version

For simple sites:

```text
project/
├── index.html
├── css/
├── js/
├── images/
└── pages/
```

This is perfectly fine for landing pages or small portfolios.

---

## Medium-to-Large App Recommendation

As the app grows:

```text
src/
├── features/
│   ├── auth/
│   ├── dashboard/
│   └── profile/
```

Feature-driven architecture scales extremely well.

Example:

```text
features/
└── auth/
    ├── components/
    ├── services/
    ├── auth-api.js
    ├── auth.css
    └── login-page.js
```

---

## If Using Modern Tooling

For apps using:

* React
* Vue
* Svelte
* Vite
* Webpack

A common structure becomes:

```text
src/
├── components/
├── layouts/
├── pages/
├── hooks/
├── services/
├── store/
├── routes/
├── assets/
└── utils/
```

---

## Best Practice Summary

Recommended priorities:

1. Feature-based organization
2. Co-locate related files
3. Separate reusable/shared code
4. Keep global styles minimal
5. Organize assets clearly
6. Use consistent naming
7. Avoid deeply nested folders
8. Make paths predictable

A good rule:

> “If a new developer can guess where a file belongs, the structure is working.”
