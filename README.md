# UI/UX Meta-Prompt

A structured protocol for designing and generating user interfaces that are intentionally designed, accessible by default, consistent by system, and specific to real user workflows — not to technically possible capabilities.

## What Is a Meta-Prompt?

A meta-prompt is a structured protocol document that initializes an AI-assisted development environment before task execution begins. Instead of starting with an ad-hoc prompt, the meta-prompt establishes workflow structure, behavioral constraints, and quality standards so that subsequent prompts operate inside a disciplined, well-defined system.

## This Meta-Prompt

UI/UX governs how software functionality is presented and experienced by users. It covers:

- **User Research** — persona definition, user journey mapping for critical tasks, designing for realistic (not ideal) users
- **Information Architecture** — navigation hierarchy (max 3 levels), goal-based feature grouping, primary actions in primary positions
- **Interaction Design** — form patterns with visible labels and validation states, destructive action confirmations, loading/error/empty states for all dynamic content
- **Visual Design and Design Systems** — design token systems (colors, typography, spacing), component variant documentation, semantic color with contrast requirements
- **Responsive Design** — mobile-first at 320px, 44×44px minimum touch targets, no horizontal scroll on mobile
- **Accessibility (WCAG 2.1 AA)** — 4.5:1 contrast ratio, semantic HTML, keyboard navigation, screen reader compatibility, `aria` attributes
- **Usability Testing** — 5-user think-aloud protocol, failure recording, re-testing after changes
- **Agent Instructions** — specific behavioral rules for LLM-generated frontends, including semantic HTML requirements and state completeness

This meta-prompt specifically addresses the gap between AI-generated interfaces that *function* and those that provide *good user experience*.

## Part of the Meta-Prompt Ecosystem

This meta-prompt works alongside companion protocols:

| Meta-Prompt | Repository | Purpose |
|---|---|---|
| LLM-Native Software Engineering | https://github.com/pragnakar/LLM_NATIVE_SOFTWARE_ENGINEERING | Architecture and application development |
| Deployment Engineering | https://github.com/pragnakar/Deployment_Engineering | Infrastructure, containerization, and deployment |
| DevOps | https://github.com/pragnakar/DevOps | Runtime operations, observability, and reliability |
| Database | https://github.com/pragnakar/Database | Data persistence, schema design, and management |
| UI/UX | https://github.com/pragnakar/UI-UX | Interface and experience design |
| Security Engineering | https://github.com/pragnakar/Security_Engineering | Threat modeling, secure coding, and vulnerability management |
| MLOps | https://github.com/pragnakar/MLOps | Model lifecycle, training pipelines, and production ML |
| API Design | https://github.com/pragnakar/API_Design | Interface contracts, versioning, and developer experience |
| Testing Strategy | https://github.com/pragnakar/Testing-Strategy | Test architecture, coverage strategy, and quality verification |
| Documentation | https://github.com/pragnakar/Documentation | Technical writing, knowledge management, and developer docs |
| Scrum | https://github.com/pragnakar/Scrum | Agile sprint cycles, backlog management, ceremonies, and team coordination |

## Usage

1. Load `UI-UX.md` into your AI coding agent when user interface design or frontend generation begins
2. The agent follows the Principles, Practices, and Agent Instructions to generate semantic HTML, accessible components, responsive layouts, and all required component states
3. Use the Quick-Start Checklist to verify all UX and accessibility baselines before any user-facing feature ships
4. Run automated accessibility checks (axe, Lighthouse) on every pull request; supplement with manual keyboard and screen reader testing before major releases

## License

MIT

## Author

Pragnakar Pedapenki
