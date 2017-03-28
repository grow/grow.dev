(Work in progress)

## Content

- Place pages content in the `/content/pages` directory.
- Place partial content in the `/content/partials` directory.
- Keep content separate from presentation. Use `yaml` format when requiring structured data, and `md` format when requiring long-form, text-heavy content.

## Templates

- Place templates in the `/views` directory.
- Name the main site template `/views/base.html`.
- Place page-specific templates in the `/views/pages` directory.
- Place partial templates in the `/views/partials` directory.

## Naming

- Be consistent.
- If a page `/content/pages/foo.yaml` has a page-specific template, name the template `/views/pages/foo.html`.
- If a partial `/content/partials/header.yaml` warrants a template, name the template `/views/partials/header.html`.

## Partial templates

Partial templates are a powerful concept that permit site architects to divide a design up into sections, and then freely rearrange and reuse those designs throughout the site.

Most pages that can be divided up into discrete sections (such as a header, content area – or collection of various content areas in order, and a footer) should be implemented using partials.

- Name partials in a generic way. The name of the partial should not be coupled to a specific page if possible, but rather the partial's design. For example, a you might have a partial named `/views/partials/hero.html` which would be the "hero" element for a page.

## Styles

- Follow BEM, strictly.
- Use mixins to denote shared styles, e.g. a mixin for the body typeface, or for font sizes or margins.
- BEM names should correspond directly to partial template names. In general, there should be one Sass file per partial template. See the following complete example:

```
/content/partials/header.yaml
/source/sass/partials/header.sass
/views/partials/header.html
```
