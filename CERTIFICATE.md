# Verification certificate

## Claim

- a(9) = 1861878186.
- a(10) = 56412888628.
- Supporting file `a398184.txt`: counts of maximal subsets by size for n = 1..10 (reviewed, pending approval).

## Evidence

| What | Repository path | Author and date | Coverage | Result | Independence / shared code or data |
|---|---|---|---|---|---|
| Producer | `programs/line_rows.c`; `programs/reference/n9.json`; `n10/shards-n10.tar.gz` | Athanor lab, AI assisted; n=9 on 3 Nov and n=10 on 5 Nov 2026; individual coder not identified | Row traversal and recorded profiles | n=9: total 167892639418, maximal 1861878186; n=10: 7287023194031, 56412888628 | Producer |
| Independent check | `programs/determinant_check.c`; `programs/reference/determinant-n9.json`; `n10/shards-n10.tar.gz` | Athanor lab, AI assisted; same dates; individual coder not identified | Determinant traversal, n=9 and 10 profiles | Reports agreement in each size cell; 512/512 n=10 shards each | Independently written enumeration, no shared enumerator code according to `programs/method.md`; same mathematical definition and target data, shared collection/receipt pipeline |
| Receipt and identity check | `programs/collect.py`; `n10/profile-n10.json` | Athanor lab, date and individual author not stated | Recorded n=10 outputs, shard receipts and profile identities | Complete receipts, matching profiles and totals | Reads both producers' stored data; no independent enumeration |

## Replayed for this repository

Executed on 13 Nov 2026 WITA, locally. Commands use the logged working directory; logs contain the full outputs. Wall times include process startup.

- `cc -O2 -std=c11 /Users/iwasborninbali/projects/science/oeis-A398184/programs/determinant_check.c -o /tmp/c7-A398184/determinant_check` — exit 0, 0.119 s; output: compiler produced no output [`logs/certificate-2026-11-13/build-determinant_check.log`](logs/certificate-2026-11-13/build-determinant_check.log) (SHA-256 `f6b73dc24ccfa1ee4f2b0f035ded017c140bfe36b4ba63ed55b8c33217ab6ff8`).
- `cc -O2 -std=c11 /Users/iwasborninbali/projects/science/oeis-A398184/programs/line_rows.c -o /tmp/c7-A398184/line_rows` — exit 0, 0.264 s; output: compiler produced no output [`logs/certificate-2026-11-13/build-line_rows.log`](logs/certificate-2026-11-13/build-line_rows.log) (SHA-256 `4b3de792441decb5951c7297377db5abb73ff678928adf659f7e1f74e2b89d0b`).
- `python3 -B /tmp/c7_compare.py /Users/iwasborninbali/projects/science/oeis-A398184` — exit 0, 0.039 s; output: PASS: maximal-profile file n=8,9,10 matches stored profiles; row totals agree; from pathlib import Path; import sys,json,re; r=Path(sys.argv[1]); s=r.name; load=lambda p:json.loads((r/p).read_text()); a=load('programs/reference/n9.json'); b=load('programs [`logs/certificate-2026-11-13/data-compare.log`](logs/certificate-2026-11-13/data-compare.log) (SHA-256 `4dc22bbc3b4e54e7bf76fda53c67261c026620bc0b51ab069d87a2b4ddd5edc5`).
- `/tmp/c7-A398184/determinant_check 5 0 1 2` — exit 0, 0.461 s; output: total 109536, maximal 5646; matching size profiles. [`logs/certificate-2026-11-13/n5-determinant_check.log`](logs/certificate-2026-11-13/n5-determinant_check.log) (SHA-256 `2e16ddb6402128e4d12aca8997e8a31c3f1112bb2b2f4f06c94e4f9ff7bc5fb2`).
- `/tmp/c7-A398184/line_rows 5 --shard 0 --shards 1 --split-rows 2` — exit 0, 0.638 s; output: total 109536, maximal 5646; matching size profiles. [`logs/certificate-2026-11-13/n5-line_rows.log`](logs/certificate-2026-11-13/n5-line_rows.log) (SHA-256 `0e4433fd83e3c7aeb770efddd28f4ad7f02bca101449da49eee1729aa46be869`).
- `python3 -I /Users/iwasborninbali/projects/science/oeis-A398184/programs/collect.py /tmp/c7-A398184/run-n10 --require-complete` — exit 0, 0.431 s; output: 512/512 shards per program; totals 7287023194031 and 56412888628; matching profiles. [`logs/certificate-2026-11-13/receipts.log`](logs/certificate-2026-11-13/receipts.log) (SHA-256 `4ace589b0d99cb8698f67d9fec67b205f46dd5a2e05f06050986fe19a1d0dee6`).

The archived shards were safely extracted to `/tmp/c7-A398184` after checking paths and sizes. The collector operates on those existing results, not a fresh enumeration. Full n=10 reruns were omitted: README reports about 104 core-hours for both programs; stored n=9 reference runs report about 2635 and 4836 seconds.

## Not covered

The full n=9 and n=10 computations were not rerun; the n=9 results are stored reports and n=10 receipts do not prove execution correctness. This replay compared n=8..10 cells with stored profiles, but did not independently recount every cell in n=1..10. The full independence of the generation and aggregation pipeline remains to be reviewed.

## Guide's independent check

pending

## Verdict

partial — The evidence and replay leave the gaps above, and the Guide's independent check is pending.
