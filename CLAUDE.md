# CLAUDE.md

Guidance for working in this repository. These are durable principles, not task
instructions.

## What this project is

zzData is an exploratory experiment testing whether an autonomous machine will
*voluntarily* pay a small amount for convenient, structured access to information that
is already free to humans on the open web.

Read [docs/experiment.md](docs/experiment.md) before making design decisions. It
defines the hypothesis, the evidence standard, and the constraints — and most design
questions here are really questions about whether the experiment stays measurable.

## Working principles

### Understand before modifying

Read the surrounding code and the relevant docs before changing anything. In a repo
this small the cost of reading everything is near zero, so there is no excuse for
guessing.

### Keep the experiment measurable

Every feature should either help answer the current research question or get out of the
way. Before adding something, ask what observation it makes possible. If a change makes
it harder to tell our own traffic from a third party's, it is a regression regardless of
how good the feature is.

### Do not manufacture artificial scarcity

Humans keep normal free access to the underlying public information. Never degrade the
human path, obfuscate values, add artificial friction, hide information to force API
use, or misrepresent public data as proprietary. Coerced demand invalidates the
experiment rather than proving it.

### Preserve provenance

Every value should be traceable to its source and to when it was observed. Provenance is
part of the product, not metadata we can drop when it is inconvenient.

### Never fabricate source data

No invented values — not for demos, not for tests presented as real, not to fill a gap
in a schema. Unknown means absent or explicitly null. Fabricated data in a project whose
entire premise is trustworthiness is a fatal error, not a shortcut.

### Prefer deterministic code

If a task can be done with parsing, arithmetic, or a lookup, do that. Reserve model
inference for problems that genuinely require judgment, and make it obvious in the code
and in the output which values were inferred rather than extracted.

### Keep financial actions tightly bounded

Anything touching money is small, capped, auditable, and explicit. No open-ended
spending authority, no unbounded retries against a paid endpoint, no implicit
transactions. Payment-related code paths should be the most boring code in the
repository.

### Migrations belong in Git

Database schema changes are versioned migrations committed here, applied forward, never
edited after the fact. Schema state that exists only in a live database is not a schema,
it is an accident. The same applies to `agent_economics` once it holds anything.

### Secrets never belong in Git

No keys, tokens, wallet material, seed phrases, account identifiers, or environment
values in tracked files. Use the platform's secret storage; keep local values in
gitignored files, with committed `.example` templates if a shape needs documenting. If a
secret does land in a commit, rotate it — removing it from history is not sufficient.

### Distinguish implemented from planned in public claims

The README, docs, and any public metrics must never imply that something exists when it
does not. Specifically: do not state or suggest that autonomous agents are discovering
or purchasing data from zzData unless that has actually been observed and can be
attributed under the evidence rules in `docs/experiment.md`. Use present tense only for
what is built.

### Prefer the smallest architecture that answers the current question

Build what the current stage needs. The repository structure should grow when a real
requirement appears, not in anticipation of one.

### Avoid speculative abstractions

No interfaces with one implementation, no configuration for cases that do not exist, no
plugin points for hypothetical sources, no placeholder files or directories. Duplication
is cheaper to fix than a wrong abstraction.

### Test economic and idempotency behaviour carefully

Once payment exists, the important tests are the unglamorous ones: a payment settled
once must never deliver twice or charge twice; replayed requests must be safe;
concurrent requests for the same resource must not double-charge; partial failures must
leave a recoverable state. Test the failure paths, not the happy path.

## Repository conventions

- TypeScript on Cloudflare is the intended direction, but no runtime, framework, or
  build tooling has been chosen or installed. Do not add any speculatively — a
  dependency should arrive with the code that needs it.
- Documentation lives in `docs/`. Long-form reasoning goes there, not in commit
  messages.
- Conventional commit-style messages (`feat:`, `fix:`, `chore:`, `docs:`).
- `docs/experiment.md` is amended by dated addition, not silently rewritten. Its value
  depends on being auditable against Git history.

## External context and boundaries

- **`agent_economics`** — a Cloudflare D1 database that already exists, created
  manually. It is intended to hold zzData's economic telemetry eventually. Do not
  modify it, create tables in it, or create additional D1 databases without an explicit
  instruction to do so. Its schema, when it arrives, comes from migrations in this repo.
- **`jazzchng.com`** — a separate personal website that may later be one source of
  human-readable datasets. zzData is an independent project and must remain
  independently deployable. There is no integration, and adding one is a deliberate
  decision, not a convenience.
- Do not create cloud resources as a side effect of some other task. Provisioning is
  always an explicit, requested step.
