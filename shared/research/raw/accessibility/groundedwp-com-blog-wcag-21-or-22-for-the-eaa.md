<!--
URL: https://groundedwp.com/blog/wcag-21-or-22-for-the-eaa/
Fetch date: 2026-08-18
Source type: vendor blog
Research cluster: accessibility
Archived by: forge stage 2 sweep (mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc. build sequence step 6.
-->

# WCAG 2.1 or 2.2 for the European Accessibility Act? The directive names neither. — Grounded
URL: https://groundedwp.com/blog/wcag-21-or-22-for-the-eaa/
Published: 2026-08-08

WCAG 2.1 or 2.2 for the European Accessibility Act? The directive names neither. — Grounded

# WCAG 2.1 or 2.2 for the European Accessibility Act? The directive names neither.

 August 8, 2026 

Search for what the European Accessibility Act requires and you will be told, confidently and in a lot of places, that it requires WCAG 2.1 Level AA. Some pages say 2.2. A few say "2.1, moving to 2.2".

Open Directive (EU) 2019/882 and search it for the string "WCAG".

It is not there. The directive never names the Web Content Accessibility Guidelines, and it never names a version of them.

This is not a technicality, and getting it right changes what you write in your own accessibility information.

## What the directive actually requires

The binding obligation is Annex I: functional accessibility requirements, expressed as outcomes rather than as a checklist. Information must be perceivable through more than one sensory channel, understandable, presented in ways users can perceive; functionality must be operable; and so on for the specific service categories.

Annex I does not tell you what contrast ratio to hit. That is deliberate — a directive that named a version number would need amending every time the version changed.

## Where a WCAG version does come from

Article 15(1):

> Products and services which are in conformity with harmonised standards or parts thereof the references of which have been published in the Official Journal of the European Union, shall be presumed to be in conformity with the accessibility requirements of this Directive in so far as those standards or parts thereof cover those requirements.

Three conditions, and all three matter.

It must be a harmonised standard, not any standard. Its reference must be published in the Official Journal — not drafted, not approved by a standardisation body, not widely adopted. And the presumption reaches only as far as the standard covers the requirement; it is not a blanket pass.

The relevant standard is EN 301 549, the European ICT accessibility standard. Version V3.2.1 dates from March 2021 and maps its web requirements to WCAG 2.1 Level AA. The revision aligned with WCAG 2.2 is V4.1.1, expected to be cited in the Official Journal around October 2026; a draft, V4.1.0, went out for review in November 2025.

So as things stand while I write this in August 2026, the WCAG version with a route to presumption of conformity is 2.1 AA, and 2.2 is coming.

## Why the bigger number is not automatically the safer claim

The intuition is that claiming WCAG 2.2 AA is a superset, so it must be at least as good. For engineering, broadly yes. For a written legal claim, no, and for two separate reasons.

It is more than the law asks and less than the law recognises. A statement saying "this service conforms to WCAG 2.2 AA" asserts something the directive never required, while not asserting conformity with the instrument that would actually give you the presumption. You have taken on extra exposure and bought no extra protection.

And it is a bigger promise to keep. WCAG 2.2 adds nine success criteria over 2.1, including 2.4.11 Focus Not Obscured (Minimum), 2.5.7 Dragging Movements and 3.3.8 Accessible Authentication (Minimum) at AA. Every one is another thing that can be wrong on your site, in a claim you published, in writing, about yourself. The FTC's action against accessiBe turned on claims of exactly this shape — not on the state of anyone's site, but on what was said about it.

None of which means do not implement 2.2. Implement whatever you can; 3.3.8 in particular is a real improvement for real people. The point is narrower: what you build and what you claim in a formal document are two different decisions, and the second one should be made deliberately rather than by reaching for the larger number.

## The honest gap in this

I can tell you what Article 15 says, that the directive does not name WCAG, and which EN 301 549 version maps to which WCAG version. I could not establish from secondary sources, to my own satisfaction, exactly which references currently stand cited in the Official Journal under Directive (EU) 2019/882 as opposed to under Directive (EU) 2016/2102, the older public sector directive. Sources disagree, and vendor pages state it with a confidence their citations do not support.

That gap is the practical advice. If you are about to publish a document claiming presumption of conformity, the thing to check is not a blog post — mine included. It is the OJ listing for the directive that applies to you, on the day you publish. It takes a few minutes and it is the only source that settles it.

If that sounds like more diligence than a compliance claim should need, that is worth sitting with, because it is an argument for making a narrower claim.

## What I would write instead

Rather than "this service conforms to WCAG 2.2 AA", something that is true and that you can defend:

> We test against WCAG 2.1 Level AA, the level referenced by EN 301 549 V3.2.1. Our most recent audit was on [date]. The following issues are known and outstanding: [list]. If you hit a barrier, contact us at [address] and we will respond within [time].

Dated. Specific. Contains known failures, which paradoxically makes it more credible rather than less, and makes it very hard to characterise as deceptive. And it says how to reach a human, which is the most useful line on the page and the one that vendors' templates most often leave out.

## The caveats

I am not a lawyer. I am a developer who reads the primary texts because a marketplace reviewer once proved to me that I had built the wrong document entirely, and I have not trusted a summary since.

Also: check whether you owe any of this. Article 4(5) exempts microenterprises providing services — fewer than 10 persons, with turnover or balance sheet total under €2 million — from the accessibility requirements and from every obligation attached to them. That is a large share of the people currently being sold compliance tooling, and it is worth reading before you write anything down.

Sources: Directive (EU) 2019/882 · Directive (EU) 2016/2102 · EN 301 549 (ETSI) · FTC v. accessiBe

## About this

This was written by the person who builds the plugin it discusses. That is stated plainly rather than buried, so you can weigh it.

Accessibility Audit — WCAG & EAA Compliance Checker

## More on this

Other pieces on the same ground.

- ### Does the European Accessibility Act apply to you? If you employ fewer than 10 people, probably not.
- Article 4(5) of Directive (EU) 2019/882 exempts microenterprises providing services from the accessibility requirements and from every obligation attached to them. Almost nobody selling EAA compliance tools mentions this, including, for a while, me.
- ### Your audit report says 2.1.1 fails on every element. Here is how to tell whether that is real.
- A vendor's keyboard test marks every control on the page as a Keyboard (2.1.1) failure. You unplug t
