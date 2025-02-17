### Kap padaryt "uv_labas" Python package su `uv`

#### Projekto struktura
```
.
├── README.md
├── pyproject.toml
├── src
│   └── uv_labas
│       ├── __init__.py
│       ├── example.py
│       ├── py.typed
│       └── return_hello.py
├── tests
└── uv.lock
```

#### Kap sukurt
1. `uv init --lib uv_labas`
2. Create virtual env: `uv venv`
3. `source .venv/bin/activate`

#### Kap paleist koda
4. `uv run`
5. `uv build`

#### Kap pridet / ismest deps
6. `uv add/remove <package name>` ARBA rankomis pridet `dependencies = []` @ `pyproject.toml`

### Source
https://sarahglasmacher.com/how-to-build-python-package-uv/
https://docs.astral.sh/uv/guides/projects/#building-distributions
