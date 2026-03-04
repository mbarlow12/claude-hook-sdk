# Claude Agent SDK — Hook Type Definitions

Python type definitions for [Claude Code hooks](https://docs.anthropic.com/en/docs/claude-code/hooks). This package provides typed inputs, outputs, and utilities for building Claude Code hook scripts.

## Installation

```bash
pip install claude-agent-sdk
```

Requires Python 3.10+.

## What's Included

- **Hook inputs** — Typed dictionaries for each hook event (`PreToolUseHookInput`, `PostToolUseHookInput`, `StopHookInput`, etc.)
- **Hook outputs** — `SyncHookJSONOutput`, `AsyncHookJSONOutput`, and per-event specific outputs (`PreToolUseHookSpecificOutput`, etc.)
- **Hook event type** — `HookEvent` literal type covering all event names
- **Hook callback** — `HookCallback` callable type for SDK-style hook functions
- **Hook context** — `HookContext` type for callback context
- **Hook matcher** — `HookMatcher` dataclass for matching hooks to tool names

## Usage

```python
from claude_agent_sdk import (
    PreToolUseHookInput,
    SyncHookJSONOutput,
    PreToolUseHookSpecificOutput,
)

# Type-check hook input
def handle_pre_tool_use(input_data: PreToolUseHookInput) -> SyncHookJSONOutput:
    if input_data["tool_name"] == "Bash":
        command = input_data["tool_input"].get("command", "")
        if "rm -rf" in command:
            return SyncHookJSONOutput(
                hookSpecificOutput=PreToolUseHookSpecificOutput(
                    hookEventName="PreToolUse",
                    permissionDecision="deny",
                    permissionDecisionReason="Dangerous command blocked",
                )
            )
    return SyncHookJSONOutput()
```

See the [Claude Code hooks documentation](https://docs.anthropic.com/en/docs/claude-code/hooks) for details on hook events and output fields.

## Development

```bash
# Install dev dependencies
pip install -e ".[dev]"

# Lint and format
python -m ruff check src/ tests/ --fix
python -m ruff format src/ tests/

# Typecheck
python -m mypy src/

# Run tests
python -m pytest tests/ -v
```

## License and Terms

Use of this SDK is governed by Anthropic's [Commercial Terms of Service](https://www.anthropic.com/legal/commercial-terms), including when you use it to power products and services that you make available to your own customers and end users, except to the extent a specific component or dependency is covered by a different license as indicated in that component's LICENSE file.
