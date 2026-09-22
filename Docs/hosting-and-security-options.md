# Hosting and security options

Prepared September 2026 for the Communications Committee and the Board.

This document sets out realistic options for hosting the DRMCCAA website and protecting
its members-only content, with indicative costs, pros, cons and risks for each.

Prices are indicative, in USD, checked September 2026, and change often — confirm current
pricing before committing. Sources are listed at the end.

---

## 1. Separate the two decisions

The discussion so far has treated "the website" as one choice. It is two, and they can be
answered independently:

```mermaid
graph LR
    A[Website] --> B[Hosting<br/>where the pages live<br/>and who edits them]
    A --> C[Identity<br/>who can sign in<br/>and who they are]

    classDef main fill:#00008b,stroke:#000000,stroke-width:2px,color:#fff
    classDef sub fill:#b0c4de,stroke:#6495ed,color:#1b4332

    class A main
    class B,C sub
```

Some platforms bundle both (Google Sites, Wix, Wild Apricot). Others let you pick them
separately (a static site behind Cloudflare Access). Bundled is simpler to run; separate is
cheaper and more flexible but means two things to administer.

## 2. What the committees have already asked for

These come from the April 2024 workshop and the committee responses. They rule some options
out before cost is even considered.

| # | Requirement | Where it came from | Consequence |
|---|---|---|---|
| R1 | The site must know **who** is signed in | Members update their own networking-survey entry | Rules out a single shared password |
| R2 | **No second password** for the networking data | Professional Development Committee | Identity must be reusable across embedded tools, or the tools must move behind the same gate |
| R3 | Committees edit **their own** pages | Responsibilities model | Needs a visual editor and per-committee permissions, not a code deploy |
| R4 | Volunteer-maintainable | Maintenance is a stated top-three issue | Favours platforms over anything self-hosted |
| R5 | Little or no recurring cost | Funding is unresolved | Favours free tiers and nonprofit programmes |
| R6 | Must embed Google Calendar, Looker Studio, Google Forms, SoundCloud | Multiple committees | All mainstream options handle this; note the caveat in §4 |
| R7 | Members are international, many in the EU | Alumni network | GDPR applies to the networking survey data |

**R1 is the decisive one.** It is worth being explicit about this, because "password-protect
the whole site" is the cheapest and most tempting option and it cannot satisfy R1 or R2.

---

## 3. The options

### Option A — Google Sites on Google Workspace for Nonprofits

The current test site, formalised.

**How it works.** Google Sites hosts the pages. Access is restricted to named Google accounts
or a Google Group. Members sign in with their own Google account. Editing is drag-and-drop,
and edit rights can be granted per page section to different committees.

**Cost.** Free, if the association is validated as a nonprofit. Google Workspace for Nonprofits
is free for verified 501(c)(3) organisations *or their country equivalents*, validated through
Goodstack (2–14 business days), up to 2,000 users. Without nonprofit status: Business Starter
at standard rates, or run it on a personal Google account with a Group as the allowlist, which
is free but gives you no custom domain mail and no admin console.

**Pros**
- Zero cost and zero hosting to run.
- Per-person identity out of the box, which satisfies R1.
- Same account signs in to Google Forms, Google Calendar and Looker Studio — this is the
  cleanest answer to R2 anywhere on this list.
- Non-technical committee members can edit directly.
- Revoking one person is one line in a Google Group.

**Cons**
- Members must have a Google account, and must be signed into the right one. In practice the
  most common support complaint on Google Sites is people being signed into a personal account
  when the invitation went to a work address.
- Design is constrained. The site will look like a Google Site.
- No real membership features: no renewals, no member directory, no payments.
- Sharing is per-file. Getting the boundary right between public pages and members-only pages
  takes care, and a mis-set share link is the most likely way this leaks.

**Risks**
- *Nonprofit validation may fail or lapse.* Alumni associations are not automatically eligible,
  and re-validation is periodic. Check eligibility before building on it.
- *Account ownership.* If the Workspace is created under one person's identity, that person
  effectively owns the association's website and mail. Must be an association-owned account
  with at least two super-admins.

---

