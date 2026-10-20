# `artifacts/chronicle.md` — format

The chronicle is the probe's only output. In round 1 it is exactly 83 bytes: two lines, each
ending in a single `\n`, encoded as UTF-8/ASCII, with no other content:

| Line | Content | Meaning |
| --- | --- | --- |
| 1 | `LINEAGE_GATE_0x4d9ba887eea71e29c152c4ee8a287885c404b311466f43a1e2d66186f455de78` | Lineage marker. The 32-byte hex value is given verbatim by the requester. This repository does not compute or verify it, and says nothing about where it came from. |
| 2 | `R1` | Round 1 has been completed. |

## Rules

- **Do not add `R2` in round 1.** A third line `R2` would claim that round 2 is done.
- Line 1 must stay byte-identical. Changing any character breaks the lineage check.
- Nothing more is specified. The brief does not say whether a later round appends `R2`
  as line 3 or replaces line 2. That is for the round-2 brief to define.

## Delivery

The file is created in the working tree and deliberately left **untracked**. The delivery
process uploads it separately from the Git history, so a fresh clone does not contain it. To check
a copy you have received, run the `cmp` command in the [README](../README.md#test).

## Failure modes

- **File absent**: expected in a fresh clone. Get the delivered artifact.
- **Trailing whitespace, CRLF line endings, or a missing final newline**: the byte-exact check
  fails, even if the file looks correct.
- **Extra line `R2`**: the file was changed after round 1, or by mistake.
