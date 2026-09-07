# llm-batch-dev

Batch prompt runner with real rate limiting and retries

## Examples

```bash
python batch.py prompts.jsonl -o answers.jsonl --workers 4 --rpm 300
```

## Installation

```bash
pip install -r requirements.txt
export OPENAI_API_KEY=sk-...
```

## What it does

- 4xx fails fast; 429 and 5xx retry with jittered backoff
- JSONL in, JSONL out: the input is streamed line by line
- Failures go to a sidecar file with error type, message and status
- Real rate limiting: sliding windows on requests/min and tokens/min
- Per-row overrides for model, system, temperature and max_tokens
- Idempotent: ids already in the output are skipped on a rerun
- Progress, token counts and a cost estimate on stderr
- A bad input line is logged and skipped, never fatal

## Project structure

```text
├── .github/
│   └── workflows/
│       └── ci.yml
├── docs/
│   ├── configuration.md
│   ├── development.md
│   ├── faq.md
│   ├── tradeoffs.md
│   └── usage.md
├── examples/
│   └── quickstart.md
├── tests/
│   └── test_smoke.py
├── .gitignore
├── CHANGELOG.md
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── LICENSE
├── SECURITY.md
├── batch.py
├── prompts.sample.jsonl
└── requirements.txt
```

## Development

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python -m pytest -q
```

## Changelog

- `0.1.1` - fix edge case in argument parsing
- `0.1.0` - first working version

## License

MIT. Do whatever you want.
