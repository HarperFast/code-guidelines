# Harper Repository Meta Documents

Companion to the [public repository policy](./repository-policy.md). The policy says **which** meta documents an active public repo carries; this document covers the **purpose, scope, and authorship** of each one, so that the right content lands in the right file. It applies to humans and agents alike.

Scope follows the policy's: these expectations are written for **active public** repositories. Archived repos keep the taxonomy type and archive note the policy requires of them and are exempt from the rest — they are read-only, so there is nothing to add.

Treat these as living documents: update them as the repository evolves.

## How meta documents are supplied

Two mechanisms, and the difference is the thing to get right:

- **Inherited org-wide.** GitHub serves `CONTRIBUTING`, `CODE_OF_CONDUCT`, `SECURITY`, and `SUPPORT` from [`HarperFast/.github`](https://github.com/HarperFast/.github) to every repository in the organization that does not define its own. A repo with none of those files already has all four.
- **Repo-local.** `LICENSE`, `README`, and `AGENTS.md` are never inherited; if a repo wants one, it writes its own. The policy _requires_ `LICENSE` and `README`; `AGENTS.md` is optional and added when a repo has agent-specific facts worth recording.

**Inheritance is the default; a local copy is the exception.** Add a repo-local version of an inherited document only when that repo genuinely needs to say something the org version does not — and remember that a local file _replaces_ the org one for that repo in full, so the repo then owns keeping it current. Never copy an org file in unchanged: a verbatim copy is a second source for the same policy, and it will drift.

Every document described here lives in a public repository and is therefore **public** — `CONTRIBUTING.md` and `AGENTS.md` included, despite both being written for people and agents already working on the project. Credentials, tokens, private hostnames, internal-only runbooks, and anything else unpublishable belong in internal documentation, never in a repo-local meta document. A public repo is [training surface](./repository-policy.md#why-this-exists); what lands in one of these files is indexed and ingested.

## LICENSE

Required, repo-local, on every active public repo — there is no org-wide default and no inheritance.

The license is the legal statement of what others may do with the code, so it is the one meta document that is never a judgment call to include. See the [public repository policy](./repository-policy.md#required-meta-documents) for the baseline.

## README.md

Required, repo-local. The primary entrypoint for any project. It answers _what is this?_, _how do I use it?_, and _where do I go next?_.

Everyone reads the README: users, contributors, evaluators, agents, etc.

### What belongs here

- Project summary and purpose
- Installation and usage instructions
- Public API reference (if not documented elsewhere)
- Links to CONTRIBUTING, LICENSE, and community spaces (Slack, Discord, forums, etc.)
- Links to external documentation (hosted docs, changelogs, blog/marketing)
- Badge/status indicators if relevant
- The archive note, if the repo is archived (see the [policy](./repository-policy.md#required-archive-note))

### What does not belong here

- Internal development workflows
- Contributor onboarding
- Agent-specific instructions
- In-depth usage guides (consider dedicated guides or posts instead)

### Template

> **Deferred.** A README template is tracked as follow-up work; the scope guidance above is the current reference.

## CONTRIBUTING.md

Inherited org-wide by default; repo-local by exception.

The **public** contributor-facing guide to a project. It answers _how do I work on this project — and should I?_. The org-wide default in [`HarperFast/.github`](https://github.com/HarperFast/.github/blob/main/CONTRIBUTING.md) covers whether Harper accepts contributions at all and how to reach maintainers, and explicitly routes readers to the repository's own `CONTRIBUTING.md` for specifics.

Write a repo-local one when the project has specifics worth stating — which is most repos with a build, a test suite, or a release process — or to say that contributions are not accepted here.

A repo-local file replaces the org default entirely, so the org-wide contribution policy and contact routing stop reaching that repo's readers. Link back to it rather than restating it: open the local file with a line like `Harper's [organization-wide contribution policy](https://github.com/HarperFast/.github/blob/main/CONTRIBUTING.md) applies; what follows is specific to this repository.` That keeps one source for the shared text and leaves the local file holding only what is actually local.

Its readers are maintainers and contributors (humans and agents), but it is a public file in a public repo: write it for an outside contributor.

### What belongs here

- Repository structure overview
- Development environment setup
- Contribution workflow (branching, PRs, commit conventions)
- Build process
  - Build command(s)
  - Relevant configuration
- Release process
  - Manual vs automated steps
- Testing guide
  - How tests are structured
  - How to add new ones
  - How to execute them
  - Known flakiness
  - Manual local testing
- Code style and formatting rules
  - Linter and formatting commands
  - Relevant configuration
- CI environment
- Development-facing documentation
  - Particularly useful APIs for development
  - Scripts necessary for development/testing

### What does not belong here

- Public interface documentation (API, scripts, etc.)
- Usage information
- Agent specific instructions
- Internal-only material: credentials, private infrastructure, internal runbooks, or anything else that cannot be published

### Template

> **Deferred.** A CONTRIBUTING template is tracked as follow-up work; the scope guidance above is the current reference.

## AGENTS.md

Optional, repo-local; never inherited.

A minimal, agent-specific document _complementary_ to the `README.md` and `CONTRIBUTING.md`. It answers _what does an agent need to know that it **cannot reliably infer** from existing documentation?_. Furthermore, it does **not replace or duplicate** existing documentation.

The audience for this document is strictly agents. While humans may read it too, the primary utility of this document is meant to be purely for agents. Any information relevant to a human should exist within another document (likely `README.md` or `CONTRIBUTING.md`). It should accelerate the agent's comprehension of the code base without excessive file reads and token usage.

That last point is why `AGENTS.md` may restate a bare command — `npm run build`, the test invocation — that `CONTRIBUTING.md` also documents: the agent gets it in one read instead of three. Keep the restatement to the command itself and leave the explanation in `CONTRIBUTING.md`, which stays the source of truth; when a command changes, `AGENTS.md` is one of the files to update. What does not belong here is a second copy of `CONTRIBUTING.md`.

### What belongs here

- Facts or instructions that may seem obvious to a human, but would require the agent to read and understand specific project files
- Specific instructions to- or not-to- do such as commands to execute or file paths to interact with
- Preferences for agentic workflows such as specific ways to attribute or sign-off commits or particular headers to include in requests

### What does not belong here

- Project description or summary (README.md)
- Contribution workflows: how to open a PR, commit conventions, the release process (CONTRIBUTING.md)
- Prose written for a person — rationale, onboarding narrative, explanation. If a human contributor needs to _read_ it, it belongs in another document
- Secrets of any kind: tokens, API keys, internal hostnames, or private endpoints. An agent that needs a credential reads it from the environment; the file naming that environment variable is public

### Template

```md
# AGENTS.md

Review `README.md` and `CONTRIBUTING.md` for all relevant repository information.

## Development Tips

- Use `npm install` to install dependencies.
- Use `npm run build` to compile `src/` to `dist/`.
- Do not edit files in `dist/`; it is compiled output.
- Do not run `npm version` or `npm publish`; these commands are for humans only.
- [Any file/extension constraints specific to this repo's module system.]

## Code Style

- [Language and module system in use: ESM, CJS, TypeScript, etc.]
- [Any enforced syntax restrictions, e.g. erasable-only TypeScript.]
- [Formatter command if one exists, or note that none exists.]

## Testing

- [How to run the test suite.]
- [Any required setup steps before first run, and when to re-run them.]
- [Known slow operations that should not be interpreted as failure.]
- [Any test files or areas that are intentionally skipped or work-in-progress;
  note what an agent should not do with them.]
- [Note if there are currently no tests.]

## CI

- [Status of CI and any known disabled conditions.]
- [Where to find logs or artifacts on failure.]
```

## CODE_OF_CONDUCT.md

Inherited org-wide by default; repo-local by exception.

The behavioral standard for everyone participating in the project, and the route for reporting a violation. The org-wide [`CODE_OF_CONDUCT.md`](https://github.com/HarperFast/.github/blob/main/CODE_OF_CONDUCT.md) applies to every Harper repository.

Override it only if a repo has a genuinely different standard or reporting path — a jointly-owned or foundation-governed project, for example. A repo-local copy that only restates the org text is drift waiting to happen; leave it inherited instead.

## SECURITY.md

Inherited org-wide by default; repo-local by exception.

How to report a vulnerability, and what a reporter can expect in return. The org-wide [`SECURITY.md`](https://github.com/HarperFast/.github/blob/main/SECURITY.md) is the default reporting path for every Harper repository, and GitHub surfaces it from the repo's Security tab even when the file is inherited.

Override it when a repo needs its own disclosure terms — a different contact, a bug bounty scope, supported-version statements, or a published signing key. State what differs; don't restate what doesn't.

## SUPPORT.md

Inherited org-wide by default; repo-local by exception.

Where to go for help, which is deliberately not the same as where to report a bug. The org-wide [`SUPPORT.md`](https://github.com/HarperFast/.github/blob/main/SUPPORT.md) covers issues, Discord, Code of Conduct reports, and the customer support and `opensource@` contacts.

Override it when a repo has its own support channel, or when it is unmaintained and readers need to be told so plainly. Otherwise leave it inherited.
