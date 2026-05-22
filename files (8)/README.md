# Solon Playbooks

A collection of open-source code review playbooks for [Solon AI](https://solonreview.dev) — the team standards enforcement layer for AI-generated code.

Each playbook is a set of rules that Solon automatically enforces on every pull request. No linter config, no YAML gymnastics — just describe your team's standards and Solon enforces them.

---

## Available Playbooks

| Playbook | Rules | Best For |
|---|---|---|
| [Next.js + TypeScript](./nextjs-typescript/playbook.json) | 12 | Next.js App Router teams |
| [Security](./security/playbook.json) | 12 | Any JavaScript/TypeScript codebase |
| [Accessibility (WCAG 2.2)](./accessibility/playbook.json) | 11 | React/Next.js with a11y requirements |
| [Vibe Coder](./vibe-coder/playbook.json) | 12 | Teams shipping AI-generated code (Cursor, Claude Code, Copilot) |

---

## How to Use

### With Solon AI (Recommended)

1. Install [Solon AI](https://github.com/apps/solon-ai) on your GitHub repo
2. Copy the playbook JSON you want into your repo as `.solon.config.json`
3. Solon automatically reviews every PR against your chosen rules

```json
{
  "playbooks": ["security", "nextjs-typescript"],
  "severity": {
    "blocking": true,
    "warning": true,
    "info": false
  }
}
```

### Combine Playbooks

Stack multiple playbooks for comprehensive coverage:

```json
{
  "playbooks": ["security", "nextjs-typescript", "accessibility"],
  "severity": {
    "blocking": true,
    "warning": true,
    "info": false
  }
}
```

---

## Playbook Breakdown

### Next.js + TypeScript
Covers the most common production mistakes in Next.js App Router codebases: type safety, Server vs Client Component misuse, data fetching patterns, route handler validation, and performance anti-patterns.

**Blocking rules:** No `any` types, untyped props, `useEffect` for data fetching, unhandled async errors, hardcoded env values, unvalidated route handler input.

### Security
Covers OWASP Top 10 patterns for JavaScript/TypeScript web applications. Built for teams that don't have a dedicated security engineer but ship customer-facing products.

**Blocking rules:** Hardcoded secrets, SQL injection, XSS via `dangerouslySetInnerHTML`, missing auth checks, IDOR vulnerabilities, sensitive data in logs, `localStorage` for auth tokens, dynamic `require`/`eval`.

### Accessibility (WCAG 2.2)
Covers Level AA compliance for React/Next.js. Catches what automated axe/Lighthouse scans miss — semantic structure, keyboard patterns, focus management, and ARIA correctness.

**Blocking rules:** Missing alt text, non-keyboard-accessible interactive elements, unlabeled form inputs, focus removed without replacement, modals that don't trap focus.

### Vibe Coder (AI-Generated Code)
Built specifically for teams shipping code written by Cursor, Claude Code, GitHub Copilot, or similar tools. Targets the exact failure patterns AI models produce most often.

**Blocking rules:** `any` escape hatches, unhandled Promises, hallucinated imports, wrong third-party API signatures.

---

## Contributing

Have a playbook your team uses? Open a PR.

Format requirements:
- Valid JSON matching the [playbook schema](./schema.json)
- At least 8 rules
- Each rule must have a `bad` and `good` example
- Severity must be `blocking`, `warning`, or `info`

---

## Schema

```json
{
  "name": "string",
  "version": "string",
  "description": "string",
  "author": "string",
  "tags": ["string"],
  "rules": [
    {
      "id": "string",
      "title": "string",
      "severity": "blocking | warning | info",
      "description": "string",
      "examples": {
        "bad": "string",
        "good": "string"
      }
    }
  ]
}
```

---

## License

MIT — use these playbooks freely in any tool, not just Solon.

---

Built by [Donta' Ruffin](https://linkedin.com/in/dontaruffin) · [solonreview.dev](https://solonreview.dev)
