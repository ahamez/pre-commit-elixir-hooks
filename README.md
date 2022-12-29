# pre-commit-elixir-hooks

Git hooks for Elixir using [pre-commit](https://pre-commit.com).

## Usage

First, make sure that `pre-commit` is installed and that `mix` is available in `PATH`.

Configure hooks as follows:

```yaml
repos:
  - repo: https://github.com/ahamez/pre-commit-elixir-hooks.git
    rev: v1.0.0
    hooks:
      - id: elixir-mix-format
      - id: elixir-mix-credo
      - id: elixir-mix-deps-check-unused
      - id: elixir-mix-dialyzer
      - id: elixir-mix-test
        args: ["--exclude", "some_tag"]
```

Then, install hooks:

```sh
pre-commit install
```

## Usage with different stages

As some actions are slow to perform (like `mix dialyzer`), you can confine them to specific stages, like `pre-push`:

```yaml
repos:
  - repo: https://github.com/ahamez/pre-commit-elixir-hooks.git
    rev: v1.0.0
    hooks:
      - id: elixir-mix-format
        stages: [commit]
      - id: elixir-mix-credo
        stages: [commit]
      - id: elixir-mix-deps-check-unused
        stages: [push]
      - id: elixir-mix-dialyzer
        stages: [push]
      - id: elixir-mix-test
        args: ["--exclude", "some_tag"]
        stages: [push]
```

Then, install hooks:

```sh
pre-commit install && pre-commit install -t pre-push
```
