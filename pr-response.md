# PR Response Doc — CineLog Watchlist Feature

## AI Usage
<!-- Fill in at the end — how you used AI tools during this project -->

## Comment 1 — Rename
**What I did:**
Services/watchliat_service.py contained a function: save_to_watchlist.py.
Function names should follow the project's naming convention - The pattern here is verb_to_noun.
Renames the function to Add_to_watchlist() and updated all call sites following this convention.
**How I verified:**
Used editor's find-all references to find the function def and call sites ,then updated and verified the changes.

## Comment 2 — Deduplication
**What I did:**
Following the deduplication pattern from services/collection_service.py i updated the add_to_watchlist() function to contain a deduplication feature preventing duplicate entries.
**How I verified:**
add_to_watchlist() now checks for an existing WatchlistEntry with the same user_id/film_id before inserting, raising AlreadyInWatchlistError if found — mirroring add_to_collection()'s pattern. Verified via pytest tests/test_watchlist.py::test_add_to_watchlist_duplicate_raises, which passed, confirming the second add raises the error and only one row exists
## Comment 3 — Missing test
**What I did:**
Followed the pattern existing in tests/test_collection.py , create a test_watchlist.py for watchlist service testing:
test_add_to_watchlist_creates_entry()
test_add_to_watchlist_duplicate_raises()
test_add_to_watchlist_nonexistent_film_raises()

**How I verified:**
Ran pytest tests/test_watchlist.py -v — all three tests passed (create entry, duplicate raises, nonexistent film raises). Note: at the time of this test run, Film.id was still an integer (pre-rebase), so the nonexistent-film test passed because SQLite's weak typing didn't match the UUID-format fake ID against an integer column — not yet a true UUID-lookup test. This will be re-verified for the correct reason after rebasing onto main
## Comment 4 — Default visibility
**My position:**
**Reasoning:**
**Tradeoff acknowledged:**

## Comment 5 — Sort order
**My position:**
**Reasoning:**
**Engagement with reviewer's point:**

## Comment 6 — Rebase
**What conflicted:**
**How I resolved it:**
**How I verified no conflict remains:**

## PR Description
<!-- Written at the end — feature overview, design decisions, manual testing steps -->