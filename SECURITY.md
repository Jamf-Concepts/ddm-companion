# Security Policy

DDM Companion is a native macOS app for Jamf Pro administrators that authenticates to a Jamf Pro instance using OAuth 2.0 Client Credentials stored in the macOS Keychain, then surfaces DDM fleet health and issues commands — DDM sync, software update deployments, and inventory updates — on behalf of the signed-in admin. Vulnerabilities in how the app stores or transmits credentials, or in how it authorizes commands against a managed fleet, are taken seriously.

For Jamf Concepts' broader security posture, see **[concepts.jamf.com/en/security](https://concepts.jamf.com/en/security/)**.

## Supported versions

Security fixes are applied to the latest released version. Please make sure you can reproduce an issue on the most recent release before reporting it.

## Reporting a vulnerability

**Please do not open a public GitHub issue for security vulnerabilities.**

Instead, report privately using one of:

- Jamf's [Vulnerability Disclosure Program](https://www.jamf.com/trust-center/vulnerability-disclosure/), or
- The **Report a vulnerability** button under this repository's **Security** tab.

Please include:

- A description of the issue and its potential impact.
- Steps to reproduce, or a proof of concept.
- The DDM Companion version, macOS version, and Jamf Pro version you observed it on.

You can expect an initial acknowledgement within a few business days. Once a fix is available, the report will be disclosed publicly with credit to the reporter, unless you ask to remain anonymous.

## Scope

In-scope examples: mishandling or leakage of OAuth credentials or tokens (Keychain storage, disk writes, or logging), insecure HTTPS communication (certificate validation bypasses or plaintext fallback), unauthorized command dispatch (DDM sync, software update push, blank MDM push) without explicit admin intent, or privilege escalation within the app itself.

Out of scope: vulnerabilities in Jamf Pro, the Jamf Pro REST API, macOS, or the system Keychain. Please report those to the relevant vendor. Issues stemming from an admin's own API Client configuration (overly broad privileges, shared credentials) are also out of scope.
