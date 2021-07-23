# SX-Aurora Offloading

This repository contains the documentation for `sotoc` and the SX-Aurora TSUBASA OpenMP Offloading toolchain.

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

### Fenced code blocks

To add a code block use the following syntax.

````markdown
``` <Language Name>
Your Code goes here
```
````

### Linking pages and media

To link to another page use:

```markdown
[Link Text](page.md)
```

To add an image use:

```markdown
![Screenshot](img/image.png)
```