### Option B — Website builder with a members area (Wix or Squarespace)

**How it works.** A hosted site builder with a built-in member login. Members register or are
invited, get their own account, and specific pages are marked members-only.

**Cost.** Wix paid plans run roughly $17–$159/month billed annually; the members area itself is
included without extra charge unless you need payments or bookings, which push you to Core or
above. Squarespace is comparable, though member areas there have historically been a paid add-on.
Budget **$200–$400/year**.

**Pros**
- Much better looking than Google Sites, with real design control.
- Per-person accounts, satisfying R1.
- Genuinely easy for non-technical editors, and per-page access control is a checkbox.
- One vendor, one bill, one support line.

**Cons**
- Recurring cost with no free tier that includes the members area on a custom domain.
- The Wix member identity is *not* a Google identity, so it does not unlock an embedded Looker
  Studio report or a Google Form. R2 is only half-solved — see §4.
- Content is locked into the platform. Migrating away later means rebuilding.

**Risks**
- *Funding continuity.* A subscription needs someone to keep paying it. A lapsed card takes the
  site down, and volunteer treasurers change.
- *Note on the site-wide password feature.* Wix also offers one password for the whole site.
  That is a different, much weaker mechanism than the members area, and it fails R1. If Wix is
  chosen, it must be the members area, not the site password.

---

### Option C — Static site behind Cloudflare Access

The technical-but-cheap option.

**How it works.** The site is built as static pages (GitHub Pages, Cloudflare Pages or Netlify)
and Cloudflare Access sits in front of it. A visitor hits the site, Cloudflare asks for their
email, sends a one-time PIN, and only lets them through if their address is on the allowlist.
No member accounts, no passwords to manage — just a list of approved email addresses.

**Cost.** Hosting free. Cloudflare Zero Trust is **free up to 50 users**, then $7/user/month.
Domain ~$10–20/year. So **effectively free under 50 members**, and roughly $4,200/year at 50+
users — which is the cliff that matters here, because an alumni association will pass 50.

> Worth checking carefully: the 50-seat limit counts *active authenticating users*, and a large
> alumni association will exceed it. That single fact may disqualify this option, so confirm the
> current limit and the member count before pursuing it.

**Pros**
- Per-person identity via email one-time PIN, with no Google account required and no password
  for anyone to lose. This is the lowest-friction sign-in on the list.
- Free at small scale, and completely under association control.
- Fast, and nothing to patch.
- Access logs show who opened what, which is real accountability for sensitive data.

**Cons**
- **Fails R3 and R4.** Committees cannot edit a static site without a technical workflow. This
  is the option's fatal flaw for a volunteer organisation, unless a CMS is added on top — which
  adds cost and complexity back.
- Needs someone comfortable with DNS and Git. When that person leaves, the site freezes.
- Note that GitHub Pages cannot be made private except on GitHub Enterprise Cloud, so the
  privacy comes entirely from the Cloudflare layer, not the host.

**Risks**
- *Key-person dependency,* the single largest risk in this document for a volunteer body.
- *Cost cliff at 50 users,* as above.

---

### Option D — Association management platform (Wild Apricot and similar)

**How it works.** Purpose-built software for membership organisations: member database, member
accounts, event registration, email, payments and a website, all in one.

**Cost.** Wild Apricot starts around **$63/month** (about $53/month if pre-paid for two years) for
100 contacts, rising to roughly **$140/month at 500 contacts**. Budget **$750–$1,700/year**
depending on membership size.

**Pros**
- Solves problems the other options do not: a real member directory, renewals, event
  registration with capacity limits, and payment collection.
- Per-person accounts with roles, comfortably satisfying R1.
- Members can maintain their own profile — which is close to the "member profiles" nice-to-have
  and overlaps substantially with the networking database.
- Built for exactly this kind of organisation, so the workflows match how a committee thinks.

**Cons**
- By far the most expensive option, and the cost scales with the thing you want to grow.
- Considerable overkill if the association does not collect dues.
- The bundled website builder is the weakest part of most of these products.

**Risks**
- *Cost scaling.* The price rises as membership grows, so success makes it more expensive.
- *Funding.* This option only works if there is a dues or donation model behind it. It makes
  the funding question urgent rather than deferrable.

