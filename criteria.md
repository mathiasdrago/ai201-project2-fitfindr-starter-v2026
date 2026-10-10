# Acceptance criteria — FitFindr

Five criteria that say what "working" means for this agent, written in unit 3
**before** any results existed.

An acceptance criterion names a target: a number, a count, a rate, or something
a person could plainly observe. *"The agent handles errors"* is an opinion.
*"When search returns nothing, the agent stops before calling the second tool,
in 5 of 5 tries"* is a criterion.

Under each one, write a sentence or two on **why that target** and not a
stricter one. A reason that says something about your tools, your loop, or the
data earns credit; *"80% seemed reasonable"* does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

**Two are written for you. You write three.**

---

## 1. A matching query completes all three tools

Given a query that matches at least one listing, the agent completes all three
tool calls and returns a fit card — in at least 4 of 5 tries.

**Why this target:** 4 of 5 allows for the fact that my search uses keyword matching, and some phrasings may not match even when a relevant item exists. A stricter 5 of 5 would require a more sophisticated search than I'm implementing.

---

## 2. An impossible query stops before the second tool

Given a query that matches no listings, the agent stops before calling
`suggest_outfit` and returns a message naming what to change — 5 of 5 tries.

**Why this target:** 5 of 5 is reasonable here because detecting "no results" is deterministic — if the search returns an empty list, the branch condition is clear. Unlike the happy path where search quality affects results, the empty case is a binary check that should work every time.

---

## 3. Session state carries the item correctly

In 5 of 5 successful runs, the item title and price in the fit card match the first item returned by search_listings.

**Why this target:** This verifies that the item found by search flows through the session to the later tools without being overwritten or corrupted. A mismatch would indicate the session state isn't being preserved correctly between tool calls.



---

## 4. Fit card mentions required elements

In 5 of 5 successful runs, the fit card mentions the item price and platform at least once each.

**Why this target:** The fit card should be a practical caption for a social post. Missing price or platform makes it incomplete for a thrifting context. Since the model output varies, this is a structural requirement that should be met consistently regardless of wording.



---

## 5. Search respects price ceiling

When a query includes a price ceiling (e.g., "under $30"), all returned items are at or below that price in 5 of 5 tries.

**Why this target:** The price filter is a core feature of search_listings. If it doesn't work, users will see items they can't afford. This is a deterministic check on the filtering logic, not dependent on model output.



---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 4 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath it, like this:

         ## 4. Something about the fit card

         The fit card is different every time.

         **Why this target:** ...

         > **Revised in unit 4:** For 5 different items, the 5 fit cards share
         > no opening sentence.
         >
         > **Why revised:** "different" wasn't checkable — two cards that
         > differed by one word still counted. The new version is something I
         > can actually score.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "I said the empty search stops it 5 of 5 times, but I got 3 of 5,
            so 3 of 5 is more realistic."

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.
     ───────────────────────────────────────────────────────────────────────── -->
