# Security Policy

## 1. Purpose

This policy describes how to report security vulnerabilities affecting [GameCatalog](https://github.com/YuStellarGamesStudio/GameCatalog), how reports should be handled, and the boundaries for responsible security research.

GameCatalog is maintained under the YuStellarGamesStudio GitHub organization. Its repository includes Jekyll configuration for a GitHub Pages site and a `CNAME` identifying `data.ysgs.app` as the configured custom domain. A configured domain does not, by itself, establish that a deployment is live or that every service on that domain is part of this project.

The security concerns addressed by this policy include the integrity of repository content, the safety of generated pages and catalog information, the confidentiality of credentials, and the security of the publication process.

**Do not disclose an unpatched vulnerability, credentials, or sensitive proof-of-concept material in a public issue, pull request, discussion, or commit.**

## 2. Supported Versions and Deployments

Security fixes are targeted at the current `main` branch. This policy does not establish long-term support for older commits or separate release branches.

| Version or deployment | Security support scope |
| --- | --- |
| Current `main` branch | Primary target for investigation and security fixes |
| Project-controlled site built from this repository | In scope for project-specific vulnerabilities; the deployed revision must be identified when possible |
| Older commits, snapshots, or archived copies | No ongoing backport commitment; report issues that may also affect `main` |
| Other branches or experimental changes | No independent support commitment; relevant findings may inform fixes on `main` |
| Forks, mirrors, and independently hosted copies | Maintained by their respective operators, not covered by this project's deployment support |
| Third-party games, stores, downloads, or services linked by catalog content | Outside this project's maintenance scope; report to the responsible vendor |

A current source revision and a published site may differ. Reports about a deployment should include the observed URL and time, even when the source revision is unknown.

If you consume catalog content or host your own copy, keep your source and build dependencies current. Applying a repository fix does not automatically update independent deployments, caches, or downstream consumers.

## 3. What to Report

### 3.1. Findings within scope

Report a concrete security weakness affecting project-controlled content, configuration, or publication. Examples include:

- Cross-site scripting or unsafe HTML rendering caused by repository content, templates, Markdown processing, or site generation.
- Unsafe URL handling that enables script execution, deceptive navigation, or another demonstrable security impact in project-controlled pages.
- Unauthorized modification of catalog content or published artifacts.
- Exposure of passwords, access tokens, private keys, deployment credentials, or other non-public information in repository files, history, generated output, or build logs.
- A compromised or vulnerable Jekyll theme, plugin, or other build dependency with a demonstrable impact on this project's build or output.
- Unsafe handling of untrusted contributions that could expose privileged build credentials or modify a deployment, if such automation is introduced or configured.
- A project-controlled custom-domain or publication configuration that creates a demonstrable takeover risk.
- Malicious catalog entries or links introduced into project-controlled content, especially when they could mislead visitors into downloading harmful files or disclosing credentials.
- A parsing or data-integrity flaw in project-owned catalog processing, if present, that crosses a trust boundary or produces a demonstrable security impact.

A static site can still have security problems. The absence of a backend does not make injected scripts, compromised dependencies, exposed secrets, or publication tampering harmless.

### 3.2. Findings that usually belong elsewhere

The following generally are not project vulnerabilities on their own:

- Ordinary catalog inaccuracies, broken links, spelling errors, or display problems without a security impact.
- A vulnerability in a third-party game, store, launcher, download server, or external website merely referenced by the catalog.
- A vulnerability in GitHub, GitHub Pages, a DNS provider, or another hosting platform that is not caused by project-controlled configuration.
- A generic scanner result, dependency version match, or missing security header without evidence of an applicable attack and an affected trust boundary.
- A hypothetical attack that requires an attacker to already possess the same level of administrative control needed to cause the claimed impact, unless it demonstrates a separate privilege boundary failure.
- Public information that was intentionally published and is not confidential, such as public repository metadata or a deliberately public catalog entry.
- Duplicate reports of the same underlying issue without additional impact or new evidence.

These categories are triage guidance, not a reason to dismiss a demonstrated impact. If you are unsure, explain the affected boundary and why the finding matters. Non-security improvements can use the normal contribution process without including sensitive vulnerability details.

## 4. Reporting a Vulnerability

### 4.1. Preferred route: GitHub private vulnerability reporting

1. Open the repository's [Security page](https://github.com/YuStellarGamesStudio/GameCatalog/security).
2. If **Report a vulnerability** is available, use it to submit a private report.
3. Include the information listed in Section 5 and continue coordination in the private report.
4. Keep exploit details and attachments private until disclosure is coordinated.

GitHub private vulnerability reporting must be enabled separately by repository administrators. **Adding this file does not enable that feature.** This policy does not assert that the reporting button is currently available.

See [GitHub's private vulnerability reporting instructions](https://docs.github.com/en/code-security/how-tos/report-and-fix-vulnerabilities/report-privately) for the platform's current workflow and access requirements.

### 4.2. If private reporting is unavailable

This repository does not currently publish a dedicated security email address or an encryption key in this policy. Do not guess an address, assume an organization member's personal account is an approved security channel, or send sensitive material to an unverified recipient.

If the private reporting button is unavailable:

1. Use a security contact explicitly published by the repository maintainers, if one becomes available, and verify that it applies to this repository.
2. Otherwise, if repository issues are available, open a minimal contact request asking for a private reporting channel. Do not include the affected component, exploit, credentials, sensitive screenshots, or other details that would reveal the vulnerability.
3. Wait for a maintainer to identify an appropriate private channel. Verify the responder's repository role and the destination before sending sensitive information.
4. If issues are unavailable, use a contact method explicitly published by the organization only to request a private security channel; do not submit the vulnerability details until that channel has been verified.

A suitable public contact request is:

> I would like to report a potential security issue privately. Please provide a private reporting channel for this repository or enable GitHub private vulnerability reporting. I will not publish technical details here.

A public contact request is **not** a private vulnerability report. Do not attach a proof of concept to it or turn a lack of response into an accidental public disclosure.

### 4.3. Urgent exposure or active exploitation

For suspected active exploitation, exposed credentials, or deployment compromise, mark the private report as urgent and explain the immediate risk. Describe the affected location and discovery time without using or reproducing the secret unnecessarily.

Do not use an exposed credential to validate its permissions, access another account, or attempt a repair. Credential revocation and incident containment must be performed by the authorized owner.

This repository does not provide an emergency response hotline or a guaranteed continuously monitored reporting channel.

## 5. Information to Include

A useful report should include as much of the following as you can provide safely:

- **Summary:** A concise description of the weakness and its security impact.
- **Affected location:** Repository path, URL, configuration, template, dependency, or publication stage.
- **Affected revision:** Commit SHA, branch, release identifier if applicable, or the date and time the deployment was observed.
- **Environment:** Relevant browser, operating system, Jekyll/build environment, dependency versions, and configuration.
- **Prerequisites:** Required access level, attacker-controlled inputs, user interaction, and any non-default settings.
- **Reproduction steps:** Minimal, deterministic steps performed locally or in an environment you are authorized to test.
- **Observed result:** What happened, with appropriately redacted evidence.
- **Expected result:** Which security boundary or protection should have prevented the behavior.
- **Impact:** What an attacker can obtain or change, which users or systems are affected, and the limits of the attack.
- **Proof of concept:** The smallest safe example necessary to demonstrate the issue. Prefer harmless local demonstrations rather than weaponized payloads.
- **Mitigation or fix ideas:** Optional suggestions, including known limitations or compatibility concerns.
- **Disclosure status:** Whether the issue has been shared elsewhere, has an existing advisory, or is believed to be actively exploited.
- **Follow-up preference:** How you can be reached through the verified private channel and whether you want public credit.

A severity assessment or CVSS vector is welcome, but not required. State the assumptions behind your assessment. Do not delay a credible report merely because you cannot determine the complete impact or implement a fix.

### Private report template

Use this template only in a verified private reporting channel:

```text
Title:

Summary:

Affected repository paths or deployment URLs:
Affected commit, version, or observation time:
Environment and relevant configuration:

Attacker capabilities and prerequisites:
Steps to reproduce safely:
1.
2.
3.

Observed result:
Expected security boundary:
Security impact and limitations:

Redacted evidence or minimal proof of concept:
Suggested mitigation, if known:
Known upstream advisories, if applicable:
Active exploitation or credential exposure, if known:
Previous or planned disclosure:
Preferred attribution name, or request for no public credit:
```

## 6. Evidence and Sensitive Data

Collect only the evidence necessary to demonstrate the finding.

- Redact tokens, private keys, passwords, session identifiers, personal information, and unrelated data from screenshots, logs, and attachments.
- For an exposed secret, provide its location and type rather than its complete value. A short redacted identifier may be sufficient to distinguish it.
- Do not include authentication headers, browser cookies, or environment dumps containing credentials.
- Do not upload sensitive evidence to public paste services, public forks, or publicly accessible file-sharing links.
- Do not commit an exploit or a leaked secret to repository history as part of a report.
- If you unexpectedly encounter non-public data, stop accessing it and report the circumstances. Do not enumerate, download, or retain more of it to prove impact.
- Keep report access limited to people who need it for investigation and remediation.

Private reporting reduces public exposure; it is not a promise that only one person will see the report. Repository administrators, authorized collaborators, and the reporting platform may have access according to their roles and platform rules. Supply no more sensitive information than necessary.

## 7. Responsible Research Boundaries

Prefer source review, a local clone, local Jekyll builds, and isolated test data. Use synthetic credentials and records for demonstrations.

This policy provides reporting guidance. **It does not authorize penetration testing of production systems, third-party services, other accounts, or infrastructure outside your control.** Obtain explicit permission from the relevant owner before testing anything that requires it.

Do not:

- Perform denial-of-service, load, resource-exhaustion, or high-volume scanning against the published site or hosting infrastructure.
- Attempt to compromise maintainer accounts, bypass GitHub permissions, or access private repositories.
- Use social engineering, phishing, credential stuffing, malware, or physical intrusion.
- Exploit exposed credentials or access information belonging to other people.
- Modify or delete production content, publish a malicious catalog entry, or alter a live deployment to demonstrate control.
- Register or take over a suspected dangling custom domain, provision a competing hosted site, or change DNS without authorization.
- Run a suspected malicious dependency on a machine containing valuable credentials or sensitive data.
- Continue exploitation after obtaining the minimum evidence necessary to establish the issue.
- Test third-party games, stores, or services on the assumption that inclusion in the catalog grants permission.

If demonstrating a finding would exceed these boundaries, report the evidence you already have and ask maintainers to arrange a safe validation method.

## 8. Triage and Remediation

The intended handling process is:

1. **Acknowledge and clarify:** Establish a private discussion and request missing information when necessary.
2. **Validate:** Reproduce the issue in an appropriate environment, identify the affected boundary, and determine whether the project controls the vulnerable component.
3. **Assess impact:** Consider exploitability, required privileges, affected users, exposed information, and any evidence of active exploitation.
4. **Contain urgent risks:** Where applicable, coordinate removal of harmful published content, credential revocation, access restriction, or temporary suspension of an affected publication path.
5. **Prepare remediation:** Fix the underlying issue, assess whether dependencies or configuration need changes, and check related affected paths.
6. **Verify:** Confirm that the reported attack is blocked without unnecessarily breaking legitimate use.
7. **Publish and communicate:** Coordinate deployment, downstream guidance, attribution, and any appropriate advisory.

Depending on the finding, a report may be accepted, require more evidence, be identified as a duplicate, be referred upstream, or be determined not to represent a security vulnerability. A useful resolution should explain the relevant reasoning without exposing sensitive material.

This policy does not promise a fixed acknowledgment, resolution, or disclosure deadline. It does not establish a 24/7 incident response service. Timing depends on severity, reproducibility, maintainer availability, deployment constraints, and upstream coordination. Any specific timeline should be agreed in the private discussion rather than inferred from this document.

If a report is awaiting a response, follow up in the same private channel instead of opening repeated public issues. If that channel is unavailable, use a non-sensitive contact request as described in Section 4.2.

## 9. Severity Considerations

Severity is assessed using the actual impact and environment, not solely a scanner label or theoretical worst case.

Important considerations include:

- Whether an unauthenticated attacker can trigger the behavior.
- Whether a normal visitor, contributor, or privileged maintainer must interact with malicious content.
- Whether arbitrary script execution, credential disclosure, or unauthorized publication is possible.
- Whether the issue affects one page, a specific build, all catalog output, or independent consumers.
- Whether the vulnerable dependency is actually loaded and its vulnerable functionality is reachable.
- Whether existing configuration prevents exploitation or merely makes it less convenient.
- Whether exploitation is reproducible and whether it is occurring in practice.

Credential compromise, malicious publication, and confirmed visitor-facing script execution may require immediate containment. A version-only dependency alert or a hardening suggestion may require further investigation before its practical severity is known.

## 10. Coordinated Disclosure and Advisories

The preferred approach is coordinated disclosure that gives maintainers a reasonable opportunity to investigate, contain, and remediate the issue while keeping reporters informed through the private channel.

- Discuss a disclosure plan privately before publishing exploit details.
- Agree on what can be published, when it can be published, and which details must remain redacted.
- Avoid publishing sensitive information even after the vulnerability has been fixed.
- Account for deployments and downstream consumers that may need time to apply an update.
- Coordinate with upstream maintainers when a theme, plugin, hosting platform, or other external component is involved.
- If a mutually agreed timeline becomes impractical, discuss the reason and a revised plan rather than assuming indefinite secrecy or an automatic publication date.

Where appropriate, maintainers may publish a GitHub Security Advisory describing affected revisions, impact, mitigation, and fixed revisions. A CVE identifier may be considered when applicable; neither an advisory nor a CVE is guaranteed for every report.

Published advisories, if any, can be found on the repository's [Security Advisories page](https://github.com/YuStellarGamesStudio/GameCatalog/security/advisories).

### Attribution and rewards

Reporters may request public credit or request that no public credit be given. Confirm the desired display name and link privately before publication. Do not assume that a private platform account is anonymous to repository administrators.

This policy does not establish a paid bug bounty, compensation arrangement, merchandise reward, or other entitlement. Any separate reward program would require its own explicit terms.

## 11. Dependency and Publication Security

The Jekyll configuration selects `jekyll-theme-tactile` and the `jekyll-readme-index` plugin. Reports involving these components should identify the actual version used in the affected build, the vulnerable behavior, and whether the project's configuration makes that behavior reachable. Configuration names alone are not proof of a vulnerability.

For maintainers and contributors, the following practices reduce publication risk:

- Review themes, plugins, templates, and dependency changes for their effect on both build execution and generated content.
- Do not assume that Markdown, catalog fields, or external links are safe merely because they are stored as text.
- Treat build-time plugins and dependency installation as code execution, not as passive content processing.
- Keep private configuration, credentials, and internal artifacts out of generated public output.
- If automation is added, use narrowly scoped permissions and prevent untrusted contribution code from receiving publication credentials.
- Review changes to the configured domain, publication source, and deployment permissions as security-sensitive changes.
- Avoid placing executable payloads or live malicious URLs in public regression fixtures when a harmless equivalent demonstrates the boundary.
- Do not assume a security scanner, branch protection rule, or deployment control exists unless it has actually been configured and verified.

These are security practices and review guidance, not a claim that particular scanners, automated checks, or access controls are enabled on this repository.

## 12. Guidance for Catalog Users and Self-Hosters

Catalog content and external links should be treated as information, not as an unconditional endorsement of the security of a game, store, or download.

- Check a destination before submitting credentials or downloading executable files.
- Prefer official publisher and store sources, and independently verify software authenticity where appropriate.
- Do not execute catalog fields, interpolate them into commands, or render them as trusted HTML without appropriate handling.
- Apply security fixes to the source, rebuild your site, and update deployed artifacts when self-hosting.
- Review your own dependency versions, domain configuration, permissions, and hosting settings; this project's policy does not administer your deployment.
- If a malicious link or compromised entry appears in project-controlled content, report its location privately. Do not investigate the suspected malicious destination by entering real credentials or running its downloads.

Removing an exposed secret from the current file does not invalidate copies in Git history, caches, logs, forks, or downloads. The owner must revoke or rotate the credential; content removal alone is not a complete remedy.

## 13. Policy Limitations and Updates

This policy is not a certification that the repository or its dependencies are vulnerability-free. It does not expand the permissions granted by the project license, grant legal immunity, bind third-party service providers, or authorize activity prohibited by applicable law or platform terms.

The policy may be updated when reporting channels, project architecture, deployment arrangements, or supported versions change. Use the version on the current `main` branch for current reporting guidance. If an older copy contains a different contact method, verify the current method before sending sensitive information.

Thank you for helping protect the integrity of GameCatalog and the people who use its content.
