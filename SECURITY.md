# Security policy

## Reporting a problem

**Report it privately, not in an issue.** On the repository it concerns, use
GitHub's private vulnerability reporting — **Security → Report a
vulnerability**. Where a repository does not offer it, or the problem is in
the hub itself, use the contact form at <https://pcfhub.dev/contact>: say that
it is a security report and how to reach you, and leave the details out until
someone replies.

Please include what an attacker could do, the steps to reproduce it, and the
versions or URLs involved. We will acknowledge the report, keep you told what
we found, and credit you when the fix ships unless you would rather we did not.

## What is in scope

- **pcfhub.dev** — the site, its public API at `/api/v1`, the MCP server at
  `/mcp`, and the demo harness that runs controls in the browser.
- **[`_template`](https://github.com/pcfhub/_template)** — its scripts and the
  shared release and build workflows every control repository calls.
- **[`pcfhub-controls-skill`](https://github.com/pcfhub/pcfhub-controls-skill)**
  — anything a skill tells an assistant to run or install.
- **The control repositories** in this organisation, at their latest release.

A control published by someone outside this organisation belongs to its own
repository: report it there, and tell us through the contact form if it is
listed on the hub, so the listing can be reviewed.

## Versions

The hub is deployed continuously, so only what is live is supported. For the
template, the skills and each control, the latest release is.
