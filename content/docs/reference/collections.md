---
$title: Collections
$category: Reference
$order: 1.04
---
# Collections

All content in Grow is stored as flat files in your pod's `/content/` directory. Content is grouped into __collections__, and each collection contains a single __blueprint__ and many __documents__. Blueprints describe the structure of all documents in the collection.

Grow makes it easy to separate content from presentation, but ultimately leaves the choice up to you. Content documents can be associated with URLs and with views (so they represent pages in your site), or not. Content documents without URLs are simply used internally, and can be referenced by other content documents.

## Blueprints

Every content collection must have a blueprint. Blueprints define how the content of a collection is structured, displayed, and served. Blueprints are stored as YAML files in your pod's *content* directory.  For example, the blueprint for a collection called `people` would be `/content/people/_blueprint.yaml` and might have the following content

```yaml
path: /people/{slug}/              # The URL path format for content.
view: /views/people.html           # The template to use.

localization:                      # Overrides localization from podspec.yaml.
  path: /{locale}/people/{slug}/
  locales:
  - de
  - fr
  - it
```

The values in the blueprint are applied to all documents in the collection but can be overridden through the front matter of a document. See the documentation of the [front matter]([url('/content/docs/reference/documents.md')]#front-matter).

### path

Specifies the URL path format for all content in this collection. If `path` is omitted, content in this collection will not be generated into pages, unless a document specifies its own `$path`. If `path` is specified, `view` is a required field.

Paths can be formatted in several ways, see the [list of path formatters]([url('/content/docs/reference/urls.md')]#content-document-path-formatters).

### view

Specifies which template should be used to render content in this collection. If `view` is specified, `path` is a required field.

```yaml
# Documents in this collection will use the following template.
$view: /views/pages.html
```

### localization

Localization configuration for content in this collection.

#### path

Specifies a URL path format for localized content. By specifying both `path` and `localization:path`, you can use different formats for the URL paths for "root" and localized content.

```yaml
$localization:
  path: /{locale}/people/{slug}/
```

#### locales

Specifies a list of locales that documents in this collection are available in. Each document's *path* will be expanded using *locales* to derive the URLs that the document is available at.

```yaml
$localization:
  locales:
  - de
  - fr
  - it
```

### categories

The `categories` key contains a list of categories that documents inside the collection can fall into. A collection's categories can be used in conjunction with the `g.categories` template function to iterate over the documents in the collection, grouped by category.

## Nested collections

You can create collections inside other collections simply creating a nested directory containing a blueprint

```bash
├─ /content*                     # All your content.
|  ├─ /books                     # The collection "books".
|     ├─ /_blueprint.yaml*       # The blueprint for "books".
|     ├─ /index.md               # A document belonging to "books".
|     ├─ /contacts.md            # A document belonging to "books".
|     └─ /how_to_use_grow        # The collection "how_to_use_grow".
|        ├─ /_blueprint.yaml*    # The blueprint for "how_to_use_grow".
|        ├─ /chapter01.md        # A document belonging to "how_to_use_grow".
|        ├─ /chapter02.md        # A document belonging to "how_to_use_grow".
|        ├─ /chapter03.md        # A document belonging to "how_to_use_grow".
|     └─ /grow_style_guide       # The collection "grow_style_guide".
|        ├─ /_blueprint.yaml*    # The blueprint for "grow_style_guide".
|        ├─ /chapter01.md        # A document belonging to "grow_style_guide".
|        ├─ /chapter02.md        # A document belonging to "grow_style_guide".
```

Here, `books` is a collection that contains documents, namely `index.md` and `contacts.md`. It also contains two nested collections, `books/how_to_use_grow` and `books/grow_style_guide`, each one with their own blueprint and content files.

Inside the view used by `books/index.md` the variable `doc.collection.basename` will be `books`, while for `books/how_to_use_grow/chapter01.md` the value will be `books/how_to_use_grow`, and for `books/grow_style_guide/chapter01.md` it will be `books/grow_style_guide`.

Anywhere in the pod you can refer to nested collections using their full basename, e.g.

``` jinja
{% for chapter in g.collection('books/how_to_use_grow).list_docs() %}
<a href="{{ chapter.url }}">{{ chapter.title }}</a>
{% endfor %}
```
