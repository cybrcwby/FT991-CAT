# FT991-CAT: current status and clearance

Review date: 2026-10-18 UTC. Public-safe proposed documentation. No publication or deployment authorized.

## Evidence baseline

- Public fork of m0lit/FT991-CAT.
- Master: [414afede83d90d557671b9257f23010ccb658172](https://github.com/cybrcwby/FT991-CAT/commit/414afede83d90d557671b9257f23010ccb658172), 2018-06-06.
- No issues or PRs returned during review. This was source inspection, not an assessment of a running installation or connected radio.

## Established findings

The repository is a legacy PHP/Python CAT-control example. It is not cleared by this review for current deployment.

- CAT-01: [php/ft991a.php](https://github.com/cybrcwby/FT991-CAT/blob/414afede83d90d557671b9257f23010ccb658172/php/ft991a.php) concatenates the GET parameter par into a shell command invoking sudo python. This is an unsafe command-injection pattern.
- CAT-02: [php/README.txt](https://github.com/cybrcwby/FT991-CAT/blob/414afede83d90d557671b9257f23010ccb658172/php/README.txt) recommends broad passwordless sudo for a web-service identity. Its historical example also has malformed identity/rule text; correcting the syntax would not resolve the excessive-privilege design.
- CAT-03: inspected reboot/shutdown PHP handlers invoke privileged system commands without an application authorization check in those handlers. No claim is made about external controls or exposure of any deployment.
- CAT-04: setup guidance targets an old runtime/layout. Present compatibility, archive/source correspondence and deployment suitability were not established.

## Clearance conditions

Before deployment, replace shell-string handling with strictly allowed commands and validated arguments; remove broad web-service sudo; establish narrowly scoped privilege boundaries and authenticated/authorized management; and test rejection paths. Review supported runtime/dependencies and archive provenance in isolation. Assess radio-command and PTT behavior without transmitting.

These are source-level findings. They do not establish that an exposed vulnerable instance exists. A future security/functional review must cover more than the inspected entry points.

## Deferred decision and closure

Reference-only retention is valid. Modernization requires an explicitly approved scope, not simply the age of the fork. A reference-only decision can close planning while deployment remains unapproved. Operational clearance requires reviewed remediation and tests, not documentation alone.

## Minimal update

Add a public-safe legacy/security warning and a relative link to this document in README. Preserve upstream attribution. Do not add private infrastructure details or private station-document links to this public fork.
