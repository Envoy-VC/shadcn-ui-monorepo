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