# US case law: the United States Tax Court

Part of [lexifina/global-law](https://github.com/lexifina/global-law), one git history for every country's law: this is
the case law of the United States Tax Court, which global-law reads at `united-states/tax-court/caselaw/`.

The Tax Court's opinions from its own case system, DAWSON, as a git history: one file per decision, one commit per
decision, dated the day it was filed. 13,888 decisions from 1986-06-26: 340 T.C. opinions, 8,899 memorandum opinions (T.C. Memo.), 2,788 summary opinions, 1,861 bench opinions.

T.C. opinions printed in volumes 1 to 144 of the Tax Court Reports (to 2015), and the Board of Tax Appeals, are in
[lexifina/united-states-federal-special-caselaw](https://github.com/lexifina/united-states-federal-special-caselaw)
(from the Caselaw Access Project) and are not repeated here. This repository holds what that one lacks: T.C. opinions
from volume 145, every memorandum opinion, summary opinion and bench opinion DAWSON holds.

## Questions as git commands

| Question | Command |
|---|---|
| A decision by its citation or docket | `grep -P '^T.C. Memo. 2020-20\t' decision-index.tsv` then `cat <path>` |
| Decisions filed in a window | read the `In-force:` trailer: `git log --format='%(trailers:key=In-force,valueonly,separator=) %an'` |
| Decisions citing 26 U.S.C. § 6662 | `cat judgments/united-states/federal/usc/title-26/6662.jsonl` |
| The section as the court applied it | each overlay row's `law_commit` is the section's own version in the US Code record on the day filed |

## What each kind is

- **T.C. opinions** (`reporter: tc`): reported opinions of the Court, cited by their slip number ("160 T.C. No. 1")
  until a volume is printed. Precedential.
- **Memorandum opinions** (`tc-memo`, "T.C. Memo. 2020-20"): the Court treats them as nonprecedential.
- **Summary opinions** (`tc-summary`): small tax cases; under 26 U.S.C. §7463(b) a decision "shall not be treated as a
  precedent for any other case".
- **Bench opinions** (`tc-bench`): stated orally at trial and served as a transcript with an order (Tax Court Rule 152).

Each file's `precedential_status` and `precedential_note` say which. The same opinion filed in several consolidated
dockets is one decision here, listing every docket.

## Dates and authors

The commit date is the day DAWSON gives as the opinion's filing date, at noon US Eastern (`In-force:` and `Decided:`).
The author is the court and the citation (or docket), at an address that cannot exist. These are court rulings, not
laws: every commit is `Kind: court`.

## Source

The United States Tax Court's case system, DAWSON (`https://dawson.ustaxcourt.gov`): the opinion search of its public
API for the list, and each opinion's PDF through its public download link. Text is the PDF's own text layer, unchanged
except for whitespace. Opinions of the Court are works of the US Government and in the public domain (17 U.S.C. §105).

## What it does not show

Orders other than bench opinions, decisions entered, briefs and other filings; opinions DAWSON does not hold (most
memorandum opinions before the mid-1990s); statute citations to US Code titles the record does not hold.