---

### Option E — Self-hosted WordPress with a membership plugin

**How it works.** Shared hosting, WordPress, and a membership plugin for gated content.

**Cost.** Hosting $5–15/month, membership plugin $150–250/year, domain $15/year. Roughly
**$250–430/year**, plus the unpriced cost of someone's time.

**Pros**
- Maximum flexibility, full data ownership, no platform lock-in.
- Familiar editing interface for many people.
- Fine-grained roles map well onto per-committee editing.

**Cons**
- **You own the security.** WordPress and its plugins need patching, and unpatched membership
  plugins are a well-known route to data exposure. This is an ongoing obligation, not a setup task.
- Needs a genuinely technical volunteer, indefinitely.

**Risks**
- *This is the only option where a lapse in attention becomes a breach rather than just staleness.*
  Given that the site holds personal data on alumni, and that the association's own documents
  list maintenance as an unsolved problem, this combination is hard to recommend.

---

### Option F — Do less, and gate only what actually needs gating

Not a platform. A different scoping of the problem, worth costing because it may beat all of the above.

**How it works.** Make the site public. Put the association overview, committees, contacts,
calendar, podcast, book club and public resources out in the open, where they need no protection
at all. Leave the networking survey data where it already is, behind whatever access control the
Professional Development Committee already uses, and link to it.

**Cost.** Free to ~$200/year depending on host. No identity layer at all.

**Pros**
- Eliminates the hardest problem instead of paying to solve it.
- Removes the biggest GDPR exposure, because the site never holds personal data.
- Doubles as recruitment: prospective members and the wider field can see the association exists.
- Much of the wish list — calendar, podcast, book club, committee info, resources, newsletter
  archive — is not actually confidential.

**Cons**
- Does not satisfy R1 or R2; it sidesteps them. The networking database keeps its separate
  password, which is precisely what the Professional Development Committee asked to be rid of.
- Some members may be uncomfortable with any association material being publicly indexed.

**Risks**
- *Deferral, not resolution.* The identity question returns the moment anyone wants member
  profiles or a job board.
- Content posted publicly is indexed and cached. Assume anything published is permanent.

---

## 4. The embedded-content caveat that affects every option

Several of the wish-list items are embeds: Google Calendar, a Looker Studio report, Google
Forms, SoundCloud. **Putting an embed behind your site's login does not protect the embedded
content.** The embedded service applies its own access rules. Two consequences:

- If a Looker Studio report is shared with "anyone with the link", the link works whether or not
  the person got it from behind your login. The site's gate is decorative in that case.
- Conversely, if the report is restricted to named Google accounts, members will be prompted to
  sign in to Google *again* — which is exactly the second password the committee objected to.

This is why **Option A is unusually strong on R2**: when the site identity and the embedded-tool
identity are the same Google account, the problem disappears. With any non-Google platform, the
realistic answer is either to accept a second sign-in for the sensitive report, or to migrate
that data into the platform itself.

## 5. Scenario: one shared password plus external forms

This came up in discussion and is the most likely proposal to be raised at the meeting, so it
is worth costing properly rather than dismissing.

**The proposal.** Protect the whole site with a single shared password. Members have no
accounts. Anyone who needs to update their networking-survey information does it through a
form, which a committee member reviews and applies.

### What it genuinely fixes

R1 — the site must know who is signed in — exists *only* because members need to edit their own
entry. Move that to a form and the requirement disappears. The site no longer needs to know who
anyone is.

This is a real simplification, not a dodge. It also matches how the association already works:
the April 2024 notes describe committees sending content to Communications to publish.

Two caveats on the form half:

- **An open form cannot tell who is submitting.** Anyone with the password could submit an
  update in someone else's name, or add a fabricated entry. Low likelihood in a trusted
  community, but it means every submission needs human review before it goes live — and that
  work lands on the Professional Development Committee.
- **Requiring a Google sign-in on the form** fixes that, and is free. But it reintroduces
  per-person identity at the form rather than at the site. That is a perfectly reasonable
  answer; just note that identity has been moved, not avoided.

