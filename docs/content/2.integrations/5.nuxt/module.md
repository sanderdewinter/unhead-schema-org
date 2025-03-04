---
title: nuxt-schema-org
description: Install the nuxt-schema-org module to start using Schema.org in your Nuxt app.
---

# Nuxt Schema.org

ℹ️ Looking for a complete SEO solution? Check out [Nuxt SEO Kit](https://github.com/harlan-zw/nuxt-seo-kit).

## Install

::code-group

```bash [yarn]
yarn add -D nuxt-schema-org
```

```bash [npm]
npm install -D nuxt-schema-org
```

```bash [pnpm]
pnpm add -D nuxt-schema-org
```

::

## Demo

<a href="https://stackblitz.com/edit/nuxt-starter-z9np1t?file=app.vue" target="_blank">
  <img alt="Open in StackBlitz" src="https://camo.githubusercontent.com/bf5c9492905b6d3b558552de2c848c7cce2e0a0f0ff922967115543de9441522/68747470733a2f2f646576656c6f7065722e737461636b626c69747a2e636f6d2f696d672f6f70656e5f696e5f737461636b626c69747a2e737667">
</a>


## Setup Module

### 1. Add Module

Add the module to your Nuxt config.

```ts [nuxt.config.ts]
export default defineNuxtConfig({
  modules: [
    'nuxt-schema-org',
  ],
})
```

::alert{type="info"}
This module uses auto-imports for composables and components.
::


### 2. Configure the module

To server-side render Schema.org, you'll need to provide a [canonical host](https://developers.google.com/search/docs/advanced/crawling/consolidate-duplicate-urls). 

```ts nuxt.config.ts
export default defineNuxtConfig({
  // ...
  schemaOrg: {
    host: 'https://example.com',
  },
})
```

See the [User Config page](/guide/guides/user-config) for all options you can pass on `schemaOrg`.

### 3. Recommended: Add Site Schema.org

To quickly add the recommended Schema.org to all pages, you can make use [Runtime Inferences](/guide/getting-started/how-it-works#runtime-inferences).

This should be done in either your `app.vue` or `layouts/default.vue` file.

::code-group

```vue [Composition API]
<script lang="ts" setup>
useSchemaOrg([
  // @todo Select Identity: https://unhead-schema-org.harlanzw.com//guide/guides/identity
  defineWebSite({
    name: 'My Awesome Website',
  }),
  defineWebPage(),
])
</script>
```

```vue [Component API]
<template>
  <!-- @todo Select Identity: https://unhead-schema-org.harlanzw.com//guide/guides/identity -->
  <SchemaOrgWebSite name="My Awesome Website" />
  <SchemaOrgWebPage />
</template>
```

::

### Next Steps

Your Nuxt app is now serving basic Schema.org, congrats! 🎉

The next steps are:
1. Choose an [Identity](/guide/guides/identity)
2. Set up your pages for [Runtime Inferences](/guide/getting-started/how-it-works#runtime-inferences)
3. Then feel free to follow some recipes:

- [Breadcrumbs](/guide/recipes/breadcrumbs)
- [FAQ Page](/guide/recipes/faq)
- [Site Search](/guide/recipes/site-search)


## Module Options

All module options can be passed on the `schemaOrg` key in your `nuxt.config.ts`.

See [User Config](/guide/guides/user-config) for config options.

## NuxtApp Hooks

- `schema-org:meta`: `(meta: MetaInput) => void`{lang="ts"}

You can hook into the generation of the meta-data used to generate the Schema.org data. 

For example, this can be useful
for dynamically changing the host.



```ts [my-nuxt-plugin.ts]
import { defineNuxtPlugin } from '#app'

export default defineNuxtPlugin((nuxtApp) => {
  nuxtApp.hooks.hook('schema-org:meta', (meta) => {
    if (nuxtApp._route.path === '/plugin-override') {
      meta.host = 'https://override-example.com'
      meta.url = `${meta.host}${meta.path}`
    }
  })
})

```
