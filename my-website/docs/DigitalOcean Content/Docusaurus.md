**Plugin-Client-Redirects**

A Docusaurus plugin to generate client-side redirects.

This plugin writes additional HTML pages to your static site that redirect users to your existing Docusaurus pages using JavaScript.

### **Production Only**

> This plugin is always inactive in development and only active in production because it works on the build output.

### **Warning**

It is better to use server-side redirects whenever possible.

Before using this plugin, check whether your hosting provider already offers redirect support.

## Installation

### npm

```bash
npm install --save @docusaurus/plugin-client-redirects
```

### Yarn

```bash
yarn add @docusaurus/plugin-client-redirects
```

### pnpm

```bash
pnpm add @docusaurus/plugin-client-redirects
```

### Bun

```bash
bun add @docusaurus/plugin-client-redirects
```

## Configuration

The plugin accepts the following configuration options:

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `fromExtensions` | `string[]` | `[]` | Extensions removed from the route after redirecting. |
| `toExtensions` | `string[]` | `[]` | Extensions appended to the route after redirecting. |
| `redirects` | `RedirectRule[]` | `[]` | List of redirect rules. |
| `createRedirects` | `CreateRedirectsFn` | `undefined` | Callback used to generate redirect rules dynamically for existing paths. |

### **Note**

This plugin also reads the `siteConfig.onDuplicateRoutes` configuration to adjust its logging level when multiple files would be generated at the same location.

## Types

### RedirectRule

A single redirect rule:

```ts
type RedirectRule = {
  to: string;
  from: string | string[];
};
```

*   The concepts of **`from`** and **`to`** are central to this plugin.
*   -   **`from`** is the path you want to create (an additional HTML file).
*   -   **`to`** is the destination path that users are redirected to (typically an existing Docusaurus route).

## CreateRedirectsFn

A callback function used to generate redirect rules dynamically for existing paths:

```ts
// The parameter `path` is an existing Docusaurus route ("to").
// The return value specifies one or more redirect paths ("from").

type CreateRedirectsFn = (
  path: string
) => string[] | string |