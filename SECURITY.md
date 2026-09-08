# Security Policy

This file is the organisation default. It applies to every Log10x repository
that does not carry its own.

## Reporting a vulnerability

**Email `security@log10x.com`.** It reaches the person who can act on it.

You can also use **GitHub private vulnerability reporting** on any public
repository here, through the Security tab. Both routes reach the same place.

Reports are accepted from anyone, including anonymously. You do not need an
account, a prior relationship, or permission to look.

The same address is published in
[`security.txt`](https://www.log10x.com/.well-known/security.txt), and the full
policy it points at is at
[doc.log10x.com/security](https://doc.log10x.com/security/).

## What to expect

| | |
|---|---|
| First response | Within **24 hours** |
| Remediation target, CVSS 9.0 and above | **48 hours** |
| Remediation target, everything else | **30 days** |

These are the commitments already published on the security page rather than
new ones written for this file. If we miss one, say so in the thread.

## What is most useful to report

Anything affecting a released artifact carries the most weight, because those
run on other people's infrastructure:

- The container images on Docker Hub and ghcr.io
- The engine binaries, packages and installers on `pipeline-releases`
- The Helm charts
- The `log10x-mcp` npm package
- The public `tenx-receive` Lambda layers

Also: the licensing and account API, the console, and anything that would let
one customer see another customer's data.

## What we ask

Give us a reasonable chance to fix it before publishing. We will not take legal
action against anyone who reports in good faith, does not access or modify data
belonging to others, and does not degrade the service for anyone else.

There is no bug bounty. We will credit you if you want to be credited.

## Scope note, stated plainly

Log10x is a small company. There is no security team and no 24/7 rota. The
response commitments above are what one person can actually meet, which is why
they are what they are rather than something more impressive.
