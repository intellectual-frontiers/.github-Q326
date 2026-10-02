# Intellectual Frontiers LLC — Company facts

> **Status: canonical for narrative facts.** This file is the source of
> truth for how Intellectual Frontiers describes itself. `intellectualfrontiers.com`
> should sync from it, not the reverse.
>
> **Not canonical for registry facts.** The formation date, Maryland
> Department ID, and standing below are stated as of a 2026-09-14 manual
> check of the Maryland Department of Assessments and Taxation's business
> entity search — they can drift out of date, and that search is the
> actual source of truth for them, not this file. Re-check the source
> before relying on these for anything time-sensitive. See the claims
> standard at the bottom of this file.
>
> **What this file leaves out on purpose:** the SDAT record also lists a
> resident agent and a principal office street address. Per the
> non-disclosure policy below, neither is repeated here even though both
> are a matter of public record at SDAT.
>
> Distilled from `src/content/corporate.ts` at commit `6260a3b` of
> `intellectual-frontiers/www.intellectualfrontiers.com-aiw-lovable`
> (2026-09-13), the last point this text was copied from.
>
> **Reconciled 2026-10-01** with Lovable commit `5688cba`: the unit's name
> in "What each unit asks" (`corporate.ts`, `unitQuestions`) and the new
> "Operating proposition" section below (`src/content/operating-model.ts`,
> added to the website on 2026-09-14, after the `6260a3b` text). The
> registry facts in "Corporate facts" are deliberately not reconciled: the
> website still shows them as awaiting verification, and this file's
> 2026-09-14 SDAT check is newer.

## Opening statement

Intellectual Frontiers LLC is a Maryland limited liability company that
develops, owns, commercializes, funds, builds, and publishes intellectual
assets and ventures organized around Native Alpha.

The company is deliberately lightweight. It owns the capabilities where
control, judgment, rights, relationships, capital allocation, and accumulated
knowledge can compound into advantage, and it uses partners and specialized
providers for work that does not need to become permanent overhead.

That means a small number of people, a large number of records, and a
preference for keeping decisions and rights in house while renting execution.

## Corporate facts

