# @michael-andreuzza/seo

SEO component for Astro projects.

This package renders SEO `<meta>` and `<link>` tags in your page `<head>` using a single `AstroSeo` component.

## Install

```bash
npm i @michael-andreuzza/seo
```

## Quick Start

Use it directly in a page or layout:

```astro
---
import { AstroSeo } from "@michael-andreuzza/seo";
---

<html lang="en">
  <head>
    <AstroSeo
      title="Lexington Theme - Home"
      description="Production-ready Astro themes for freelancers and businesses."
      canonical="https://example.com/"
    />
  </head>
  <body>
    <slot />
  </body>
</html>
```

## Common Examples

### Basic page SEO

```astro
---
import { AstroSeo } from "@michael-andreuzza/seo";
---

<AstroSeo
  title="About"
  description="Learn more about our team and services."
  canonical="https://example.com/about"
/>
```

### Open Graph + Twitter

```astro
---
import { AstroSeo } from "@michael-andreuzza/seo";
---

<AstroSeo
  title="Astro Landing Page Kit"
  description="Fast, modern landing pages built with Astro."
  canonical="https://example.com/templates/landing-kit"
  openGraph={{
    url: "https://example.com/templates/landing-kit",
    title: "Astro Landing Page Kit",
    description: "Fast, modern landing pages built with Astro.",
    site_name: "Lexington Themes",
    images: [
      {
        url: "https://example.com/og/landing-kit.jpg",
        width: 1200,
        height: 630,
        alt: "Landing Page Kit Preview",
      },
    ],
  }}
  twitter={{
    cardType: "summary_large_image",
    site: "@lexingtonthemes",
    handle: "@lexingtonthemes",
  }}
/>
```

### Noindex pages

```astro
---
import { AstroSeo } from "@michael-andreuzza/seo";
---

<AstroSeo
  title="Internal Preview"
  description="Internal preview page."
  noindex={true}
  nofollow={true}
/>
```

### Language alternates

```astro
---
import { AstroSeo } from "@michael-andreuzza/seo";
---

<AstroSeo
  title="Docs"
  description="Documentation page."
  canonical="https://example.com/docs"
  languageAlternates={[
    { hreflang: "en", href: "https://example.com/docs" },
    { hreflang: "sv", href: "https://example.com/sv/docs" },
  ]}
/>
```

### Extra meta/link tags

```astro
---
import { AstroSeo } from "@michael-andreuzza/seo";
---

<AstroSeo
  title="PWA Page"
  description="PWA-enabled page."
  additionalMetaTags={[
    { name: "theme-color", content: "#0f172a" },
    { property: "og:locale", content: "en_US" },
  ]}
  additionalLinkTags={[
    { rel: "icon", href: "/favicon-32x32.png", sizes: "32x32" },
    { rel: "manifest", href: "/site.webmanifest" },
  ]}
/>
```

## Migrating from `@astrolib/seo`

If your existing themes already use `AstroSeo`, only the import path changes:

```astro
---
import { AstroSeo } from "@astrolib/seo";
import { AstroSeo } from "@michael-andreuzza/seo";
---
```

The prop shape is intentionally compatible for easy migration.

## API

Main props include:

- `title`, `description`, `canonical`
- `openGraph`, `twitter`, `facebook`
- `noindex`, `nofollow`, `robotsProps`
- `languageAlternates`, `mobileAlternate`
- `additionalMetaTags`, `additionalLinkTags`

For full types, see `src/types.ts`.

## Capabilities (What You Can Output)

### Standard SEO

- Page title and optional title template
- Meta description
- Canonical URL
- Robots directives (`noindex`, `nofollow`)
- Advanced robots directives via `robotsProps`:
  - `nosnippet`
  - `maxSnippet`
  - `maxImagePreview`
  - `maxVideoPreview`
  - `noarchive`
  - `unavailableAfter`
  - `noimageindex`
  - `notranslate`

### Open Graph

- Core OG tags:
  - `og:url`
  - `og:type`
  - `og:title`
  - `og:description`
  - `og:locale`
  - `og:site_name`
- OG media:
  - images (`og:image`, width, height, alt, type, secure_url)
  - videos (`og:video`, width, height, alt, type, secure_url)
- OG type-specific fields:
  - Profile (`firstName`, `lastName`, `username`, `gender`)
  - Article (`publishedTime`, `modifiedTime`, `expirationTime`, `authors`, `section`, `tags`)
  - Book (`authors`, `isbn`, `releaseDate`, `tags`)
  - Video (`actors`, `directors`, `writers`, `duration`, `releaseDate`, `tags`, `series`)

### Twitter Cards

- `twitter:card`
- `twitter:site`
- `twitter:creator`

### Facebook

- `fb:app_id`

### Alternate URLs / Internationalization

- Mobile alternate (`media`, `href`)
- Language alternates (`hreflang`, `href`)

### Custom Meta and Link Tags

- Add custom HTML5 / RDFa / HTTP-Equiv meta tags via `additionalMetaTags`
- Add custom link tags (icon, manifest, preconnect, alternate, etc.) via `additionalLinkTags`

## Development

```bash
npm install
npm test
```
