---
title: Collection Types
position: 27
---

# Collection Types

All editable content types are defined in the `collections` field of your `config.yml` file, and display in the left sidebar of the Content page of the editor UI.

Collections come in two main types: `folder` and `files`.


## Folder collections

Folder collections represent one or more files with the same format, fields, and configuration options, all stored within the same folder in the repository. You might use a folder collection for blog posts, product pages, author data files, etc.

Unlike file collections, folder collections have the option to allow editors to create new items in the collection. This is set by the boolean `create` field.

Example:

```yaml
- label: "Blog"
  name: "blog"
  folder: "_posts/blog"
  create: true
  fields:
    - {label: "Title", name: "title", widget: "string"}
    - {label: "Publish Date", name: "date", widget: "datetime"}
    - {label: "Featured Image", name: "thumbnail", widget: "image"}
    - {label: "Body", name: "body", widget: "markdown"}
```

### Filtered folder collections

The entries for any folder collection can be filtered based on the value of a single field. By filtering a folder into different collections, you can manage files with different fields, options, extensions, etc. in the same folder.

The `filter` option requires two fields:

- `field`: the name of the collection field to filter on
- `value`: the desired field value

The example below creates two collections in the same folder, filtered by the `language` field. The first collection includes posts with `language: en`, and the second, with `language: es`.

``` yaml
collections:
  - label: "Blog in English"
    name: "english_posts"
    folder: "_posts"
    filter: {field: "language", value: "en"}
    fields:
      - {label: "Language", name: "language", widget: "select", options: ["en", "es"]}
      - {label: "Title", name: "title", widget: "string"}
      - {label: "Content", name: "body", widget: "markdown"}      
  - label: "Blog en Español"
    name: "spanish_posts"
    folder: "_posts"
    filter: {field: "language", value: "es"}
    fields:
      - {label: "Lenguaje", name: "language", widget: "select", options: ["en", "es"]}
      - {label: "Titulo", name: "title", widget: "string"}
      - {label: "Contenido", name: "body", widget: "markdown"}      
```


## File collections

A `files` collection contains one or more uniquely configured files. Unlike items in `folder` collections, which repeat the same configuration over all files in the folder, each item in a `files` collection has an explicitly set path, filename, and configuration. This can be useful for unique files with a custom set of fields, like a settings file or a custom landing page with a unique content structure.

When configuring a `files` collection, each file in the collection is configured separately, and listed under the `files` field of the collection. Each file has its own list of `fields`, and a unique filepath specified in the `file` field (relative to the base of the repo).

Example:

``` yaml
- label: "Pages"
  name: "pages"
  files:
    - label: "About Page"
      name: "about"
      file: "site/content/about.yml"
      fields:
        - {label: Title, name: title, widget: string}
        - {label: Intro, name: intro, widget: markdown}
        - label: Team
          name: team
          widget: list
          fields:
            - {label: Name, name: name, widget: string}
            - {label: Position, name: position, widget: string}
            - {label: Photo, name: photo, widget: image}
    - label: "Locations Page"
      name: "locations"
      file: "site/content/locations.yml"
      fields:
        - {label: Title, name: title, widget: string}
        - {label: Intro, name: intro, widget: markdown}
        - label: Locations
          name: locations
          widget: list
          fields:
            - {label: Name, name: name, widget: string}
            - {label: Address, name: address, widget: string}
```