### What the shared password costs you

It is easier to set up and to explain. It is not more secure. Its real failure mode is not
attackers, it is **drift**: the password ends up in the alumni WhatsApp group, gets forwarded to
a friend doing research, sits in an email chain from two years ago. There is no breach event,
just gradual loss of meaning. Concretely:

- You cannot revoke one person's access without changing it for everyone.
- You cannot tell who accessed what, so you cannot demonstrate anything after the fact.
- Rotation means emailing the whole membership, which in practice means it never happens.

Set against that, it does buy the main thing "not public" means to most associations: the site
stops being indexed by search engines and stops being casually discoverable. That is worth
something, and it is worth being clear that it is the thing you are actually buying.

### It works or fails on one question: what sits behind it

| Fine behind a shared password | Not fine behind a shared password |
|---|---|
| Calendar, podcast, book club, newsletter archive, committee internals, resources, blog | The networking database and any alumni contact details |

The left column is *"don't index this publicly"* rather than *"this is confidential"*. A shared
password is a proportionate control for it.

Putting the networking data behind the same password **widens** access to personal data, from
"people who were sent the survey password once" to "anyone who has ever held the site password".
That is weaker than the status quo, and hard to defend under GDPR because you cannot show who
had access.

So the workable version still has two passwords — but only one of them is used regularly, and
the rarely-used one guards the only genuinely sensitive thing. The Professional Development
Committee's request (R2) is not met; it is consciously traded away.

### The consequence that changes the platform choice

**Google Sites has no shared-password mode.** Its access control is Google accounts and Groups,
or fully public. There is no middle setting.

Choosing "one password for the whole site" therefore rules out the free option in §3A and points
at **Wix (~$200–400/year)**, which does have a site-wide password. That is the hidden cost of
this route: not the security posture, the platform bill.

### A middle option with the same benefit

If the real goal is *less administration* rather than a password specifically, there is a better
version of the same instinct: **an email one-time PIN, or a Google Group allowlist**. Members
receive a code or use the account they already have. Nothing to remember, nothing to leak,
revocable per person, and no member-account administration to run.

Counter-intuitively, **a Google Group allowlist is easier to run than a shared password over
time.** You never rotate it, members never forget it, and adding or removing someone is one
line. The "shared password is simpler" intuition holds for the first week and not for the next
five years.

### Verdict

Defensible, on two conditions: the networking data stays out from behind it, and the association
accepts paying for Wix. If either condition fails, this route is worse than Option A on both
cost and security.

## 6. Risks that apply whatever you choose

| Risk | Why it matters here | Mitigation |
|---|---|---|
| **Key-person dependency** | Domain, hosting account and billing often sit with one volunteer. Their departure can lose the site entirely. | Association-owned accounts, a shared password manager, two admins minimum, and the domain registered to the association. Do this on day one; retrofitting it is painful. |
| **Content staleness** | Already identified as a top-three issue. A stale site is worse than none. | Launch small. Prefer linking and embedding over rebuilding. Name individuals, not committees, as owners. |
| **GDPR / personal data** | The networking survey holds contact details for EU-resident alumni. | Collect the minimum, state a purpose, get explicit consent for anything shown to other members, and have a route to delete on request. Keep the survey data in one place, not copied across tools. |
| **The allowlist only ever grows** | Nobody resigns from an alumni association, so the approved list is never pruned and slowly diverges from reality. | Decide in advance what removes someone, and review the list annually. |
| **Funding lapse** | Any paid option dies quietly when a card expires. | Annual pre-payment from association funds, on an association payment method, not a personal card. |
| **Over-scoping** | The wish list is roughly 15 pages. Each one is a maintenance commitment. | Treat the phase-2 flags as binding. |

## 7. Comparison

