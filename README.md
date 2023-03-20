# Outlines

This project collects detailed notes as aggregate outlines.

Please send `pull requests` if you notice errors.

## Purpose

1. Store information in a way that can be easily referenced or updated.
2. Have a destination for information curated during deep projects, especially after they end.


## Locations

1. `praxes` - praxis/process oriented information
2. `reference` - primarly aggregated from another source
3. `monographs` - my original, observations from data and experiences
4. `talks` - notes from speakers and events 
5. `digests` - for longer works, if it is worth reading, it is worth taking notes on
6. `external` - copies of external outlines worth keeping handy


## Github Pages

- Portray is configured in `pyproject.toml`
- requiring the project to have a `docs` directory for now (maybe there is some hack to get rid of the `docs/` top level directory.

### Rebuilding

- Rebuild github pages in the `~/code/outlines` project root using virtualenv: `~/virtualenvs/portray`.
  - publish with the command: `portray on_github_pages`
- Rebuild the portray virtualenv by simply installing `portray` and `mkdocs-awesome-pages-plugin`.

The [github pages](https://robbintt.github.io/outlines/) are rendered with [portray](https://timothycrosley.github.io/portray/) and [mkdocs-awesome-pages-plugin](https://github.com/lukasgeiter/mkdocs-awesome-pages-plugin)

- [github pages reference](https://docs.github.com/en/pages/quickstart)
