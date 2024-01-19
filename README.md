# Docs

![Proof HTML](https://github.com/groupplants/docs/actions/workflows/proof-html.yml/badge.svg)

Documentation for group student project based on [mkdocs](https://squidfunk.github.io/mkdocs-material/creating-your-site/#creating-your-site-unix-powershell).

## How to run

### Docker

`docker run --rm -it -v ${PWD}:/docs squidfunk/mkdocs-material new .`

### Python

`mkdocs serve`

## Creating UML schematics

### Gaphor

Download [gaphor](https://gaphor.org/download/). When creating schematics save the graphor project to the `graphor` directory.
Export them to `docs/assets/uml` - svg format.