| Fact | Value | Source / note |
| --- | --- | --- |
| Legal name | Intellectual Frontiers LLC | — |
| Entity type | Limited liability company | — |
| Jurisdiction | Maryland, United States | — |
| Location | Silver Spring, Maryland, United States | — |
| Website | [intellectualfrontiers.com](https://www.intellectualfrontiers.com/) | — |
| Formation date | September 5, 2023 | [Maryland Department of Assessments and Taxation](https://egov.maryland.gov/BusinessExpress/EntitySearch), checked 2026-09-14 |
| Maryland Department ID | W24347692 | [Maryland Department of Assessments and Taxation](https://egov.maryland.gov/BusinessExpress/EntitySearch), checked 2026-09-14 |
| Maryland standing | Active; in good standing | [Maryland Department of Assessments and Taxation](https://egov.maryland.gov/BusinessExpress/EntitySearch), checked 2026-09-14 |
| Federal EIN | Provided to counterparties on request | There is no public IRS lookup for a private LLC, so it is not published here. |

**What this company deliberately does not publish:** its resident agent,
a street address, a telephone number, headcount, revenue, financing
details, or ownership percentages. That's a stated policy, from the
corporate fact sheet at commit `adf0aef` (2026-09-14) of the Lovable-managed
web repo — not an oversight in this file.

## Provenance

Intellectual Frontiers acquired all Netspective Communications LLC patents in
2023. Intellectual Frontiers has subsequently continued to develop and
prosecute intellectual property directly.

The age of an underlying invention and the age of Intellectual Frontiers LLC
are different things. Some patent families now owned by Intellectual
Frontiers trace their priority histories back more than a decade.

You do not have to take our word for either statement. Assignment records,
file histories, and priority dates are public — see Verification links,
below.

## What each unit asks

| Unit | Path | Question |
| --- | --- | --- |
| Intellectual Frontiers Research & IP | `/ip` | What do we know, own, control, or have rights to that may create unusual advantage? |
| Intellectual Frontiers Press | `/press` | What do we understand that is worth making clearer, more useful, and more durable? |
| Intellectual Frontiers Capital | `/capital` | What advantage is strong enough that scarce capital should be placed behind it? |
| Intellectual Frontiers Studios | `/studios` | What venture should we create to exploit this advantage, and what is the cheapest credible path to proving whether it deserves to exist? |
| Intellectual Frontiers Network | `/network` | Who has unusual knowledge, capabilities, relationships, reputation, experience, or access relevant to an opportunity, and how do we find them when needed without building another static resume database? |

Full unit charters live in [`context/units/`](units/). Terms used across
this file and the unit charters (Native Alpha, the decision checkpoint,
IPLG, a hunt, and the rest) are defined once in
[`context/glossary.md`](glossary.md).

## Operating proposition

Intellectual Frontiers is a think tank that builds things. It turns unusual
ideas into publications, intellectual property, software, companies, and
investments.

Each unit also has a short question, a role, and the evidence it looks for.
These are the operating-model wording the website uses beside the longer
questions above:

| Unit | Question | Role | Evidence |
| --- | --- | --- | --- |
| Intellectual Frontiers Research & IP | What might be true? | Turns observations into better questions, stronger theses, defensible insights, and tests. A patent is useful evidence, but it does not prove demand. | Research, technical distinctions, rights, and disconfirming findings |
| Intellectual Frontiers Press | Can anyone understand and use it? | Makes a thesis inspectable, then tests it through attention, criticism, adoption, and willingness to pay. | Reader response, changed language, practical use, and paid demand |
| Intellectual Frontiers Capital | Should another dollar move? | Tests the economics and searches for founders already pursuing the thesis. When someone else is better positioned, Capital can back them instead of rebuilding their work. | Underwriting, founder traction, capital interest, governance, and downside |
| Intellectual Frontiers Studios | What is the cheapest useful test? | Builds an experiment when the evidence remains compelling and no better-positioned builder exists. A company is one possible result, not the starting instruction. | Customer behavior, usage, payment, renewal, and repeatable economics |
| Intellectual Frontiers Network | Who should we find, and why now? | Connects every unit to founders, operators, customers, experts, partners, and investors. Finding that someone else is already doing the work can be the most valuable result. | Conversations, worked trials, introductions, capability, and absence |

**The decision at the end of every pass:** continue, change, back someone
else, build it ourselves, or stop. This is the constitution's decision
checkpoint (§6).

**What the result may be:** a publication, a patent or license, a
partnership, an investment in somebody else, a small experiment, software, a
new company, continued research, or a decision to stop. The firm does not
manufacture activity; it improves the decision about which form the evidence
supports.

## Unit boundaries

- A patent does not prove a venture.
- A publication does not prove demand.
- Studio activity does not justify investment.
- Investment does not prove product-market fit.

## Shared services

Not to be confused with IF Studios' own portfolio-facing shared services
(Demand Engineering, Revenue Engineering — see `context/units/studios.md`).
This is the company's back office: legal, finance and accounting,
compliance, and general operations are one shared layer, not five
separate ones. Every unit routes these functions to
independent, specialized providers the same way — the pattern IF Capital
already runs for fund administration, legal, tax, audit, and valuation is
the company-wide pattern, not a Capital-specific arrangement. A function
moves in-house only when the hiring rule is met for that function
specifically (steady, strategically important, financially sound, and
supported by at least 18 months of runway) — not because one unit reached
for a hire before the others needed the same thing.

Added directly by Shahid N. Shah on 2026-09-14, resolving what his own
`native-alpha-to-market-reality.png` diagram named as a gap still to make
explicit. See [`spec-kit/memory/constitution.md`](../spec-kit/memory/constitution.md)
§7.

## Native Alpha, in one line

We look for advantages that already exist rather than manufacturing stories
around fashionable markets: we ask whether someone cares enough to spend
money, time, reputation, access, data, or another scarce resource; we prefer
small credible experiments over large speculative plans; we treat AI as an
amplifier of existing advantage, not as Native Alpha by itself; and we are
willing to stop when the evidence does not justify another dollar or another
month.

The full method is in [`spec-kit/memory/constitution.md`](../spec-kit/memory/constitution.md).

**Evidence chain:** Observation → Possible Native Alpha → Who cares →
Cheapest credible test → Evidence.

**Possible outcomes:** Stop (the evidence does not justify another dollar) ·
Continue (run the next cheapest test) · License (someone else is better
placed to build it) · Build (Studios takes it and finds a first buyer) · Fund
(Capital places money behind proven advantage) · Publish (Press makes the
understanding usable).

## Verification links

| Source | What it shows |
| --- | --- |
| [Maryland Department of Assessments and Taxation](https://egov.maryland.gov/BusinessExpress/EntitySearch) | Business entity search. Look up Intellectual Frontiers LLC for entity type, department ID, and standing. |
| [USPTO Patent Center](https://patentcenter.uspto.gov/) | File histories, office actions, and current status for every application the firm lists. |
| [USPTO Patent Assignment Search](https://assignment.uspto.gov/patent/index.html#/patent/search?q=Intellectual%20Frontiers) | Recorded assignments, including the transfer of the Netspective Communications patents. |
| [Google Patents](https://patents.google.com/?assignee=Intellectual+Frontiers) | Full text of the granted patents and published applications, assignee view. |

## Claims standard

This is the rule this file, and every file in this repository, is written
against:

- Observable facts should be verifiable.
- Opinions should be identifiable as opinions.
- Frameworks should be identifiable as frameworks.
- Illustrations should be identifiable as illustrations.
- A claim does not become a fact because we published it ourselves.

Practically: a fact this repository asserts directly (the opening statement,
the doctrine, the brand rules) is one this repository is the authority on. A
fact that traces to an external record (state registration, a patent grant, a
trademark registration) is linked to that record rather than restated as a
number that could drift out of sync with it.
