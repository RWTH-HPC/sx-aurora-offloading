# SX-Aurora Offloading
This repository contains the documentation for sotoc and the SX-Aurora TSUBASA OpenMP Offloading toolchain.

## How to update the documentation?
To update the existing text simply add your modifications to the corresponding MarkDown file in the `docs` directory.
After pushing the changes to git the CI pipeline will deploy the documentation page.

## How to add new pages?
To add pages to the documentation two steps have to be done.
First add the new page in valid MarkDown to the `docs` directory.
Second add the new file to the `nav` element in the `mkdocs.yml` config file.

```yaml
nav:
  - Home: "index.md"
  - "User Guide":
      - "Writing your docs": "writing-your-docs.md"
      - "Styling your docs": "styling-your-docs.md"
  - About:
      - "License": "license.md"
      - "Release Notes": "release-notes.md"
```

After pushing the changes to git the documentation page will be automatically deployed.

## How to update variables (e.g., version numbers etc.)?
Version numbers and such should be defined as variables (macros).
This can be done in `mkdocs.yml` in:

``` yaml
extra:
  link:
    llvm: %%llvm%%
  version:
    rpm: 1.8.0
```

In the documents variables are inserted by adding e.g., `{{ link.llvm }}` or `{{ version.rpm }}`.

- **Attention**: `{% raw %}` and `{% endraw %}` have to be used to encapsulate segments,
 in which no replacements should be performed. (e.g., Code blocks with `{{}}` in one line)

## How to add Doxygen?
Adding Doxygen has to be done manually, using [doxybook2](https://github.com/matusnovak/doxybook2/).
After downloading the software and building the Doxygen XML run:

``` shell
 doxybook2 --input doxygen/xml --output docs/internal/doxygen/ --config doxybook/config.json --templates doxybook/template
```
With the config and template folder are located in the doxybook directory.
## Special syntax
### Admonitions
Admonitions are coloured blocks of text:

```markdown
!!! note
    Your Text
```

Notes will be coloured blue.

```markdown
!!! warning
    Your Text
```

Warnings are orange.

```markdown
!!! danger
    Your Text
```

And danger is coloured red.

Others are available (see [Material Docs](https://squidfunk.github.io/mkdocs-material/reference/admonitions/#supported-types)).

These blocks can be made collapsible by changing `!!!` to `???` for
folded by default or `???+` for expanded by default.

### Fenced code blocks
To add a code block use the following syntax.

````markdown
``` <language>
Your Code goes here
```
````

Line numbers can be added by appending `linenums="1"`
````markdown
``` <language> linenums="1"
Your Code goes here
```
````

Lines can be highlighted with `hl_lines="2 4 6"` for a selection of lines or `hl_lines="2-5"` for a range.

External files can be embedded using `--8<-- "code.c"` inside a code block.

### Inline Code
Inline code can be added like such:
``` markdown
` <code>`
```
syntax highlighting can be added by providing the language
``` markdown
`#!<language> <code>`
```

### Linking pages and media
To link to another page use:

```markdown
[Link Text](page.md)
```

To add an image use:

```markdown
![Screenshot](img/image.png)
```

### Glossary
Adding `--8<-- "includes/abbreviations.md"` to the bottom of a page adds
abbreviation support to the page using the glossary provided in `includes/abbreviations.md`
