# CI/CD for Microsoft Fabric — Series Index

A prescriptive, publication-quality how-to series covering **Git repository management, development management, and the CI/CD process in Microsoft Fabric** — written for both **default** and **secured** environments. Twenty-five entries across five layers, each a self-contained runbook.

Every entry follows the same shape: **prerequisites → numbered steps → validation → limitations → rollback**, with its own architecture diagram and a dedicated **Secured environment — what changes** section. No conceptual padding — the *what* is kept short so the *how* stays front and centre. Every step is grounded in Microsoft Learn.

---

## At a glance

| Layer | Entries | Focus |
|---|---|---|
| **Layer 1 — Git foundations** | 01–05 | Provider choice, workspace connection, repository layout, the sync loop, and branching strategy. |
| **Layer 2 — Development management** | 06–10 | Developer isolation, workspace topology, dependency binding, pull request gates, and permissions. |
| **Layer 3 — Environment promotion** | 11–15 | Variable libraries, deployment pipelines, deployment rules, and per-item rebinding. |
| **Layer 4 — Release automation** | 16–20 | Git REST APIs, deployment pipeline APIs, the Fabric CLI, Azure DevOps, and GitHub Actions. |
| **Layer 5 — Secured environment** | 21–25 | Service principals, private links, in-network build agents, secrets and approvals, and audit. |
| | **25 total** | |

**Formats.** Word documents sit in `fabric-cicd/`. A markdown copy with the diagrams lives in [`fabric-cicd/markdown/`](fabric-cicd/markdown/) — ready to drop into a Git repository. LinkedIn-ready article HTML and feed pitches are in [`fabric-cicd/linkedin/`](fabric-cicd/linkedin/).

---

## The decision that shapes everything

Fabric offers two promotion mechanisms, and they are **not equally available** in a locked-down estate:

| | Git-based deployment | Deployment pipelines |
|---|---|---|
| Promotion trigger | A merge into a release branch | A person or an API call in Fabric |
| Audit trail | Git history plus build runs | Deployment history |
| Parameterisation | `parameter.yml` and variable libraries | Deployment rules and variable libraries |
| **Workspaces denying public access** | **Supported** — the Git API works over private links | **Not supported** — pipelines cannot connect |

> **Lead finding.** If any workspace in a deployment pipeline denies public inbound access, deployment pipelines cannot connect to it — and inbound restriction is blocked for any workspace already assigned to a pipeline. Deployment pipelines and workspace-level private links are mutually exclusive today. Entry 22 covers this in full.

---

## The series

- **00 · [Series overview](fabric-cicd/markdown/Fabric-CICD-00-Series-Overview.md)** — start here

### Layer 1 — Git foundations

*Provider choice, workspace connection, repository layout, the sync loop, and branching strategy.*

- **01** · [Choose Your Git Provider and Switch On Fabric Git Integration](fabric-cicd/markdown/Fabric-CICD-01-Git-Provider-And-Tenant-Settings.md) — Pick Azure DevOps or GitHub, then enable the exact tenant settings that make source control possible.
- **02** · [Connect a Workspace to a Repository, Branch, and Folder](fabric-cicd/markdown/Fabric-CICD-02-Git-Connect-Workspace.md) — Bind one workspace to exactly one branch and one folder — and control the direction of the first sync.
- **03** · [Read the Fabric Repository Layout: Folders, .platform, and Logical IDs](fabric-cicd/markdown/Fabric-CICD-03-Git-Repository-Layout.md) — Understand what Fabric actually writes to Git so you can review diffs and predict deployments.
- **04** · [Commit, Update, and Resolve Conflicts Without Losing Work](fabric-cicd/markdown/Fabric-CICD-04-Git-Commit-Update-Conflicts.md) — Run the two-direction sync safely, and know your options when both sides changed.
- **05** · [Choose a Branching Strategy That Fits Fabric Workspaces](fabric-cicd/markdown/Fabric-CICD-05-Git-Branching-Strategy.md) — Map branches to workspaces deliberately — the one-branch-per-workspace rule decides your whole topology.

### Layer 2 — Development management

*Developer isolation, workspace topology, dependency binding, pull request gates, and permissions.*

- **06** · [Give Every Developer an Isolated Workspace with Branch Out](fabric-cicd/markdown/Fabric-CICD-06-Dev-Branch-Out-Workspace.md) — Create a private branch and workspace in one action, so nobody develops on top of anyone else.
- **07** · [Design a Development, Test, and Production Workspace Topology](fabric-cicd/markdown/Fabric-CICD-07-Dev-Workspace-Topology.md) — Lay out environments so promotion is predictable and no workspace serves two masters.
- **08** · [Know What Auto-Binds Across Workspaces — and What Does Not](fabric-cicd/markdown/Fabric-CICD-08-Dev-Dependency-Binding.md) — The single table that explains most failed Fabric deployments.
- **09** · [Gate Every Change with Pull Requests and Branch Policies](fabric-cicd/markdown/Fabric-CICD-09-Dev-Pull-Request-Gates.md) — Make review, build validation, and approval mandatory before anything reaches a shared branch.
- **10** · [Set the Permission Guardrails Around Fabric Development](fabric-cicd/markdown/Fabric-CICD-10-Dev-Permissions-And-Guardrails.md) — Decide who may connect, commit, branch, and deploy — before someone decides for you.

### Layer 3 — Environment promotion

*Variable libraries, deployment pipelines, deployment rules, and per-item rebinding.*

