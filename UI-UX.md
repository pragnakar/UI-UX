# UI/UX

## A Meta-Prompt for Human Interface Design and User Experience

**Version:** 1.0
**Repository:** https://github.com/pragnakar/UI-UX
**Parent Meta-Prompt:** LLM-Native Software Engineering — https://github.com/pragnakar/LLM_NATIVE_SOFTWARE_ENGINEERING
**Companion Meta-Prompts:** Deployment Engineering, DevOps, Database, Security Engineering, MLOps, API Design, Testing Strategy, Documentation, Scrum

---

## Thesis

Software that functions correctly but is difficult to use fails its users. UI/UX design is not decoration applied after functionality is built — it is the discipline of determining how functionality is presented, organized, and experienced. This meta-prompt ensures that user interface work produces interfaces that are intentionally designed, accessible by default, consistent by system, and specific to real user workflows — not to technically possible capabilities.

## When This Meta-Prompt Is Invoked

Invoke this meta-prompt when:
- A new user-facing interface is being designed or built
- An LLM agent is generating frontend code, component structures, or form layouts
- Existing UI needs evaluation against usability or accessibility standards
- A design system or component library needs to be established
- User workflows need to be modeled before implementation begins
- AI-generated UI is being reviewed before it ships

## Scope

**This meta-prompt covers:**
- User-centered design process: user research, personas, user journey mapping
- Information architecture: navigation structure, feature grouping, content organization
- Interaction design: workflows, form design, feedback patterns, error states, loading states
- Visual design: typography, color systems, spacing, hierarchy, design tokens
- Design systems and component libraries
- Responsive design across device categories
- Accessibility: WCAG 2.1 AA compliance as the non-negotiable baseline
- Usability testing and iterative design validation
- Agent-specific guidance for LLM-generated frontends

**This meta-prompt does NOT cover:**
- Application architecture and API design — handled by **LLM-Native Software Engineering**
- Data models that back UI views — handled by the **Database** meta-prompt
- Frontend deployment, CDN configuration, and build pipelines — handled by **Deployment Engineering**
- Frontend service monitoring and error rate tracking — handled by the **DevOps** meta-prompt

## Principles

1. **Design for the user's task, not the system's structure.** Navigation and information architecture must reflect what users are trying to accomplish — not how the backend is organized or how the database is modeled. A user should never need to understand the system's internal structure to complete their task.

2. **Accessibility is a baseline, not a feature.** WCAG 2.1 AA compliance is the minimum standard for every interface, internal or external. Keyboard navigation, screen reader compatibility, and sufficient color contrast are required from the first build — not retrofitted before launch.

3. **Consistency over creativity in component design.** The same action performed in different parts of the application must look and behave identically. Users build mental models from consistent patterns; inconsistency destroys trust and increases error rates.

4. **Every interactive element must communicate its state.** Loading, error, success, empty, and disabled states are designed explicitly for every interactive element. An element with no visible state change on interaction has a broken feedback loop.

5. **Error messages are help, not blame.** Error messages tell the user what happened, why it matters, and what to do next. "Something went wrong" and "Error 500" are not error messages. They are failures to communicate.

6. **Mobile-first, not mobile-adapted.** Responsive design begins at the smallest supported viewport. Designing desktop-first and compressing for mobile produces layouts with illegible text, untappable targets, and horizontal scroll.

7. **AI-generated UI requires human UX review before shipping.** LLM-generated interfaces default to generic layouts, omit edge case states, and miss accessibility requirements. All AI-generated frontend code is reviewed against this meta-prompt's checklist before it is considered shippable.

## Practices

### User Research and Personas

- Define at minimum two primary user personas before beginning interface design for any feature. Each persona includes: role, primary goals, common workflows, technical proficiency, and key frustrations.
- Map user journeys for the three most critical tasks in the application. Each journey includes: trigger, steps, decision points, and success/failure states.
- Design for the realistic user, not the ideal user. Realistic users skip instructions, misread labels, and interact with the interface in unexpected ways. Design survives this; ideal-user design does not.

### Information Architecture

- Navigation hierarchy should not exceed three levels for the primary user journey. Deep navigation trees are a structural organization problem, not a navigation problem.
- Group features by user goal, not by technical category. "Account settings" should be where users look for it, not where it is architecturally convenient.
- Primary actions are in primary positions. The most common action on any screen is the most visually prominent and most keyboard-accessible element.

### Interaction Design

- Form fields include: a visible label, placeholder or example value, validation state (success/error with icon and text), and helper text for non-obvious requirements.
- Every destructive action (delete, archive, any unrecoverable change) requires explicit confirmation. The confirmation dialog states precisely what will be destroyed and that the action cannot be undone.
- Loading states are immediate: any action taking more than 200ms shows a loading indicator. Any action taking more than 5 seconds shows progress feedback.
- Empty states (no data, no search results) include an explanation of why the state is empty and a clear, specific call to action for what the user does next.

### Visual Design and Design Systems

