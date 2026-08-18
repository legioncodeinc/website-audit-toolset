<!--
URL: https://webvitals.tools/blog/google-core-web-vitals-update-2026/
Fetch date: 2026-08-18
Source type: vendor blog
Research cluster: core-web-vitals-and-delivery
Archived by: forge stage 2 sweep (mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc. build sequence step 6.
-->

# Core Web Vitals Update 2026: What Changed, What to Fix First — WebVitals.tools
URL: https://webvitals.tools/blog/google-core-web-vitals-update-2026/
Published: 2026-04-23

Core Web Vitals Update 2026: What Changed, What to Fix First — WebVitals.tools

Industry Analysis

# Core Web Vitals Update 2026: What Changed, What to Fix First

By Marcus Chen · April 23, 2026 · Updated June 27, 2026 · 14 min read

The 2026 Core Web Vitals update did not move the three published thresholds. What it did do is tighten the INP measurement methodology, expand CrUX soft-navigation coverage for single-page applications, and make TTFB a more prominent diagnostic in PageSpeed Insights. If you were borderline on INP under the old measurement, you may be failing under the new one — and most teams have not re-measured yet.

This is an analyst synthesis rather than a news report. It draws on web.dev documentation updates through April 2026, the Chrome team's public writing, the evolving CrUX dataset, and the practical patterns we have seen across the sites we audit. The aim is to answer three questions in order: what actually changed in 2026, what that means for search and for AI-powered answer engines, and what an engineering team should fix first if their numbers slipped.

The short version: LCP is a mostly-solved problem for teams that have done the work. CLS is mature and well-understood. INP is where the remaining performance debt lives for the majority of sites. And AI search is raising the stakes around all three metrics in ways that were not anticipated when the program launched in 2021.

## What has actually changed since 2024

The FID-to-INP transition, which became official in March 2024, is now fully bedded in. First Input Delay measured only the delay before the browser began processing the first interaction on a page. It was a narrow proxy that was easy to game and easy to pass while still shipping an application that felt sluggish and unresponsive. INP measures the latency of the slowest interaction across the entire page lifecycle, from tap to visible update. That is a fundamentally harder bar.

The practical consequence is that teams who passed CWV under the old regime and assumed nothing had changed discovered in late 2024 and through 2025 that their INP scores told a different story. Many sites that reported green FID scores were registering INP values north of 400 milliseconds. The Chrome User Experience Report, which measures real users on real devices, does not lie in the way that lab tests can.

At the same time, Google has continued to publish threshold clarifications and diagnostic guidance on web.dev. The p75 requirement — that 75 percent of a site's page loads must meet each threshold — has remained constant, but the guidance around how that p75 is measured across origins and subpages has become more precise. Teams running large e-commerce sites or media properties with heterogeneous page types have had to confront the fact that a few high-traffic page templates dragging down the p75 can invalidate good work done elsewhere in the stack.

FID measurement signals have been progressively de-emphasized in tooling. Chrome DevTools performance panels and field data tools have updated their reporting to center INP. Teams still referencing FID-era dashboards to evaluate responsiveness are flying with outdated instruments.

"Teams that passed Core Web Vitals under the FID regime and have not revisited their INP numbers since 2024 are likely carrying more performance debt than their dashboards suggest."

## The three metrics in 2026

The three Core Web Vitals thresholds have not changed: LCP at 2.5 seconds, INP at 200 milliseconds, CLS at 0.1. What has changed is the distribution of pass rates across the web and the relative difficulty of each metric for teams starting optimization work today.

78%

Origins passing LCP

72%

Origins passing INP

84%

Origins passing CLS

LCP at 78% reflects two years of ecosystem improvement: framework-level image optimization defaults, widespread adoption of CDN edge delivery, and the maturation of streaming SSR patterns. The LCP guide covers the optimization patterns in depth, but the high-level story is that modern frameworks have made the right default choices much easier to reach. The remaining 22% of origins failing LCP are disproportionately sites on legacy stacks, high-latency hosting, or with unoptimized hero images that are not benefiting from automatic format conversion and responsive sizing.

CLS at 84% is the most mature metric in the suite. Layout shift causes are well-catalogued — late-loading images without dimensions, injected banners, font swaps — and the fixes are well-understood and not particularly difficult to implement. The CLS guide covers the full taxonomy. CLS is unlikely to receive major threshold revisions in the near term; it has settled into a diagnostic role as much as a ranking signal.

INP at 72% is where the work is. At 72%, it is the lowest-passing Core Web Vital, it is the newest, and it is the hardest to fix because it requires understanding the event loop, long tasks, and the rendering pipeline rather than just optimizing asset delivery. The full breakdown is in the INP guide.

## INP is where the work is now

INP's 200-millisecond threshold sounds generous until you understand what it is measuring. The metric captures the full duration from the moment a user interacts — a click, a keypress, a tap — to the moment the browser has committed a new frame in response. That duration includes the event handler execution time, any re-rendering triggered by state changes, and the browser's own layout and paint work. On a mid-range Android device with a main thread that is regularly occupied by JavaScript parsing, third-party scripts, and reactive framework overhead, hitting that 200ms threshold consistently is genuinely difficult.

The critical distinction from FID is that INP measures the slowest interaction across the session, not just the first. FID was easy to pass on pages that had a fast first interaction before JavaScript fully loaded. INP cannot be gamed in the same way. It catches long tasks that are invisible to FID but that users experience every time they interact with a search box, a filter panel, a shopping cart, or a navigation menu. If your application has a single interaction handler that triggers an expensive re-render, that will show up in your INP p75 score even if every other interaction is fast.

"If your team has not specifically invested in INP work, you are almost certainly failing it."

The React ecosystem has provided partial answers through concurrent features.`useTransition` and`useDeferredValue` allow developers to mark state updates as non-urgent, yielding control back to the browser during expensive renders and keeping the main thread available to respond to user input. These APIs genuinely help, but they require deliberate adoption. Upgrading to React 18 or 19 without actually using the concurrent APIs does not improve INP. The same applies to Angular's signal-based reactivity, which shipped as stable in Angular 17 and has proven effective at reducin