- **11** · [Centralise Environment Configuration with Variable Libraries](fabric-cicd/markdown/Fabric-CICD-11-Promote-Variable-Libraries.md) — Put every environment-specific value in one item with a value set per stage.
- **12** · [Build and Configure a Fabric Deployment Pipeline](fabric-cicd/markdown/Fabric-CICD-12-Promote-Deployment-Pipeline.md) — Wire development, test, and production into stages and promote content without touching Git.
- **13** · [Apply Deployment Rules So Content Points at the Right Stage](fabric-cicd/markdown/Fabric-CICD-13-Promote-Deployment-Rules.md) — Override source-stage bindings with per-item rules on the target stage.
- **14** · [Rebind Direct Lake Semantic Models Across Stages](fabric-cicd/markdown/Fabric-CICD-14-Promote-Direct-Lake-Rebinding.md) — The one item type that does not follow the rules — and the two supported ways to fix it.
- **15** · [Rebind Notebooks, Data Pipelines, and Shortcuts Across Stages](fabric-cicd/markdown/Fabric-CICD-15-Promote-Notebooks-Pipelines-Shortcuts.md) — Three item types, three different binding behaviours, three fixes.

### Layer 4 — Release automation

*Git REST APIs, deployment pipeline APIs, the Fabric CLI, Azure DevOps, and GitHub Actions.*

- **16** · [Automate Git Operations with the Fabric REST APIs](fabric-cicd/markdown/Fabric-CICD-16-Automate-Git-REST-APIs.md) — Connect, commit, and update workspaces from code instead of the Source control panel.
- **17** · [Automate Stage Promotion with the Deployment Pipelines API](fabric-cicd/markdown/Fabric-CICD-17-Automate-Deployment-Pipeline-APIs.md) — Trigger promotions from a build instead of a browser, with notes and selective payloads.
- **18** · [Deploy from a Terminal with the Fabric CLI](fabric-cicd/markdown/Fabric-CICD-18-Automate-Fabric-CLI.md) — One command-line tool for exploration, scripted deployment, and agent-based release.
- **19** · [Build an Azure DevOps Release Pipeline for Fabric](fabric-cicd/markdown/Fabric-CICD-19-Automate-Azure-DevOps.md) — A YAML pipeline that deploys Fabric items with fabric-cicd, gated by environments and approvals.
- **20** · [Build a GitHub Actions Workflow for Fabric](fabric-cicd/markdown/Fabric-CICD-20-Automate-GitHub-Actions.md) — The same release process on GitHub, with OIDC instead of stored secrets.

### Layer 5 — Secured environment

*Service principals, private links, in-network build agents, secrets and approvals, and audit.*

- **21** · [Run Fabric CI/CD as a Service Principal, Not a Person](fabric-cicd/markdown/Fabric-CICD-21-Secured-Service-Principal.md) — Give automation its own identity, then remove the secret from it entirely.
- **22** · [Operate Fabric CI/CD Behind Workspace-Level Private Links](fabric-cicd/markdown/Fabric-CICD-22-Secured-Private-Links.md) — What still works when public access is denied — and what stops working entirely.
- **23** · [Run Build Agents Inside Your Network](fabric-cicd/markdown/Fabric-CICD-23-Secured-Build-Agents.md) — Put the deployment runner where the private endpoint is, because hosted agents cannot reach it.
- **24** · [Protect Deployment Secrets and Gate Production Releases](fabric-cicd/markdown/Fabric-CICD-24-Secured-Secrets-And-Approvals.md) — Keep credentials in a vault, and make production wait for a human.
- **25** · [Audit and Monitor Your Fabric CI/CD Process](fabric-cicd/markdown/Fabric-CICD-25-Secured-Audit-And-Monitoring.md) — Prove who changed what, when — and detect the changes that bypassed your process.

---

## Reading paths by role

| If you are… | Read in this order | Why |
|---|---|---|
| Setting up Fabric CI/CD from scratch | 01 → 02 → 05 → 07 → 12 | The minimum viable path from no source control to a working promotion. |
| Platform / Fabric administrator | 01 → 10 → 21 → 22 → 25 | Tenant settings, guardrails, identity, network, and assurance. |
| Analytics developer | 02 → 04 → 06 → 09 | The daily loop: connect, sync, isolate, and get reviewed. |
| Debugging a bad deployment | 08 → 14 → 15 → 13 | Diagnosis first, then the per-item remedies. |
| Build / DevOps engineer | 16 → 17 → 18 → 19 → 20 | The API primitives, then complete pipelines on either platform. |
| Security architect / auditor | 22 → 21 → 23 → 24 → 25 | Network constraints first — they decide the rest. |

---

## Where to start

- **Nothing under source control yet?** Layer 1, in order. Entries 01 and 02 are the minimum viable state.
- **Developers overwriting each other?** Layer 2, starting at entry 06.
- **Deployments succeed but read the wrong data?** Entry 08 for the diagnosis, then 11, 13, 14, and 15 for the fixes.
- **Promotion still manual?** Layer 4 — entry 16 for the primitives, entry 19 for a complete pipeline.
- **Facing a private-link mandate or an audit?** Layer 5 — and read entry 22 *before* restricting anything.

---

> **A note on currency** — Fabric CI/CD ships quickly. Every step here reflects the product and documentation as of publication, including dated changes already announced (the **December 1, 2026** Git integration permission change and the **February 12, 2026** deployment pipeline semantic model retirement). Verify current behaviour in your own tenant before standardising on it.
