# Example: Design System Project

This example shows how Agent Execution OS can be adapted for a design system, component library, or token system.

## Project type

Design system / component library.

## Risk profile

Medium to high, depending on adoption. Risks include breaking component APIs, visual regressions, accessibility regressions, token drift, and release mistakes.

## Example sections

```text
Section 1: Foundation, Package Setup & Release Safety
Section 2: Token Architecture
Section 3: Component API Standards
Section 4: Core Component Migration
Section 5: Documentation & Storybook
Section 6: Accessibility & QA
Section 7: Versioning, Changelog & Release
Section 8: Adoption Tooling & Governance
```

## Design-system-specific quality extensions

- Component changes require Storybook examples.
- Interactive components require accessibility notes.
- Token changes require migration notes.
- Breaking prop/API changes require explicit approval.
- Visual changes require before/after documentation when practical.
- Public package exports must be intentional.
- Do not change component APIs casually.

## Example task names

```text
01_audit-existing-component-apis.md
02_define-canonical-prop-taxonomy.md
03_add-storybook-coverage-for-button.md
04_add-accessibility-contract-for-dialog.md
05_create-release-readiness-checklist.md
```

## Example user request

```text
I need the package publishing token so the release pipeline can publish test releases.

How to get it:
1. Open the package registry dashboard.
2. Go to Access Tokens.
3. Create a token scoped only to this package/project.
4. Add it to CI secrets as `NPM_TOKEN`.

Safety: do not paste the token into chat or commit it. Use the narrowest permission scope available.

Next: after the token is added, the release verification task can run a dry-run publish.
```