- Establish a design token system before building components: color primitives, semantic colors, typography scale, spacing scale, border radii, shadow levels. All component values reference tokens, not hardcoded values.
- Document every component's variants and states before implementation: default, hover, focused, active, disabled, loading, error, success.
- Typography hierarchy: use at most three font sizes in a UI section. Hierarchy is created by size, weight, and color — not by many different typefaces.
- Color system: primary, secondary, neutral, and semantic colors (success, warning, error, info). Every semantic color passes contrast requirements against its background.
- Never use color as the only differentiator between states. Color-blind users (8% of males, 0.5% of females) must interpret all states from text, icons, or patterns, not color alone.

### Responsive Design

- Design at three breakpoints: mobile (320–767px), tablet (768–1023px), desktop (1024px+).
- Minimum touch target size: 44×44px on mobile. Small touch targets are the single most common mobile usability failure in AI-generated interfaces.
- Horizontal scrolling is never acceptable on mobile. All content reflows to fit the viewport width.
- Navigation patterns that work on desktop (horizontal nav bars, hover menus) require full redesign on mobile — not compression or hamburger menus that reveal the same desktop structure.

### Accessibility (WCAG 2.1 AA)

- Color contrast: minimum 4.5:1 ratio for normal text, 3:1 for large text (18pt regular or 14pt bold).
- All images have meaningful `alt` text. Decorative images use `alt=""`.
- All interactive elements are keyboard-reachable via `Tab` and have a visible focus indicator. Suppressing the default focus ring without replacing it is an accessibility failure.
- Form inputs have associated `<label>` elements linked via `for`/`id` or `aria-labelledby`. Placeholder text is not a label.
- Error messages are associated with their input field via `aria-describedby` so screen readers announce the error when the field is focused.
- Page structure uses semantic HTML: `<main>`, `<nav>`, `<header>`, `<footer>`, `<section>`, heading levels in order (h1 → h2 → h3, never skipping).
- Run automated accessibility checks (axe, Lighthouse, or equivalent) on every PR. Automated checks catch approximately 30–40% of issues. Manual keyboard-only and screen reader testing is required before major releases.

### Usability Testing

- Test with real users before major releases — not internal stakeholders who are not the target audience.
- Minimum viable usability test: 5 users, 3 core tasks, think-aloud protocol.
- Record specific failures (user could not complete task) and near-failures (user completed task with visible confusion or hesitation).
- Changes made in response to usability findings are re-tested before shipping.

## Agent Instructions

When an LLM coding agent is operating under this meta-prompt:

**Do:**
- Use semantic HTML elements: `<button>` for buttons, `<a>` for navigation links, `<nav>` for navigation, `<main>` for page content, `<form>` for forms
- Include `aria-label` or an associated `<label>` for every interactive element that lacks visible text
- Generate all states explicitly: loading, error, empty, success — not just the happy-path state
- Use design tokens (CSS variables or theme values) for all colors, spacing, and typography — not hardcoded hex values or pixel values
- Write error messages that explain what happened and what the user should do next
- Include keyboard navigation support: proper `tabindex`, focus management for modals and dialogs (`focus-trap`), `Escape` key to close overlays
- Generate responsive layouts using `rem`/`em` units, `min()`, `clamp()`, CSS Grid, and Flexbox
- Include `alt` text for all `<img>` elements
- Set minimum touch target size to 44×44px for all interactive elements in mobile layouts

**Do NOT:**
- Use `<div onClick>` or `<span onClick>` for clickable elements — always use `<button>` or `<a>`
- Use color as the only differentiator between states
- Use placeholder text as a substitute for a visible label
- Generate a component with only the happy-path state and no loading, error, or empty states
- Hardcode color values, spacing, or typography when a design system or token system is defined
- Compress a desktop layout for mobile — generate mobile layouts from a mobile-first starting point
- Generate forms without visible client-side validation feedback
- Suppress the default browser focus ring without providing a visible custom focus style

**Verify before proceeding:**
- Does every interactive element use a semantic HTML element (`<button>`, `<a>`, `<input>`)?
- Are there explicit loading, error, and empty states for all dynamic content?
- Do all form inputs have associated `<label>` elements (not placeholder-as-label)?
- Do all images have `alt` text?
- Does the layout function at 320px viewport width without horizontal scroll?
- Does body text color contrast meet 4.5:1 against its background?
- Are all interactive elements reachable and operable via keyboard?

## Integration Points

- **LLM-Native Software Engineering:** UI/UX design requirements (data needed, interaction flows, component states) feed into API design and data model specifications. UI specifications belong in SPEC.md before frontend build phases begin. LLM-Native SE verification prompts for user-facing phases should include a UX review step against this meta-prompt's checklist.

- **Database:** Data requirements of UI views (what fields are displayed, pagination behavior, filter and sort options) determine what queries and indexes the database must support. Pagination design (cursor-based vs offset) is a joint decision between this meta-prompt and the Database meta-prompt.

