# swarm-benchmark-evidence

This repo is a public **commitment** to a set of benchmark results that
are not yet released in full. It serves two purposes:

1. **Timestamp**: a permanent, world-visible record that specific results
   existed in a specific form on a specific date.
2. **Integrity proof**: the cryptographic hash below pins the exact bytes
   of the unreleased evidence bundle so that, when the full archive is
   released later, anyone can verify it has not been edited after the
   fact.

The actual evidence bundle (per-instance patches, cleanroom verdicts,
reproducibility metadata) is held privately and will be released
publicly when ready. The bundle's content is described at a high level
in [`summary.md`](summary.md); the byte-exact commitment is in
[`hash.txt`](hash.txt).

## What is in the held archive (high level)

- Per-instance AI-generated source-only patches (`patch.diff`) for a set
  of public software-engineering benchmark instances.
- Deterministic cleanroom verdict files (`verdict.json`) recording the
  result of applying each patch and running the benchmark's hidden test
  suite inside the curator's published Docker image.
- Public benchmark identifiers (`meta.json`: `instance_id`,
  `base_commit`, `container_image`) sufficient to reproduce.

The bundle does **not** include any agent-system internals, prompts,
chain-of-thought, or methodology details. When released, the bundle
will be a stand-alone evidence artifact that any reviewer with Docker
can independently verify by re-running the cleanroom pipeline.

## Verifying when the bundle is released

When the held bundle is later published, anyone can run:

```bash
sha256sum swarm-benchmark-results-<short>.tar.gz
```

and confirm the hash matches [`hash.txt`](hash.txt). If the hashes
match, the bundle's bytes are identical to what was committed on this
repo's timestamp.

## Why bother with a commitment

Releasing AI benchmark results invites the obvious question "did you
cherry-pick or edit the patches after seeing the verdicts?" The hash
commitment removes that ambiguity: the bytes were fixed at the time
this repo was created, before any external review. Anything published
later that does not match the committed hash is not the original
bundle.
