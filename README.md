# OEIS A398184: maximal no-three-in-line subsets of the n X n grid

<!-- oeis-status:begin -->
**OEIS status** (lab registry, 14 Nov 2026):

- [A398184](https://oeis.org/A398184), a(9), a(10): maximal no-three-in-line subsets: **approved** (2026-11-12: approved). Certificate: complete.
- [A398184](https://oeis.org/A398184), supporting file: maximal subsets by size, n = 1..10: **approved** (2026-11-13: approved (live revision #73)). Certificate: complete.

Rules and the full registry: [athanor-oeis](https://github.com/iwasborninbali/athanor-oeis/blob/main/REGISTRY.md).
<!-- oeis-status:end -->

[A398184](https://oeis.org/A398184): the number of maximal subsets of the n X n grid with no three collinear points (no further grid point can be added without creating a collinear triple). Rotations and reflections are counted separately.

This repository holds the programs, data and checks behind the terms we contributed to this sequence. It concerns
A398184 only; the related sequences have their own repositories ([oeis-A398172](https://github.com/iwasborninbali/oeis-A398172), [oeis-A398580](https://github.com/iwasborninbali/oeis-A398580)).

| n | a(n) |
|---|---|
| 1 | 1 |
| 2 | 1 |
| 3 | 23 |
| 4 | 347 |
| 5 | 5646 |
| 6 | 116411 |
| 7 | 2445518 |
| 8 | 66509584 |
| 9 | 1861878186 |
| 10 | 56412888628 |

a(9) and a(10) are our contribution (approved in the OEIS on 12 Nov 2026); a(8) is from Sean A. Irvine. The counts by size are in `a398184.txt`.

## How the terms were computed

- **n ≤ 7** (September 2026): two independent exhaustive Python programs (`python/`), sharing no code.
- **n = 8**: first computed by Sean A. Irvine (September 2026); reproduced here by both C programs below.
- **n = 9** (3 November 2026) and **n = 10** (5 November 2026): two independently written exhaustive C programs in
  [`programs/`](programs/) (method in `programs/method.md`):
  - `line_rows.c`: a row-by-row search over row patterns (empty, one or two points), with occupancy counters on every
    lattice line through at least three grid points, analytic completion of the last row and a justified reflection reduction;
  - `determinant_check.c`: a point-by-point traversal that tests every triple with an integer determinant and uses no
    symmetry weights (adapted from the September program `tri.c`, credited as such; `original_*.c` are the earlier versions).
  Both split the search by the first two rows into deterministic frontiers; frontier i goes to shard i mod S, so every
  subset is counted in exactly one shard. For n = 10 each program completed 512 of 512 shards and they agree in every cell
  (see [`n10/`](n10/)). Through n = 9 they also match `programs/reference/`.

Build and run one shard (any C compiler):

```sh
cd programs && ./build.sh
./line_rows N --shard i --shards S --split-rows R
./determinant_check N i S R
```

## Contents

| Path | What |
|---|---|
| [`b398184.txt`](b398184.txt) | a(1)–a(10) |
| [`a398184.txt`](a398184.txt) | the numbers of maximal subsets by size, n = 1..10 (also uploaded to the OEIS entry) |
| [`python/a398172.txt`](python/a398172.txt) | the two September Python programs (they count A398172 and A398184) |
| [`programs/`](programs/) | the two exhaustive C programs, build script, collector and auditor, method, small-n references |
| [`n10/`](n10/) | the n = 10 profile and the 1,024 shard outputs with receipts, and how to recheck them |

## Author and licence

Aleksei Kudriashov (ORCID 0009-0006-8885-5338), Athanor lab, with AI assistance (OpenAI Codex cores; Claude Code as the
lab's guide). Code: MIT; data and text: CC BY 4.0 (see `LICENSE.md`). The same computation is also part of the lab's
broader archive [no3-results](https://github.com/iwasborninbali/no3-results).

[Verification certificate](CERTIFICATE.md) and [prior-art record](PRIOR-ART.md).