- **Deployment Engineering:** Frontend static assets are built and published via CI/CD pipelines defined by Deployment Engineering. Asset hashing, CDN cache configuration, and build steps for bundling and minification are configured there. This meta-prompt defines what the build must produce; Deployment Engineering defines how it is delivered.

- **DevOps:** Frontend performance metrics (Core Web Vitals: LCP, FID/INP, CLS) are monitored as part of DevOps observability. Frontend JavaScript errors and failed API calls are tracked in the operational monitoring stack. User-facing SLOs are defined in UX performance terms (e.g., "95% of page loads complete LCP in under 2.5 seconds").

- **Security Engineering:** UI components handling sensitive data (authentication forms, payment inputs, PII display) follow security requirements from Security Engineering: CSRF protection, Content Security Policy, `HttpOnly` cookies, and output encoding. Accessibility and security reinforce each other — semantic HTML, visible focus styles, and form validation serve both user needs and security boundaries.

- **MLOps:** When interfaces present ML model outputs (recommendations, predictions, classifications), UI/UX governs how those outputs are displayed, explained, and how user feedback is captured. User interaction data collected through the interface may feed back into model retraining pipelines.

- **API Design:** The API Design meta-prompt ensures the API delivers data in the format the UI requires. UI data needs (field names, pagination behavior, filtering options) drive API contract decisions. This meta-prompt defines what the UI needs; API Design ensures the contract provides it efficiently.

- **Testing Strategy:** Frontend components require testing for all states: loading, error, empty, and success. Accessibility testing (automated with axe-core or Lighthouse, manual with screen readers) is part of the test plan. Visual regression testing catches unintended UI changes. End-to-end tests verify critical user journeys.

- **Documentation:** Design system documentation (component catalog, usage guidelines, design tokens) follows Documentation meta-prompt standards. User research findings, design decisions, and accessibility standards are documented as ADRs. Onboarding guides for new designers and frontend developers are maintained alongside code.

- **Scrum:** UI/UX design work precedes implementation by at least one sprint (design sprint pattern). User stories originate from user research and persona workflows defined here. Acceptance criteria for UI stories include explicit usability, accessibility, and responsive design conditions.

## Anti-Patterns

| Anti-Pattern | Why It's Harmful |
|---|---|
| Happy-path-only UI generation | Production interfaces encounter errors, loading delays, and empty states constantly; missing states produce broken, confusing experiences for real users |
| `<div onClick>` for interactive elements | Breaks keyboard navigation; invisible to screen readers; violates semantic HTML; creates inaccessible interfaces by default in all generated code |
| Placeholder text as label | When users begin typing, the label disappears; users cannot review what a field requires without clearing their input; screen readers often skip placeholders |
| Color as the only state indicator | Color-blind users cannot distinguish error from success; fails WCAG 1.4.1; the most common accessibility failure in AI-generated forms |
| Generic AI aesthetic applied to every project | LLMs default to identical card-grid layouts with blue primary buttons and grey secondary buttons; every application looks the same; the brand and user context are erased |
| Desktop-first responsive design | Mobile layout becomes an afterthought; results in illegible text at small viewports, 8px touch targets, and horizontal scrolling |
| Missing confirmation on destructive actions | Users accidentally delete data they intended to keep; no recovery path; support burden increases |
| Skipping accessibility on "internal tools" | Internal tool users have the same diversity of abilities as external users; accessibility is not a public-facing-only concern; it is a legal requirement in many jurisdictions |
| Importing a full component library without establishing design tokens | Library defaults become the de facto design system; components are overridden inconsistently; visual coherence degrades over time |

## Quick-Start Checklist

```
[ ] Define 2 primary user personas (role, goals, workflows, frustrations)
[ ] Map user journeys for the 3 most critical tasks
[ ] Establish design token system (colors, typography scale, spacing scale)
[ ] Define all component variants and states (default, hover, focus, disabled, loading, error, empty, success)
[ ] Set navigation hierarchy (max 3 levels for primary journey)
[ ] Verify all interactive elements use semantic HTML
[ ] Verify all form inputs have associated <label> elements
[ ] Verify body text color contrast meets 4.5:1 (WCAG 2.1 AA)
[ ] Verify all images have alt text
[ ] Verify all interactive elements are keyboard-reachable with visible focus indicator
[ ] Verify layout functions at 320px viewport width without horizontal scroll
[ ] Verify touch targets are minimum 44x44px on mobile
[ ] Generate loading, error, and empty states for all dynamic content
[ ] Add explicit confirmation dialogs to all destructive actions
[ ] Run automated accessibility check (axe or Lighthouse) — target zero violations
[ ] Plan usability test (5 users, 3 tasks) before major release
```

## Version History

- v1.0 — 2026-03-06 — Initial harmonization: full restructure to canonical meta-prompt template, added Principles, Practices, Agent Instructions, Integration Points, Anti-Patterns, and Quick-Start Checklist

---

*Part of the Meta-Prompt Ecosystem: https://github.com/pragnakar*
