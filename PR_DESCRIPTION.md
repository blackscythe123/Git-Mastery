# Fix: UI inconsistencies, logic bugs, accessibility and failing tests

Hi, first time contributing here. I have been using GitMastery since late 2025 and it genuinely helped me get comfortable with Git. Been meaning to contribute for a while and finally got the time this week.

I went through the codebase and fixed a few things I noticed while using the app and reading the source.

## Changes

**Bug fixes**
- Mobile nav link pointed to `/level` which does not exist, changed to `/`
- `getNextDifficulty()` was called twice in the render and could produce "Advance to null Difficulty" text when it returned null
- Unknown stage IDs passed the `indexOf` check and got incorrectly unlocked
- Buying Double XP repeatedly extended the timer forever, now it only activates if not already active
- Passing a negative amount to `spendPoints` would add coins instead of rejecting

**UI and i18n**
- Seven stages had no icon and fell back to the generic one. Added fitting icons for Reset, Stash, Workflow, Teamwork, Advanced, Archaeology and Mastery
- "Mini Games" and "Git Mini Games" were used inconsistently across translation files, standardized to one
- DifficultySelector had hardcoded English strings even though translation keys for them already existed in common.ts
- Difficulty name rendered lowercase mid-sentence, capitalized the first letter
- Debug functions were always included in the React context value, now only in development builds

**Accessibility**
- Icon-only buttons in the file tree had a title prop but no aria-label

**Tests**
- `git add .` was skipping committed files even when their content had changed on disk, fixed by comparing against the committed snapshot
- Push tests were missing a remote in the setup so every push returned an error
- Stash tests were writing to the filesystem without updating git status so stash found nothing to save
- Stash pop test was checking `output[0]` for "Dropped refs/stash" but that line is always last

All 489 tests pass and the build is clean.

Thanks for building this, it is a great project.
