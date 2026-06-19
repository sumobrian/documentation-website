# AGENTS.md

## Cursor Cloud specific instructions

### Overview

This is the **OpenSearch Documentation Website** — a Jekyll-based static site that generates the official docs at docs.opensearch.org. It also includes a custom Jekyll plugin (`jekyll-spec-insert`) in `spec-insert/` that auto-generates API documentation from the OpenSearch OpenAPI spec.

### Ruby version

The project requires **Ruby 3.4.5**. It is installed at `~/.rubies/ruby-3.4.5/bin` and added to `PATH` via `~/.bashrc`.

### Key commands

| Task | Command | Working directory |
|---|---|---|
| Install deps | `bundle install` | `/workspace` |
| Dev server | `bundle exec jekyll serve --host 0.0.0.0 --port 4000 --trace` | `/workspace` |
| Dev server (with link checker) | `JEKYLL_LINK_CHECKER=internal bundle exec jekyll serve --host 0.0.0.0 --port 4000 --trace` | `/workspace` |
| RSpec tests | `bundle exec rspec` | `/workspace/spec-insert` |
| RuboCop lint | `bundle exec rubocop` | `/workspace/spec-insert` |

### Caveats

- **Build time**: The initial Jekyll build takes ~3–4 minutes due to ~1700 Markdown pages plus the remote theme download. Incremental rebuilds (after editing a single file) take 60–90 seconds.
- **Base URL**: The site is served at `http://localhost:4000/latest/` (not `/`). The `baseurl` is set to `/latest` in `_config.yml`.
- **Search**: The client-side search feature may not work in local development since it depends on a pre-built search index.
- **RuboCop**: The `spec-insert/` plugin has ~46 pre-existing RuboCop offenses. These are in the upstream code and should not block work.
- **spec-insert plugin**: Located in `spec-insert/`, this is a local gem referenced by `Gemfile` via `:path => './spec-insert'`. It fetches the OpenSearch OpenAPI spec from GitHub and caches it for 24 hours.
- **No database**: This is a purely static site — no database or external services are required.
