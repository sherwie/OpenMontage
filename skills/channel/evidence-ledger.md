---
name: evidence-ledger
role: Research agent
model: opus
---

# Evidence Ledger

Before any script is written, every factual claim intended for the episode must
have an entry in this ledger. Store it as `projects/<episode-slug>/evidence-ledger.md`.

## Entry format

For each claim:

```
### Claim
[The specific factual statement, as it will appear or be implied in the script]

### Supporting source
[Publication/document, author if named, URL]

### Source date
[Publication date — flag if the underlying event is much older than the source]

### Confidence
High / Medium / Low — Medium or Low claims need a second corroborating source
or must be phrased in the script as reported/alleged, not stated as fact

### Contradicting evidence
[Any source that disputes or complicates this claim — do not omit these]

### Allowed wording
[The most the evidence actually supports — e.g. "internal documents suggest"
vs. "the company knew" are not interchangeable]

### Visual evidence
[What footage/image/document could visually support this claim]

### Rights/licensing
[Source and license for any visual tied to this claim]
```

## Rules

- A claim with only one source and no corroboration gets Medium confidence at
  best, regardless of how authoritative that single source seems.
- If sources conflict, the ledger records both — the script agent decides how
  to handle the conflict (acknowledge it on-screen, or drop the claim), it does
  not get silently resolved at the research stage.
- Numbers (dollar figures, dates, percentages) always get their own ledger entry
  even if they're part of a larger claim — numbers are where hallucination risk
  is highest and easiest to fact-check independently.
- The research agent does not write persuasive framing into the ledger — that's
  the script agent's job. The ledger is facts and sources only.
