# The zzData experiment

Version 0.1 — established 2026-08-20. Status: **defined, not yet running.**

This document is the rigorous definition of the experiment. The [README](../README.md)
is the public summary; this is the part that is supposed to stop us from fooling
ourselves later.

It is written *before* any implementation exists, deliberately. Committing to the
evidence standard in advance is what makes the eventual result worth anything. Amend
it by dated addition rather than silent rewrite, so that what we claimed, and when we
claimed it, stays auditable in Git history.

---

## 1. Hypothesis

**H1 (primary).** An autonomous machine agent, acting on behalf of some third party
we have no relationship with, will voluntarily pay a small amount of money for
structured, trustworthy, machine-readable access to information that it could have
obtained for free from the human-readable web, because paying is cheaper for it than
doing the extraction and maintenance work itself.

**H0 (null).** It will not. Given a free human-readable source, machines will either
scrape it, ignore it, or never discover the paid alternative at all — and no
externally controlled agent will voluntarily settle a payment.

H0 is the default expectation. A null result is a real result and will be published as
one.

**H2 (secondary, only reachable if H1 survives).** Voluntary machine payments can
cover the operating cost of serving them.

---

## 2. Research question

> Will an unknown machine on the Internet discover zzData and voluntarily pay a very
> small amount for convenient, trustworthy, structured access to data that it could
> technically obtain for free from the human-readable web?

Decomposed, this is four questions that must succeed in order:

1. **Discovery** — can a machine we did not tell about zzData find it?
2. **Comprehension** — can it understand what is offered and what it costs?
3. **Willingness** — does it decide that paying beats extracting?
4. **Settlement** — can it actually complete the payment and get the resource?

Each stage can fail independently. Failure at stage 1 is the most likely outcome and
says nothing about stage 3. When reporting results we must state *which* stage failed
rather than collapsing everything into "machines won't pay."

---

## 3. Free information versus paid convenience

The distinction the experiment rests on:

| | Cost of the information | Cost of the work |
| --- | --- | --- |
| Human reading a public page | free | their own time and attention |
| Determined machine scraping it | free | build, run, and *maintain* an extractor |
| Machine calling zzData *(proposed)* | priced | approximately zero |

A human or a determined machine can always take the free route:

```
find → retrieve → understand → extract → normalize → validate → maintain
```

zzData proposes to replace it with:

```
request → HTTP 402 → tiny payment → clean structured result
```

The information is not the product. The **avoided work** is the product — and the
largest component of that work is ongoing maintenance, because sources change shape
and somebody has to keep noticing.

This framing has a consequence worth stating plainly: if the underlying source is
trivially and stably scrapable, zzData *should* fail for that dataset, and that is
useful information about where the value actually lives.

---

## 4. What constitutes evidence

Evidence is tiered. Each tier is strictly stronger than the one below it, and a claim
may only be made at the tier actually reached.

**Tier 0 — Traffic.** Requests arrive. *No evidential value whatsoever.* Recorded only
to characterise background noise.

**Tier 1 — Capability discovery.** An externally controlled client we did not direct
retrieves a machine-readable description of what zzData offers (catalogue, manifest,
schema, or equivalent) and its subsequent behaviour shows it parsed rather than merely
fetched it — for example, it then requests a specific resource named only inside that
description.

**Tier 2 — Priced challenge understood.** An external client receives a payment
challenge, and its follow-up request demonstrates it interpreted the terms rather than
blindly retrying: it addresses the correct resource with a correctly shaped payment
attempt. A retry loop that ignores the challenge does not qualify.

**Tier 3 — Settled purchase.** An externally controlled client successfully settles a
payment and retrieves the resource, without us manually directing that individual
transaction. **This is the threshold result the experiment exists to test.**

**Tier 4 — Repetition and independence.** Tier 3 recurs — across time, and ideally
across distinct counterparties we have no relationship with. Repetition is what
separates a one-off curiosity from an economic behaviour.

**Tier 5 — Sustainability.** Cumulative voluntary revenue meets or exceeds the
operating cost of the service over a stated period. This addresses H2.

For any claim at Tier 1 or above, we must be able to state: what the counterparty was,
how we know it was not us, what it requested, what it was quoted, what it paid, and
what it received. If we cannot reconstruct that record, the observation does not count.
That requirement is a design constraint on telemetry, not an afterthought.

---

## 5. What does NOT constitute evidence

None of the following may ever be presented as evidence of organic machine purchase
intent, no matter how encouraging the graph looks:

- **Search-engine and archive crawling.** Indexing is not purchasing.
- **Uptime and availability monitoring.** Including third-party monitors we did not
  configure.
- **Vulnerability and port scanning.** Including anything that fetches `/.env`,
  `/wp-login.php`, or similar.
- **Bots hitting random or nonexistent paths.** Undirected probing is noise.
- **Payment-protocol probing.** A scanner that reflexively pokes `402`/x402-shaped
  endpoints because they are fashionable is not expressing demand. This is expected to
  become a common false positive and must be actively filtered.
- **Our own traffic.** Tests, CI, local development, benchmarks, smoke checks,
  deployment verification. All of it must be attributable and excluded by construction,
  not by after-the-fact guessing.
