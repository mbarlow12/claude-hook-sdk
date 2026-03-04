# Workflow

```bash
# Lint and style
python -m ruff check src/ tests/ --fix
python -m ruff format src/ tests/

# Typecheck (only done for src/)
python -m mypy src/

# Run all tests
python -m pytest tests/
```

# Codebase Structure

- `src/claude_agent_sdk/` - Hook type definitions package
  - `__init__.py` - Public API exports (hook inputs, outputs, callback, context, matcher)
  - `types.py` - All TypedDict and dataclass definitions
  - `_version.py` - Package version
  - `py.typed` - PEP 561 typed package marker
- `tests/test_types.py` - Unit tests for hook type definitions
