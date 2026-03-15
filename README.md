# @lexingtonthemes/seo

SEO component for Astro projects.

This package renders SEO tags in your page `<head>` using a single `AstroSeo` component: **meta** and **link** tags (title, description, canonical), **Open Graph**, **Twitter Cards**, **Facebook** (`fb:app_id`), **robots** (noindex, nofollow, advanced directives), **language alternates** (hreflang), **mobile alternate**, and **JSON-LD** structured data.

## Install

```bash
npm i @lexingtonthemes/seo
```

## Quick Start

Use it directly in a page or layout:

```astro
---
import { AstroSeo } from "@lexingtonthemes/seo";
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
import { AstroSeo } from "@lexingtonthemes/seo";
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
import { AstroSeo } from "@lexingtonthemes/seo";
---

<AstroSeo
  title="Premium Astro themes"
  description="Fast, modern websites built with Astro."
  canonical="https://example.com/templates/themes"
  openGraph={{
    url: "https://example.com/templates/themes",
    title: "Astro themes",
    description: "Fast, modern websites built with Astro.",
    site_name: "Lexington Themes",
    images: [
      {
        url: "https://example.com/og/themes.jpg",
        width: 1200,
        height: 630,
        alt: "themes Preview",
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
import { AstroSeo } from "@lexingtonthemes/seo";
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
import { AstroSeo } from "@lexingtonthemes/seo";
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
import { AstroSeo } from "@lexingtonthemes/seo";
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

### JSON-LD (structured data)

```astro
---
import { AstroSeo } from "@lexingtonthemes/seo";
---

<AstroSeo
  title="Lexington Themes"
  description="Production-ready Astro themes."
  canonical="https://example.com/"
  jsonLd={[
    {
      "@context": "https://schema.org",
      "@type": "Organization",
      name: "Lexington Themes",
      url: "https://example.com",
    },
    {
      "@context": "https://schema.org",
      "@type": "WebSite",
      name: "Lexington Themes",
      url: "https://example.com",
    },
  ]}
/>
```

## Migrating from `@astrolib/seo`

If your existing themes already use `AstroSeo`, only the import path changes:

```astro
---
import { AstroSeo } from "@astrolib/seo";
import { AstroSeo } from "@lexingtonthemes/seo";
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
- `jsonLd` – one or more JSON-LD schema objects (see below)

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

### JSON-LD

- Pass one or more [JSON-LD](https://developers.google.com/search/docs/appearance/structured-data/intro-structured-data) schema objects via the `jsonLd` prop. Each object is rendered as a `<script type="application/ld+json">` tag. Use a single object or an array of objects for multiple schemas (e.g. Organization + WebSite). Values are stringified and safely escaped (e.g. `</script>` in strings) so the markup is valid.

## Development

```bash
npm install
npm test
```

## License

MIT © [Lexington Themes](https://lexingtonthemes.com)
