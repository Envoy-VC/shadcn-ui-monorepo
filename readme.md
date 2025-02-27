# shadcn/ui Monorepo

This is a monorepo starter for [shadcn/ui](https://ui.shadcn.com). Suppose your monorepo has the following structure:

```
.
├── apps
│   ├── web
│   └── mobile
├── packages
│   ├── ui
│   └── docs
├── package.json
├── tsconfig.json
├── pnpm-lock.yaml
└── {workspace/turbo}.json
```

To start using this, place this folder in your monorepo structure, say for example at `packages/ui`.

Then add this to your web-app `components.json` i.e. `apps/web/components.json`:

```json
{
  "$schema": "https://ui.shadcn.com/schema.json",
  "style": "new-york",
  "rsc": true,
  "tsx": true,
  "tailwind": {
    "css": "../../packages/ui/src/styles/globals.css",
    "baseColor": "neutral",
    "cssVariables": true
  },
  "iconLibrary": "lucide",
  "aliases": {
    "components": "~/components",
    "hooks": "~/hooks",
    "lib": "~/lib",
    "utils": "@repo/ui/lib/utils",
    "ui": "@repo/ui/components"
  }
}
```

You can change tha path aliases to whatever you want in `tsconfig.json`, but make sure to update the `ui` alias to point to the correct path.

Then create a new file at `apps/web/postcss.config.mjs` with the following content:

```js
export { default } from "@repo/ui/postcss.config";
```

Also make sure to import the `globals.css` file in your entrypoint, e.g. `apps/web/src/app/layout.tsx`:

```tsx
import type { ReactNode } from 'react';

import "@repo/ui/globals.css" // Add this line

const RootLayout = ({ children }: Readonly<{ children: ReactNode }>) => {
  return (
    <html lang='en'>
      <body>
        {children}
      </body>
    </html>
  );
};

export default RootLayout;
```

Add this to your `tsconfig.json`:

```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@repo/ui/*": ["./packages/ui/src/*"]
    }
  }
}
```

---