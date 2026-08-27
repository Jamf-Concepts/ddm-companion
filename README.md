# DDM Companion

A native macOS utility for Jamf Pro administrators who manage Apple devices
with Declarative Device Management (DDM). It gives you a focused view of
your fleet's DDM health and lets you trigger DDM syncs, software update
deployments, and inventory updates as a companion to Jamf Pro.

Jamf Pro's DDM support continues to evolve, and DDM status information —
per-device software update state, declaration activation status, Blueprint
coverage — is available through the Jamf Pro API but spread across multiple
endpoints and not always surfaced prominently in the console UI.
DDM Companion brings that data together in one place so admins can spot
devices that are stale, unmanaged, or stuck on a pending update without
navigating individual device records or running manual API queries.

This app connects to your own Jamf Pro instance using OAuth 2.0 Client
Credentials. Credentials are stored exclusively in the macOS system Keychain
— never in the app bundle or on disk elsewhere. All communication uses the
Jamf Pro REST API over HTTPS.

DDM Companion is a [Jamf Concepts](https://resources.jamf.com/documents/jamf-concept-projects-use-agreement.pdf) app.

## The Gap It Fills

- **Fleet Dashboard** — at-a-glance DDM adoption, supervision, and software
  update compliance across all Macs and mobile devices. Tap a device for a
  detail panel with per-device actions (Force DDM Sync, Update Inventory).
- **Software Updates** — per-device update state (Up to Date, Pending,
  Installing, Failed) pulled live from the DDM status API.
- **Device Inspector** — drill into any device's full DDM status item tree
  and active declarations.
- **Blueprint Coverage** — see which devices have scoped declarations.
- **Best Practices** — built-in reference guide covering enrollment,
  bootstrap tokens, network requirements, and common pitfalls.

## Requirements

- macOS 15.7 or later
- A Jamf Pro instance and a Jamf Pro API Client (Client ID + Client Secret)
  scoped per [Required API Permissions](#required-api-permissions) below

## Installation

1. Download the `.pkg` from Jamf Concepts.
2. Launch DDM Companion.
3. On first launch, enter your Jamf Pro instance URL, Client ID, and Client
   Secret in the Connect screen. Credentials are saved to the macOS
   Keychain for subsequent launches.

## Usage

1. Connect to your Jamf Pro instance (see Installation above).
2. Use the sidebar to move between the Fleet Dashboard, Software Updates,
   Device Inspector, Blueprint Coverage, and Best Practices views.
3. From the Fleet Dashboard, tap any device for a detail panel with
   per-device actions: Force DDM Sync, Push Update, and Update Inventory.
4. Use **Export CSV** or **Report** (top of the Fleet Dashboard) to save a
   snapshot of fleet data for sharing outside the app.
5. Enable notifications in Settings (⌘,) to be alerted when fleet health
   drops, stale devices are detected, or software update compliance changes
   significantly.

## Required API Permissions

Create a Jamf Pro API Role with only the privileges below,
and assign it to an API Client to be used by this app.

- Read Computers
- Read Mobile Devices
- Read Declarative Device Management
- Send Declarative Device Management Commands
- Send Managed Software Update Commands
- Send MDM Commands (Blank Push)
- Read and Update Computer Groups (Static)

## Troubleshooting

- **"Not Connected"** — check that your instance URL, Client ID, and Client
  Secret are correct, and that the API Client has the privileges listed
  above. Authentication failures surface a status message in the Connect
  screen describing the specific error.
- **Notifications never appear** — macOS notification permission may have
  been denied. Open **System Settings → Notifications** and enable
  DDM Companion, or use the "Open" link shown in Settings (⌘,) when
  permission is blocked.
- **No software update data for some devices** — the device's Blueprint
  must include a Software Update Enforcement declaration
  (`com.apple.configuration.softwareupdate.enforcement.specific`). Without
  it, `softwareupdate.install-state` and related keys are absent from DDM
  status. See the in-app Best Practices guide for setup details.
- **Update Inventory does nothing on a Mac** — the Recon Group workflow
  requires a Static Computer Group and a scoped Policy configured in Jamf
  Pro first. See the in-app Best Practices guide ("Mac Inventory Update")
  for the two-step setup.
- **DDM sync/enforcement fails with `SUMacControllerError Code=7507`** — the
  device's bootstrap token isn't escrowed with Jamf Pro. See the in-app Best
  Practices guide ("Bootstrap Token") for the escrow steps.

### Logging

If something's not working, open **Console.app** (Applications → Utilities),
select your Mac under Devices, and search for `com.jamf.concepts.ddmcompanion`
to see DDM Companion's log messages.

To pull the last hour of logs in Terminal:

```
log show --predicate 'subsystem == "com.jamf.concepts.ddmcompanion"' --last 1h
```

## Sharing Feedback

We welcome your feedback. Please send messages to the project developers via
[GitHub Issues](https://github.com/Jamf-Concepts/ddm-companion/issues).

## License

This project is used under the [Jamf Concepts Use Agreement](https://resources.jamf.com/documents/jamf-concept-projects-use-agreement.pdf).

## Privacy and Security

Please see Jamf's [Privacy Policy](https://www.jamf.com/trust-center/privacy/privacy-policy/) for information about our data policies.

Information security is a team effort. If you discover a security
vulnerability in our software, please report it via [Jamf's Vulnerability Disclosure Program](https://www.jamf.com/security/vulnerability-disclosure/).

---

Copyright 2026, Jamf Software LLC
