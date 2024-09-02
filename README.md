# Welcome to the Darwinia Documentation

This repository hosts the source files for Darwinia's documentation, built with [MkDocs](https://www.mkdocs.org/) using the [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) theme.

## Building the Documentation Locally

To build the documentation on your local machine, ensure you have Python and pip installed. Then follow these steps:

```sh
# Clone the repository.
git clone https://github.com/darwinia-network/docs.git && docs
# Install necessary dependencies.
poetry install --no-root
# Build and view the documentation in your browser at `http://127.0.0.1:8000`.
mkdocs build
mkdocs serve
```

## Contributing to the Documentation

Contributions are welcome! To contribute:

1. Fork this repository.
2. Edit Markdown files in the `docs` folder.
3. Build locally to check formatting.
4. Create a pull request with your updates.

We'll review and merge your pull request promptly.

Thanks for contributing to Darwinia's documentation!
