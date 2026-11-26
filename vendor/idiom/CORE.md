# Core rules (Adam McCarthy)

Import this from a project `CLAUDE.md`. Short on purpose; detail lives in Idiom `house/` and SubScout's style guide. Every item is tagged
**[Law]**, **[Default]**, **[Knowledge]** or **[Preference]** (`house/tiers.md`). Law is never bent; a Default is bent only by a declared
exception. Precedence among rules: Law, then Defaults in this file, then `house/`, then the style guide, then the repo's own
`CLAUDE.md`.

## Language
- **[Law]** British English (colour, licence noun, visualise, metre, analyse). Sentence-case headings.
- **[Law]** Impersonal voice for published work and documentation: no "we" or "I". No summary wrap-up: end on the last point.
- **[Default]** Plain words. Say what happened and why; mechanism first.
- **[Default]** Vary structure: one catchy headline, plain varied headings after it; do not give every section the same shape.
- **[Law]** No barred words or terms (`house/terms.md` and the private word list); prose is run through the checkers before it is shown.
- **[Default]** Written for executive leadership and technically trained colleagues (engineering, science): precise and measured, not academic.

## Units and numbers
- **[Default]** Metric first (Sm³, km, °C), boe alongside or by toggle. 1 Sm³ o.e. = 6.29 boe (Sodir convention); state it.
- **[Default]** 12,345.6; true minus (−); dates 20 March 2026 in prose, 2026-03-20 in data.
- **[Default]** No more decimals than the data supports. Every number in prose traces to data and is tested.

## Confidence
- **[Law]** (truth gate) Observed (measured or published, cited) / Derived (our calculation, method stated) / Interpreted (model or
  judgement; give range or assumption). Never hide uncertainty. Every figure: title, units, source with date,
  confidence.
- **[Default]** Rigour on the test, optimism on the supply. A page says exactly what failed and by how much, then gives the next
  idea or step. A dropped option is followed by the one taken, never by a lesson about caution. A failed test is the method
  working, not a reason to soften the next claim or the next attempt.

## Reuse and licence
- **[Default]** Reuse before you build: the maintainer keeps a directory of existing repos and what each is for (Idiom `DIRECTORY.md`). Style
  comes from SubScout, map bases from Relief, facts and the knowledge store from the data engine. Say so when none fits.
- **[Law]** Datasets: look up terms and the attribution line in Idiom `DATASETS.md`, show the line wherever the data are used, and never write a licence from memory.
- **[Law]** Every repo, public or private, carries a licence from the day it is created (`house/licence.md`): the MIT License with
  Acknowledgement for code, Creative Commons Attribution 4.0 where the repo is not just code. Anything built with the work says so,
  visibly, and never implies endorsement. Third-party data and vendored code keep their own terms. The one exception is Idiom itself: all rights reserved, no licence granted.
- **[Law]** A public repo's README opens with a badge row (workflow status, Python version, licence) under the title.
- **[Default]** Before pushing a new or changed repo, run Idiom's `scripts/check_repo.py PATH`: it applies the audit's CLAUDE.md, LICENSE and README licence checks to the local folder.

- **[Default]** Pictures on cards and tiles that have none of their own are open-licence geology photographs, credited and detuned
  into the fjord scale (`house/imagery.md`), never a generated placeholder.

## Working rules
- **[Preference]** Act on the plan; stop at agreed gates and report outcomes plainly, including failures and skipped steps.
- **[Law]** Never make anything public, delete data, force-push or commit someone's uncommitted work unasked.
- **[Default]** Never run long or costly data fetches unasked.
- **[Law]** Data ingestion re-runs only when its input has changed. Every new ingestion or processing step records what it read
  (a content hash, or ETag, size and time, or a fingerprint of path, size and modified time) together with its settings and code
  version. Before it runs again it checks that record and stops with "unchanged" when nothing differs and its outputs exist. A
  `--force` option overrides the check, and a dry run says whether it would run. The step's tests show that a second run on the
  same input writes nothing. Existing patterns to copy are listed in the maintainer's Copilot instructions.
- **[Default]** No source reaches an output except through a port: every golden table, open or classified, is declared as a port in
  the data contract with its tier, unit, confidence, key, grain and golden-key foreign key, and is read through the data-access layer.
  A source is ingested only with a classification row, an adapter and gate with an unchanged second run, a golden target, a port and
  a clean `kdc gate`. No data from the USA is ingested from internal or restricted sources (owner rule, 2026-11-23). Checklist:
  the ingestion documents of the data contract and of the data engine.
- **[Law]** Synthetic and test outputs of the internal and restricted tiers are designed and built on top of the contract on the
  open-data computer, even where a document or a role states a restriction on the tier (owner's ruling, 2026-11-25). They use the
  contract's names, types and port metadata only: no real classified row, value, count, path or source file is read or copied, and
  a synthetic root is marked `SYNTHETIC.json` (`"synthetic": true`), kept apart from the open roots and labelled with the tier it
  imitates.
- **[Preference]** `gh repo create` may be blocked by the auto-mode classifier: prepare everything locally and hand over the
  exact commands.
- **[Default]** Pin dependencies between repos by tag; dependencies run one way only. Keep heavy ingestion out of the
  framework repos.
- **[Default]** Test the numbers you quote. Look at the rendered output before calling visual work done.
