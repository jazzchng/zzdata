# zzData

> **structured data for machines that have better things to do**

zzData is a public, exploratory experiment.

It asks one narrow economic question: when information is already freely readable by
humans on the open web, will an autonomous machine *voluntarily* pay a very small
amount for convenient, trustworthy, structured access to it — instead of doing the
extraction work itself?

We do not know the answer. That is the point.

## Status

**Bootstrap.** This repository currently contains documentation only.

| Area | State |
| --- | --- |
| Intent and principles documented | started |
| Architecture / design | not started |
| Dataset catalogue | not started |
| Structured data APIs | not started |
| Payment (`HTTP 402`, micropayments) | not started |
| Agent-native interfaces | not started |
| Deployed service | none |
| Observed machine discovery | none |
| Observed machine payment | none |

Nothing is deployed. Nothing is purchasable. No machine has discovered or paid for
anything from zzData, because there is not yet anything to discover or pay for.

Any capability mentioned below as *possible* is speculative until it appears in this
table as built.

## The research question

> Will an unknown machine on the Internet discover zzData and voluntarily pay a very
> small amount for convenient, trustworthy, structured access to data that it could
> technically obtain for free from the human-readable web?

The load-bearing word is **voluntarily**. We are not trying to manufacture scarcity,
and a machine that pays because we cornered it into paying would tell us nothing.

The rigorous version of the experiment — hypothesis, what counts as evidence, what
explicitly does not, and how we intend to avoid fooling ourselves — is in
[docs/experiment.md](docs/experiment.md).

## The name

`zz` is meant to read as sleepy: lazy, low-effort, convenient.

The claim is *not* that zzData holds anything rare. Anyone, and any sufficiently
determined machine, can go get the underlying information for free. But getting it
means doing a chain of work:

```
find → retrieve → understand → extract → normalize → validate → maintain
```

That chain has a real cost even when the information itself costs nothing. The cost
is mostly in the last step: things drift, layouts change, formats rot, and somebody
has to keep noticing.

zzData proposes to sell the removal of that chain:

```
request → HTTP 402 → tiny payment → clean structured result
```

Whether the second route is worth paying for is the entire experiment.

## Humans keep free access

This is a hard constraint, not a courtesy.

zzData will not:

- degrade the human experience of the underlying public information,
- obfuscate values,
- introduce artificial CAPTCHA friction,
- hide information merely to force API usage,
- misrepresent public information as proprietary or exclusive,
- or block reasonable human access in order to create demand.

If zzData can only work by making the free path worse, then the hypothesis is not
supported and the honest result is to say so. Coerced demand would invalidate the
experiment, not rescue it.

## What would be sold

Convenience, and nothing more exotic than that:

- machine-readable structure
- stable schemas
- predictable interfaces
- provenance for every value
- validation
- freshness metadata
- reduced extraction work
- reduced inference and computation on the caller's side
- reduced maintenance burden as sources change

What would **not** be sold: exclusivity, ownership of the underlying public
information, or access that is otherwise unavailable.

## Possible future directions

Speculative and explicitly uncommitted. Listed so the intent is on the record, not
as a roadmap:

a machine-readable dataset catalogue · structured data APIs · `HTTP 402 Payment
Required` · machine-to-machine micropayments · x402 or another suitable payment
protocol · dataset provenance · economic telemetry · public experiment metrics ·
crawler and agent discovery · MCP or other agent-native interfaces · deterministic
pricing experiments · an autonomous supply and data-maintenance agent · agent
economic accounting · and eventually testing whether the service can pay for its own
operating costs.

The intent is to build the *smallest* system that can answer the current question,
and to let structure appear only when a real requirement demands it.

## Relationship to other projects

zzData is an independent project. It is intended to be independently deployable and
will not live inside any website repository.

[jazzchng.com](https://jazzchng.com) is a separate personal website that may later be
one source of human-readable datasets referenced by this experiment. No integration
exists today.

## License

[MIT](LICENSE) — for the code in this repository.

The license covers this repository's own code. It does not grant any rights over
third-party source data that the experiment may later reference; provenance and
per-dataset terms will be handled explicitly, per dataset, if and when a catalogue
exists.
