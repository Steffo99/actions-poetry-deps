# `Steffo99/actions-poetry-deps`

Github Action to install Python dependencies via Poetry

## Dependancies

This action depends on the Poetry executable being installed and available on the runner where this action is running.

> Suggestion: use [abatilo/actions-poetry](https://github.com/abatilo/actions-poetry)!

## Inputs

This action has no named inputs.

## Outputs

This action has one named output:

- `pyenv`: The path to the created Python environment.

## Example usage

In a task running pytest for unit tests and coverage on the whole repository:

```yaml
# ...

steps:
  - name: "⬇️ Checkout repository"
    uses: actions/checkout@v3

  - name: "🔨 Setup Python"
    uses: actions/setup-python@v3

  - name: "🔨 Setup Poetry"
    uses: abatilo/actions-poetry@v2.1.4

  - name: "🔨 Setup Poetry Python environment"
    id: pyenv
    uses: Steffo99/actions-poetry-deps@0.2.3

  - name: "🧪 Run tests"
    run: |
      source ${{ steps.pyenv.outputs.pyenv }}/activate
      pytest --verbose --cov=. --cov-report=html
      
  - name: "⬆️ Upload coverage"
    uses: actions/upload-artifact@v3
    with:
      name: "code-coverage-report"
      path: htmlcov
    
# ...
```
