# Git history of the United States Code, 1994-2024: one file per section, one commit per annual edition, sourced from GPO's official editions on govinfo.

Built from the canonical repository (us-code), which holds GPO's annual editions exactly as published.

- One folder per title; inside, folders for parts, chapters and subchapters, numbers padded so they sort
  (`Chapter 085 - District Courts; Jurisdiction`, `Subchapter 002 (II) - Officers`). One file per section, named
  with the section sign and padded number (&sect; 01332 - Diversity of citizenship; ....md). Each folder's `README.md` holds that division's heading and
  analysis (its table of contents) as GPO prints it, then a generated list of links to every part and section in
  the folder.
- One commit per annual edition, dated to GPO's "laws in effect as of" date, tagged `edition-YYYY`. A commit
  touches only the sections whose text changed in that edition, so `git log --follow -- "<section file>"` lists the
  editions in which that section was amended, and `git diff --word-diff edition-2018 edition-2024 -- "<file>"`
  shows what changed. Notes and amendment history stay with their section.
- Printed page numbers: each title folder's `PAGES.md` lists every section and division with the printed pages it
  occupies in that edition. They are not in the section text (pagination shifts every edition and would make every
  section look amended). Every page mark is kept with its exact position in `_page-maps/USCODE-titleN.json`;
  section files plus that map reconstruct the canonical title byte for byte, and the build proves it for every
  title of every edition.
- Folder names use normal capitals (GPO prints division headings in capitals): small words lowercase, acronyms and
  unusual spellings as the Code's own text writes them. The text inside every file is exactly as GPO printed it.
- Commit messages count separately the files whose only change is GPO's note-group headings ("Editorial Notes" /
  "Statutory Notes and Related Subsidiaries"), which GPO introduced to group each section's notes - a change in how
  the notes are arranged, not in the law.
- `GAPS.md` lists title-years govinfo holds no copy of: those titles are left exactly as in their last available
  edition and their changes appear in the next edition govinfo has. A gap in the source is never shown as a repeal.
- A section that moves or is renumbered appears as a removal plus an addition in that edition's commit.


**Unofficial. Not legal advice.** The official text is GPO's (govinfo) and the Office of the Law Revision Counsel's
(uscode.house.gov). See `NOTICE.md`.

## Source and checks

Every edition is GPO's annual edition as served by govinfo (1994-2024). Each title file was checked on arrival
against the SHA-256 digest and size in GPO's provenance record for that package, then converted to Markdown with the
text unchanged; the build proves every title of every edition rebuilds byte for byte from the section files and the
page map.

## Licence

The United States Code text is a work of the United States Government and is not claimed (17 U.S.C. &sect; 105). The
arrangement, names, guides, page tables and gap list are (c) 2026 Joshua Pearlman, CC BY 4.0. **`LICENSE`,
`LICENSES/` and `REUSE.toml`** say what is licensed, on what terms, and which files each statement covers.
**`CITATION.cff`** says how to cite this repository.

## Known source quirks

- **2024 edition, Title 16:** GPO's file for this title marks most page breaks twice (pages 1-2315). The page
  table (`PAGES.md`) and the section text are unaffected. The repeated marks are kept only in
  the page map (`_page-maps/USCODE-title16.json` at `edition-2024`), so the title can still be rebuilt exactly as
  GPO published it.
- Title-years govinfo does not serve are listed in `GAPS.md`.

## Using it

- Some paths are long (the longest is about 500 bytes). On Windows, enable long paths before cloning:
  `git config --global core.longpaths true`.

## Reporting an error

Open an issue at https://github.com/Bespoke-Legal-Intelligence/United-States-Code/issues and include:

- the title and section, and the edition (year);
- the file here (or the commit) where you saw it;
- what govinfo shows for that edition.

If the text here differs from what GPO published, that is an error in this repository and will be corrected.
