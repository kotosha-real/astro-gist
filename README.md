# Astro Gist

Dead simple yet powerful gist rendering buddy for your Astro blog.

## Features

✅ Uses the standard gist embed script and wraps it in an iframe to avoid blocking the main thread

✅ Lazy loads the gist using IntersectionObserver to improve performance

✅ Allows you to style the gist using your own stylesheet

✅ Fails gracefully when the gist fails to load, showing a link to the gist

✅ Supports rendering a specific file from the gist

✅ Supports adding a caption to the gist

✅ Less than 1 kB of client JavaScript

## Installation

```bash
# pnpm
pnpm add @kotosha/astro-gist

# npm
npm install @kotosha/astro-gist

# yarn
yarn add @kotosha/astro-gist
```

## Usage

You can use it in your Astro blog both in `.astro` and `.mdx` files. Just import the component and use it with the `id` prop:

```typescript jsx
// YourComponent.astro
---
import Gist from '@kotosha/astro-gist'
---

<div>
    <Gist id="your-gist-id" />
</div>
```

```mdxjs
// YourPost.mdx
import Gist from '@kotosha/astro-gist'

Awesome gist here:

<Gist id="your-gist-id" />
```

You can also pass additional props to customize the component behavior:

| Name                | Type    | Default | Description                                                                                                                                                                     | Required |
| ------------------- | ------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| id                  | string  | -       | Gist ID                                                                                                                                                                         | ✔️       |
| caption             | string  | -       | Caption to display below the gist. If not provided, no caption will be displayed. Caption will only be displayed if the gist is loaded successfully                             |
| className           | string  | -       | Additional class to add to the figure. Useful for styling                                                                                                                       |
| file                | string  | -       | File to display from the gist. If not provided, the whole gist will be displayed                                                                                                |
| gistStylesUrl       | string  | -       | URL to the stylesheet to use for styling the gist                                                                                                                               |
| lazy                | boolean | true    | Whether to lazy load the gist. Use IntersectionObserver to load the gist when it comes into view. If IntersectionObserver is not supported, the gist will be loaded immediately |
| observerRootMargin  | number  | 150     | Margin around the root of the IntersectionObserver. The more the margin, the earlier the iframe will be loaded                                                                  |
| showGistLinkOnError | boolean | true    | Whether to show the link to the gist when the gist fails to load                                                                                                                |

## Customization

Gist is rendered as a `figure` with an optional `figcaption`. You can style it using the `className` prop:

```typescript jsx
<Gist className="cls" id="your-gist-id" />

<style>
    .cls {
        /* Basic styles here */
    }

    .cls figcaption {
        /* Figcaption styles here */
    }
</style>
```

You can also apply styles based on the loading status using the `data-loading-status` attribute:

```css
.cls[data-loading-status='success'] {
    /* Success styles here */
}

.cls[data-loading-status='error'] {
    /* Error styles here */
}
```

To style the gist itself, pass the URL to the stylesheet you want to use as the `gistStylesUrl` prop:

```typescript jsx
<Gist id="your-gist-id" gistStylesUrl="/gist-theme.css" />
```

It might be convenient to use a wrapper component to pass the `gistStylesUrl` prop to all gists in your blog:

```typescript jsx
// GistWrapper.astro
---
import Gist from '@kotosha/astro-gist'

const props = Astro.props;
---

<Gist gistStylesUrl="/gist-theme.css" {...props} />
```

## License

MIT
