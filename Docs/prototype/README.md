# Website mock-up

A clickable visual aid for planning discussions. **Not a real website** — there is no server,
no database and no authentication behind any of it, and every name, date and figure in it is
invented.

## Opening it

Download or clone the repository and open `index.html` in any browser. There is nothing to
install and no build step; it is a single self-contained file.

It works offline apart from the web fonts, which fall back gracefully if you have no connection.

## What it shows

Fifteen pages implementing the structure agreed in
[`Docs/src/Website_draft_2025.png`](../src/Website_draft_2025.png), grouped as the navigation
would be:

- **Public pages** — Home, News
- **The association** — About & committees, Calendar, Newsletter & archive
- **Professional development** — Networking database, Mentorship, Career development database, Job board
- **Community** — Podcast, Book club, Resources, Blog
- **For the planning group** — Site map & ownership, Open questions

The last two are not pages of the real site. They exist so the structure and the outstanding
decisions can be discussed in the same place as the design.

## The three controls in the header

**Planning notes** *(on by default)* — toggles the amber callouts. These carry the unresolved
questions from the 2024 workshop and the structure diagram: whether to host or embed the
podcast, calendar versus yearplan, where the newsletter archive lives, who writes the blog.
Turn them **off** to see the site as a member would see it, and on to run a planning discussion.

**Sign in** — simulates the members' gate. Pages marked with a padlock show a lock screen until
you sign in. The sign-in offers three methods side by side — Google account, member account,
one shared site password — because that choice is genuinely still open. All three behave
identically here; the comparison of what they actually cost and risk is in
[`Docs/hosting-and-security-options.md`](../hosting-and-security-options.md).

**◐** — switches light and dark.

## What it deliberately leaves out

- **Donate.** Sketched with a question mark in the structure diagram, so it is absent here
  rather than implied.
- **Member profiles.** A nice-to-have from the Professional Development Committee, dependent on
  per-person consent. Noted on the Networking page, not built.
- **Phase 2 items are present but flagged** with a `P2` marker: Job board, Blog and public News
  were all identified as post-launch.

## Using it in a meeting

1. Start with **Planning notes off** and walk the navigation. The question to ask is whether the
   grouping makes sense and whether anything is missing.
2. Turn **Planning notes on** and revisit the pages where a decision is outstanding.
3. Finish on **Open questions**, which lists the decisions blocking a launch.

## Open decisions that would change this mock-up

Kept in one place, in
[§9 of the hosting and security document](../hosting-and-security-options.md#9-decisions-needed-to-proceed).
The *Open questions* page repeats that list for use in the room. If a decision is made, update
the document first, then this mock-up.
