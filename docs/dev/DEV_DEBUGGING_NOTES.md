# Gevals Debugging Notes

This project supports an opt-in debugging mode that preserves the temporary
files created while the agent runs. Enable it per invocation:

```bash
GEVALS_DEBUG=1 ./gevals eval <path-to-eval>
```

If you prefer a CLI option, pass `--debug` to `gevals eval` and the flag will
export `GEVALS_DEBUG=1` for the duration of the run.

When `GEVALS_DEBUG` is set, the agent runner creates a directory such as
`/tmp/gevals-debug-XXXXXXXX`. If the agent command fails, the error message will
include the exact path. Inside you will find:

- `config.toml` – the Codex configuration file generated for the attempt.
- `prompt.txt` – the raw prompt sent to Codex.
- `codex-home/` – the transient Codex state directory.
- `codex.log` – Codex stdout/stderr (JSON event stream when `--json` is enabled).
- `debug.log` – metadata such as the Codex command line and exit status.

These artifacts make it easier to compare the generated configuration with a
working local setup and inspect the HTTP error returned by the Codex CLI.
Remember to delete the directory manually after you finish debugging.
