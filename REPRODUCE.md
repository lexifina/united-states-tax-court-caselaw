# How this repository was made

Made on 2026-11-09 by Claude Code (Claude Opus 5.5, `claude-opus-5-5`), which wrote the scripts and ran them. No AI model
wrote, edited or summarised any decision text, and none ran while the repository was built.

1. `python fetch.py all` (in Lexifina's tax-court-work folder): the DAWSON public API's opinion search,
   `https://public-api-green.dawson.ustaxcourt.gov/public-api/opinion-search?keyword=&dateRange=customDates&startDate=<MM/DD/YYYY>&endDate=<MM/DD/YYYY>&opinionTypes=<TCOP|MOP|SOP|OST>`,
   month by month from January 1986, then for each opinion
   `/public-api/<docket>/<docketEntryId>/public-document-download-url` and the PDF it points to. One request at a time,
   a second apart, with curl. robots.txt: dawson.ustaxcourt.gov serves none (its app page instead); www.ustaxcourt.gov
   disallows only /admin/.
2. `python extract.py`: one record per opinion document (consolidated dockets merged by citation), text from the PDF's
   text layer with PyMuPDF; T.C. opinions in volumes 1-144 left out (held in united-states/federal-special/caselaw); decisions whose docket and year
   match a Tax Court or B.T.A. decision in united-states/federal-special/caselaw's decision-index.tsv marked as duplicates.
3. `python -X utf8 build_tc.py <out> --today 2026-11-09`: the commits (git fast-import), with the US Code citation reader
   and overlay of Lexifina's scripts/us-caselaw/build_state.py, against a mirror of lexifina/united-states-law.
