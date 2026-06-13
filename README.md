# Wistaria

A soft theme with lavender tones and a personal notebook feel. It comes with two collections: `journal` for longer, more polished articles and essays, and `log` for shorter, more informal notes, thoughts, and micro-entries. Wistaria is designed to be a cozy digital space for your writing, with a focus on readability and aesthetics.

## Installation

```bash
lith theme pull github:NTBBloodbath/wistaria
```

> [!IMPORTANT]
>
> Wistaria requires a Norgolith build with [this commit](https://github.com/NTBBloodbath/norgolith/commit/e6d1a5cc75b7fc3c13e3945f0115d51631f68668) in order to work.

## Usage

After installing, configure your site as described below. If you plan to modify the CSS, see the [Tailwind Reloading](#tailwind-reloading) section.

### Configuration

Add the following fields to your `norgolith.toml`:

```toml
# Categories directory
categoriesDir = 'library'

# Posts collections
# Journal: Longer, more polished articles and essays.
# Log: Shorter, more informal notes, thoughts, and micro-entries.
[[collections]]
name = 'journal'
dir  = 'journal'

[[collections]]
name = 'log'
dir  = 'log'

[extra]
license = "GPLv2" # Optional
favicon_path = "/assets/norgolith.svg" # Fallback to default favicon
footer_author_link = "https://github.com/NTBBloodbath" # Optional
enable_mermaid = true # Enable Mermaid.js for diagrams

[extra.nav]
Journal = '/journal'
Log = '/log'
Library = '/library'
# About = '/about'

[extra.footer]
# Link_name = "url"
# GitHub = "https://github.com/NTBBloodbath/norgolith"

# Tag colors: accepts either theme color tokens or raw CSS color values.
#
# Theme tokens (adapt automatically to dark mode):
#   primary, secondary, green, blue, violet, yellow, red
#
# Raw CSS values (static, no dark mode adaptation):
#   #rrggbb, rgb(...), hsl(...), oklch(...)
#
#[extra.tags]
#log = 'red'
#essay = 'primary'
#announcement = '#72ff47'
```

### Templates

Wistaria provides these templates:

```
templates
├── partials
│   ├── footer.html  <- Footer content
│   └── nav.html     <- Header navbar
├── base.html        <- Main template (extends others)
├── library.html     <- Categories list
├── book.html        <- Category posts list
├── default.html     <- Default template for all content
├── home.html        <- Homepage
├── journal.html     <- Journal collection
├── log.html         <- Log collection
└── entry.html       <- Blog post
```

To use a template, set the `layout` metadata in your content files. For example, in a journal/log post:

```norg
layout: entry
```

> [!TIP]
>
> 1. The `library` template is used for the categories listing page, and the `book` template is used for the category posts listing page. You can customize these templates to change how your categories and their posts are displayed.
> 2. Wistaria expects your journal entries in the `content/journal` directory and your log entries in the `content/log` directory, as specified in the `collections` configuration. Make sure to place your content files accordingly for them to be rendered with the correct templates.

### MermaidJS Support

Wistaria comes with opt-in support for MermaidJS flowcharts. You can use mermaid charts through embedded HTML in your norg content if you set the `enable_mermaid` option to `true` in the `extra` table of your configuration file:

```org
@embed html
<pre class="mermaid">
  flowchart LR
  A[HTML Fragment] --> B[Tera Engine]
  C[Validated Metadata] --> B
  D[Site Config] --> B
  E[Post Collection] --> B
  B --> F[Layout Template]
  F --> G[Final HTML]
</pre>
@end
```

### Additional Styling

Wistaria provides some additional styling options for blockquotes and code blocks that can be used with `+html.class` tags in your norg content.

#### Blockquotes

- `tip` (green)
- `note` (blue)
- `important` (violet)
- `warning` (yellow)
- `error` (red)

<img width="1380" height="340" alt="image" src="https://github.com/user-attachments/assets/e29d8368-3934-4e3a-aafb-43b6608f1668" />

#### Code Blocks

- `line-numbers` - Adds line numbers to the code block.
- `diff-highlight` - Highlights added lines in green and removed lines in red (useful for diff outputs).

<img width="1372" height="238" alt="image" src="https://github.com/user-attachments/assets/bd1c9e8e-e7cd-4b81-8805-e3f3cb78af9b" />

#### Tags/categories pills

Wistaria provides a `tags` table in the configuration where you can assign colors to specific tags or categories. You can use either theme color tokens (like `primary`, `secondary`, `red`, etc.) or raw CSS color values (like `#rrggbb`, `rgb(...)`, etc.). These colors will be applied to the corresponding tags/categories in your content. For example:
```toml
[extra.tags]
log = 'red'
essay = 'primary'
announcement = '#72ff47'
```

<img width="1392" height="485" alt="image" src="https://github.com/user-attachments/assets/8fa48976-be3a-4c1b-a5b1-5aadab9be835" />

### Tailwind Reloading

By default, Tailwind's configuration in Norgowind watches content files and templates. Each new class added to content using a `+html.class` tag will be included in the styling file.

For site development, install the TailwindCSS CLI and run:
```sh
tailwindcss -i theme/assets/css/tailwind.css -o theme/assets/css/styles.min.css --minify --watch
```

## Contributing

Contributions, issues, and feature requests are welcome! Feel free to open an issue or pull request.

## License

Wistaria is licensed under MIT license.
