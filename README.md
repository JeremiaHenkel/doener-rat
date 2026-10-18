# Dönerrat Marburg

Döner reviews, ratings, and photos from Marburg and Mittelhessen.

## Development

Use Node.js 22.22 or newer (Node.js 24 is used in CI).

```bash
npm ci
npm run dev
```

Open the local URL printed by Astro. Changes to pages and styles reload automatically.

```bash
npm run check    # Check Astro templates and TypeScript
npm run build    # Generate the static site in dist/
npm run preview  # Serve the production build locally
```

`npm run watch` is an alias for the development server.

## Project structure

```text
src/
  pages/          # Ranking, shop details, statistics, and legal pages
  layouts/        # HTML document, page metadata, and stylesheet
  components/     # Shared background and footer
  styles/         # Tailwind source and the existing custom styles
public/
  data/           # doener.json: official shop information and ratings
  stories/        # Markdown reviews
  images/         # Original photos, backgrounds, and graphics
  js/             # Existing ranking and Firebase browser scripts
  background/     # Asset license information
```

Astro generates static HTML. Tailwind builds the styles through Vite. The existing browser JavaScript still handles sorting, search, the image carousel, and Firebase community interactions. The shared templates use TypeScript for their props.

To add or update a review, edit `public/data/doener.json`, the matching file in `public/stories/`, and the shop photos in `public/images/`. Keep the existing shop names and photo naming convention: shop names also identify the Firebase comments and ratings.

## Hosting

The production output is `dist/`. The build keeps the current URLs, including `index.html`, `laden.html?name=…`, `stats.html`, `impressum.html`, and `datenschutz.html`. Static assets keep their existing URLs too.

GitHub Pages must serve the built output rather than the source branch once this migration is merged. The check workflow validates pull requests without publishing them. For the production repository, select **GitHub Actions** in Pages settings and manually run the **Deploy site** workflow on `main`. This workflow is restricted to the original repository and never runs automatically. Coordinate the Pages settings change with the merge and first deployment. See [Astro's GitHub Pages guide](https://docs.astro.build/en/guides/deploy/github/).

For a Pages preview under a repository subpath, build with the corresponding base:

```bash
ASTRO_BASE_PATH=/doener-rat/ npm run build
```

`public/CNAME` contains the existing production domain. Use that file only for the production deployment; omit it from a fork's Pages deployment.

## Migration scope

This first migration preserves the published site's layout, wording, photos, review files, Firebase integration, and browser behavior. It adds shared templates, a development server, a production build, TypeScript checks, and CI. Design changes and further refactoring can be reviewed in later pull requests.
