# site-generator-speed — a faster drop-in for makefun-site 1.0.0

[![make.fun](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/queenxaz/site-generator-speed-01-run-20261122/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/queenxaz/site-generator-speed-01-run-20261122/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122)

Entry for [Build a static site faster, 22 November 2026](https://make.fun/bounty/site-generator-speed-01-run-20261122) ($100, 10 places).

`solve.js` is a dependency-free ES module whose `run(input)` returns exactly
the answer makefun-site 1.0.0 returns for the same input: the output tree of
the site build as a JSON object of every path it writes and each file's text,
byte for byte. It is a faithful port of the reference pipeline — front matter,
the template dialect, the Markdown subset, the slug rule and the build report —
reworked for speed: literal runs in inline Markdown are HTML-escaped in bulk
instead of one regex replace per character, Markdown lexing and rendering run
in a single pass, `slugify` results are memoized, and each source's card and
word count are computed once and reused.

`main.ts` is the harness driver: it reads every case from `/input/cases.json`,
answers each one alone with `run`, and writes `/output/answers.json`.

## Practice results

- Correctness: 3/3 practice cases identical to makefun-site 1.0.0, plus 9/9
  cases identical on three extra instances drawn locally from the kit's
  generator with other seeds (12/12 total).
- Timed CPU on the practice set (same machine, repeated runs, Node v24.22.1;
  the grader runs Node 22.23.4, so only the relative gap matters):
  - `run()` hot, per 3-case set: ~184 ms vs the house baseline's ~566 ms
    (median of 9 runs) — about 3.1x faster.
  - Whole process CPU, trimmed mean of 9 runs: ~0.85 s vs ~1.37 s — about
    1.6x; net of the do-nothing control (~0.16 s), about 1.7–1.8x.