- **Manual requests.** A human running `curl`, or clicking through in a browser, is a
  human.
- **Transactions we directed.** An agent we built, configured, funded, prompted, or
  asked a friend to point at zzData is a *functional test*. Functional tests prove the
  plumbing works. They prove nothing about demand, and must be reported separately and
  labelled as such.
- **Mentions and interest.** Stars, links, social posts, or an LLM describing zzData in
  conversation.
- **Aggregate volume as a substitute for attribution.** "Lots of machine traffic"
  without per-transaction provenance is a Tier 0 observation dressed up.

**Ambiguity rule.** Where we cannot determine whether a counterparty was autonomous or
human-driven, we report the ambiguity. We do not resolve it in the direction that
flatters the hypothesis.

---

## 6. Core ethical and product constraints

These bound the experiment. Violating one does not produce a better result; it
produces an invalid one.

1. **Humans keep normal free access** to the underlying public information. This is
   non-negotiable and takes precedence over any commercial or experimental objective.
2. **No manufactured scarcity.** We do not degrade the human experience, obfuscate
   values, add artificial CAPTCHA friction, hide information to force API usage, or
   block reasonable human access to create demand.
3. **No misrepresentation of ownership.** Public information is not presented as
   proprietary, exclusive, or otherwise ours.
4. **Provenance is preserved.** Every value should be traceable to where it came from
   and when it was observed.
5. **Source data is never fabricated.** Not for demos, not to fill a gap, not to make
   a schema look complete. If a value is unknown it is absent or explicitly null.
6. **Respect the sources.** Reasonable request rates, honour stated terms, and prefer
   sources whose terms permit what we are doing.
7. **Claims distinguish built from planned.** In this repository, in the README, and in
   any public metrics or write-up.
8. **Financial actions stay tightly bounded.** Small, capped, auditable, reversible
   where possible, and never granted open-ended spending authority.
9. **Publish nulls.** If the hypothesis fails, that is the finding.

---

## 7. Experiment stages

Provisional and non-binding. Stage boundaries exist so that we notice when we are
about to skip a prerequisite, not to lock in a plan.

| Stage | Goal | Question it answers |
| --- | --- | --- |
| **0. Bootstrap** *(current)* | Repository, intent, principles, evidence standard | — |
| **1. Architecture** | Smallest design capable of answering the question; telemetry schema; dataset selection criteria | What is the minimum we must build? |
| **2. Free machine-readable baseline** | Publish something structured, free, and discoverable | Will machines find it at all? |
| **3. Priced path** | Introduce a payment challenge on a subset, human path untouched | Do machines understand a price? |
| **4. Settlement** | Real micropayment settlement, capped | Can a machine actually pay? |
| **5. Observation** | Public metrics, honestly attributed | Does anyone pay voluntarily? |
| **6. Sustainability** | Revenue against operating cost | Can it fund itself? (H2) |
| **7. Supply side** *(speculative)* | Autonomous data maintenance | Can the work of upkeep be automated too? |

Stage 2 is the real gate. If nothing ever discovers zzData, stages 3–6 are untestable
and the honest conclusion is "discovery failed", not "machines won't pay". Discovery
should therefore be measured before pricing is introduced, so we can tell the two
failures apart.

---

## 8. Threats to validity

Known ways this experiment could mislead us:

- **We cannot fully verify autonomy.** A payment could come from a human tinkering with
  an agent for fun. Curiosity is not economic demand, and at small volumes the two are
  hard to separate. Repetition over time is our main defence.
- **Tiny samples.** A handful of transactions cannot support a general claim about
  machine economic behaviour. Report n.
- **Selection effects.** Our choice of datasets determines the answer. An easily
  scrapable source predicts failure; a genuinely painful one predicts success. Neither
  generalises far.
- **Novelty effects.** Early interest in anything x402-shaped may reflect enthusiasm
  for the protocol rather than value in the data.
- **Observer effect.** Publicising the experiment attracts participants who are here
  for the experiment, not for the data. That traffic is closer to a directed test than
  to organic demand and should be treated with suspicion.
- **Our own optimism.** The most likely failure mode is us reclassifying noise as
  signal. Section 5 exists specifically to make that harder.

---

## 9. Measurement

Detailed telemetry design belongs to the architecture stage. Two things are already
fixed by this document:

- A Cloudflare D1 database named `agent_economics` exists and is intended to hold the
  economic and experimental telemetry. It is currently empty of any zzData schema. Its
  schema will be defined through migrations tracked in this repository.
- Whatever the schema turns out to be, it must be able to answer, per transaction: who
  the counterparty was, whether it was us, what it discovered, what it was quoted, what
  it settled, and what it received. Section 4 is unenforceable otherwise.

---

## 10. Open questions

Recorded now so they are not quietly resolved by accident later:

- How does a machine discover a paid capability it was never told about?
- What is the right price for a unit of avoided work, and can it be derived rather
  than guessed?
- Which datasets have a maintenance cost high enough to be worth paying to avoid?
- What makes structured data *trustworthy* to a machine — provenance, freshness,
  schema stability, or a guarantee of some kind?
- Would a machine rather pay per request, or pay once for a promise about the future?
- Is there any honest way to distinguish an autonomous economic decision from a human
  experimenting?