| | A. Google Sites | B. Wix / Squarespace | C. Static + Cloudflare | D. Wild Apricot | E. WordPress | F. Public only | G. Shared password + forms (§5) |
|---|---|---|---|---|---|---|---|
| **Cost/year** | $0 | $200–400 | $0 (<50 users) | $750–1,700 | $250–430 + time | $0–200 | $200–400 (needs Wix) |
| **Per-person identity (R1)** | Yes | Yes | Yes | Yes | Yes | No | No — moved to the form |
| **Solves the second password (R2)** | Yes | Partly | No | Partly | Partly | No | No — traded away |
| **Committees self-edit (R3)** | Yes | Yes | No | Yes | Yes | Depends | Yes |
| **Volunteer-maintainable (R4)** | High | High | Low | High | Low | High | Medium — manual update loop |
| **Design quality** | Low | High | High | Medium | High | Varies | High |
| **Security burden on us** | Minimal | Minimal | Low | Minimal | **High** | None | Low, but password drift is permanent |
| **Main risk** | Nonprofit eligibility | Funding continuity | 50-user cliff, key person | Cost scaling | Patching lapse | Defers the problem | Sensitive data ending up behind the shared password |

## 8. Recommendation

**Confirm nonprofit eligibility, then run with Option A, scoped like Option F.**

The reasoning:

1. Option A is the only one that genuinely solves the second-password problem, because the site
   identity and the Google tooling identity are the same thing. That was the Professional
   Development Committee's clearest and most specific request.
2. It costs nothing, which means the unresolved funding question stops blocking the launch.
3. A test site already exists on it, so the committee can evaluate the real thing rather than a
   proposal.
4. Its weakness is design quality, which is the least costly weakness to live with and the
   easiest to revisit later.

Scope it like Option F: put everything non-confidential on the public side and keep the gated
area small. That reduces the number of pages needing maintenance, lowers the GDPR surface, and
makes the association visible to people who might want to join it.

**If nonprofit validation fails,** the choice is between Option B and Option F. Option B buys a
better-looking site and per-person accounts for a few hundred dollars a year, at the price of
accepting a second sign-in for the networking report.

**Option D becomes the right answer** only if the association decides to collect dues or run
paid events. At that point it stops being expensive overhead and starts paying for itself.

**On the shared-password route (§5):** if the appeal is avoiding member-account administration,
note that a Google Group allowlist achieves that *and* costs nothing *and* is less work to
maintain. The shared password is only the simpler option if you also want Wix's design quality,
in which case it is a reasonable package — provided the networking data stays outside it.

## 9. Decisions needed to proceed

1. Is the association a registered nonprofit, or a country equivalent that Goodstack will
   validate? *This single answer eliminates most of the table.*
2. Roughly how many alumni would be given access? Under or over 50 changes Option C entirely,
   and moves Option D between price bands.
3. Is there any budget at all, or must the answer be free?
4. Does the association collect dues today, or plan to?
5. Who will own the domain and the administrator accounts, and who is the second admin?
6. Does the Professional Development Committee accept a second sign-in for the networking
   report if the platform is not Google, or is R2 a hard requirement?
7. If the shared-password route (§5) is preferred, is the association content to keep the
   networking database outside it, and to pay for Wix?

This list is the canonical one. The *Open questions* page in the mock-up repeats it for use in
the room — if a decision is made, update it here first.

---

## Sources

Pricing and platform facts checked September 2026.

- [Cloudflare Zero Trust free plan limits and pricing](https://zerometric.net/research/cloudflare-zero-trust-free-plan-limits-2026/)
- [Cloudflare Access pricing 2026](https://costbench.com/software/ztna/cloudflare-access/)
- [Google Workspace for Nonprofits](https://www.google.com/nonprofits/offerings/workspace/)
- [Google for Nonprofits eligibility and validation, 2026](https://stackforgood.net/guides/google-for-nonprofits/)
- [Wix pricing 2026](https://www.websitebuilderexpert.com/website-builders/wix-pricing/)
- [Wix paid plans and member areas](https://www.zentus.agency/post/wix-paid-plans-and-member-areas)
- [Wild Apricot pricing 2026](https://toolradar.com/tools/wild-apricot-membership/pricing)
- [GitHub Pages site visibility and plans](https://docs.github.com/en/enterprise-cloud@latest/pages/getting-started-with-github-pages/changing-the-visibility-of-your-github-pages-site)
- [Netlify Identity status, February 2026](https://www.netlify.com/blog/auth0-extension-identity-changes/)
