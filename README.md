# Two-round continuation probe — round 1

This repository is the first round of a public two-round continuation probe. Its only output
is a two-line marker file, `artifacts/chronicle.md`, that a later round can read to confirm it is
continuing the same lineage.

## Status — read this first

- **There is no code here.** No contracts, scripts, libraries, tests or web pages. Nothing is
  deployed anywhere, and nothing in it holds, moves or touches funds.
- **Only round 1 exists.** The chronicle ends at `R1`. Round 2 (`R2`) is deliberately not
  present; adding it is the job of a later round, not this one.
- **The chronicle is a delivered output, not a tracked file.** `artifacts/chronicle.md` is
  uploaded separately from the source and is left untracked in Git. A fresh clone therefore
  contains this README and `docs/`, but **not** `artifacts/chronicle.md`. See
  [docs/chronicle.md](docs/chronicle.md).
- **Where this differs from the brief.** The brief asked to "write the README and documentation"
  for a project, and to "keep [the chronicle] in the delivered repository". When this round
  started, the repository was a single empty commit (`0243d7d Empty workspace`) with no tracked
  files. The files visible in the working directory then (`package.json`, `.env*`, lock files,
  `node_modules/`, `.github`, `scripts`, and others) were empty placeholders or null devices
  supplied by the build environment; none of them was tracked, and none is part of this project.
  So this README documents the one artifact, not a buildable program.

## Build

Nothing to build. Clone and enter the repository:

```sh
git clone <this repository> probe && cd probe
```

## Test

There is no test suite. The only checkable property is the chronicle's exact contents. Once you
have the delivered `artifacts/chronicle.md` (it is not in the clone; see Status), run from the
repository root:

```sh
printf 'LINEAGE_GATE_0x4d9ba887eea71e29c152c4ee8a287885c404b311466f43a1e2d66186f455de78\nR1\n' \
  | cmp - artifacts/chronicle.md && echo "chronicle OK"
```

It prints `chronicle OK` and exits 0 on a byte-exact match. Otherwise `cmp` reports the first
differing byte, or says the file does not exist, and exits non-zero.

## Use

A later round reads the chronicle and checks it before continuing:

```sh
head -n 1 artifacts/chronicle.md   # LINEAGE_GATE_0x4d9b...de78
sed -n 2p artifacts/chronicle.md   # R1
```

## Entry points

| Entry point | Who can use it | Fails when |
| --- | --- | --- |
| `artifacts/chronicle.md` (read) | anyone with the delivered artifact | the file is missing (it is never in a fresh clone), or its bytes differ from the two lines above |

There are no functions, contracts, commands or pages. Full format:
[docs/chronicle.md](docs/chronicle.md).
