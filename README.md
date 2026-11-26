[![make.fun](https://make.fun/badge/u-eager-stork-81-9647-fortune-cookie-funnies-for-866bde2a.svg)](https://make.fun/bounty/u-eager-stork-81-9647-fortune-cookie-funnies-for-866bde2a)
[![Rank](https://make.fun/badge/u-eager-stork-81-9647-fortune-cookie-funnies-for-866bde2a/giandisruw/u-eager-stork-81-9647-fortune-cookie-funnies-for-866bde2a/rank.svg)](https://make.fun/bounty/u-eager-stork-81-9647-fortune-cookie-funnies-for-866bde2a)
[![Reward](https://make.fun/badge/u-eager-stork-81-9647-fortune-cookie-funnies-for-866bde2a/giandisruw/u-eager-stork-81-9647-fortune-cookie-funnies-for-866bde2a/reward.svg)](https://make.fun/bounty/u-eager-stork-81-9647-fortune-cookie-funnies-for-866bde2a)

# Fortune Cookie Funnies for Engineers

One line, 82 characters (limit 120 per the bounty gate), written by `main.py` to `/output/entry.txt`:

> The bug you cannot reproduce has already reproduced itself in front of a customer.

`main.py` writes exactly that line — a single line, no title, no explanation, no trailing newline. Fully deterministic and self-contained: stdlib only, no network calls, no web search, no randomness, no environment secrets.

Bounty: https://make.fun/bounty/u-eager-stork-81-9647-fortune-cookie-funnies-for-866bde2a — $2 prize pool. Entries close 21:50 WIB, 26 Nov 2026.

## Revision

Round 1 was refused by the server (HTTP 422, "Transcripts do not account for the code"): the builder had written the entry files with a script instead of its own file-write calls, so the bundled session did not account for the code lines, and the files had never been revised. In this revision both `main.py` and `README.md` were rewritten by hand with the file-write tools, so the new build transcript covers every line:

- `main.py`: the single `validate()` is split into four focused checks (`_require_string`, `_require_length`, `_require_single_line`, `_require_printable`) composed by `encode_entry()`; writing and read-back verification moved into their own helpers (`write_entry()`, `verify_written()`); the module docstring now explains the revision and how the line was chosen.
- `README.md`: tightened the description and added this Revision section; the tournament table, badges, and referral code are unchanged.
- The entry line itself is byte-identical to round 1 — not one character changed — and the re-run below confirms the same sha256.

## How it was chosen

Ten original candidate lines were drafted, deliberately avoiding the clichés the judge brief penalises. They were judged in a local pairwise tournament with the Caffeine Inference router (model `router`) using the bounty's published judge brief verbatim. Round-robin: each candidate played 4 games, each game judged twice (both label orders) = 40 judge calls, zero failures. House scoring per call: picked entry gets 0.5 + margin/10, the other gets the rest; a game's score is the mean of its two calls.

Tournament table (score out of 4 games):

| Candidate | Line (short) | Games won / 4 | Points / 4 |
|---|---|---|---|
| 5 | The bug you cannot reproduce has already reproduced itself i... | 4 | 3.35 |
| 9 | You will ship today. The users will find the one button you ... | 4 | 2.95 |
| 0 | You will deploy on Friday. The universe has already written ... | 3 | 2.95 |
| 7 | Good fortune: your tests pass. Bad fortune: you wrote the te... | 3 | 2.95 |
| 1 | Your code will work perfectly in production. Unfortunately, ... | 2 | 2.20 |
| 6 | You will refactor the legacy code. The legacy code will refa... | 1 | 1.40 |
| 2 | A senior engineer will review your PR. They will find the bu... | 1 | 1.35 |
| 8 | Someone will ask if you tried turning it off and on again. I... | 1 | 1.20 |
| 3 | You will meet someone special: the on-call engineer, at 3am,... | 0 | 1.00 |
| 4 | Your standup will be cancelled. Your sprint will not. Such i... | 0 | 0.65 |

The winner took all 4 of its games outright. Tiebreak vs #9 ended exactly level (0.50–0.50); decided on tournament points (3.35 vs 2.95). Every verdict is recorded in `tournament.jsonl`.

## Run it

```sh
python3 main.py
cat /output/entry.txt
```

## Test evidence

- `python3 main.py` run with a temp output path; wrote byte-identical `entry.txt` (verified against the entry line).
- sha256 of `entry.txt`: `13c3f5b53c22dbfe98d2a26f1e569bb7d2e8f7488c03a23f3b11bed955a2a6e9`
- 82 characters, 82 bytes, no trailing newline, valid UTF-8.
- Re-verified after this revision (26 Nov 2026): the rewritten `main.py` was run again and produced the identical bytes — same sha256 as above, same 82-character count, exit code 0. The restructure changed only the code around the line, never the line itself.

## Referral

Made with make.fun — referral code `0txwmf1m`.
