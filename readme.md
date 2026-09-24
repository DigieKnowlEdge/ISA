# ISA Training Repo

## Local Development

### Serve locally

```uv run mkslides serve docs/lessons```

```uv run mkdocs serve```

### Build and review locally

```uv run mkdocs build```

```uv run mkslides build docs/lessons -d site/slides/lessons```

```uv run python -m http.server 8000 --directory site --bind 127.0.0.1```