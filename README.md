<div align="center">

# PPPC Analyser

**Build a PPPC profile from any Mac app.**

Drop in an app and PPPC Analyser finds the privacy permissions it asks for. It then saves a
Privacy Preferences Policy Control (PPPC) configuration profile, ready to upload to your MDM.

[mdmmagic.au](https://mdmmagic.au)

</div>

---

## Download

Download the latest `.pkg` from **[Releases](https://github.com/MDMMagic/PPPC-Analyser/releases/latest)**
and open it to install. The installer puts **PPPC Analyser** in `/Applications`.

This repository only hosts the installer. The source code isn't published.

## Requirements

- macOS 15 (Sequoia) or later

---

## How to use it

1. **Set your organisation.** On the home screen, enter the name to show as the organisation on
   saved profiles. The app remembers it between launches. Leave it blank to leave it out of the
   profile.
2. **Add the app.** Drag a `.app` onto the window, or click **Choose App…**.
3. **Review the permissions.** PPPC Analyser reads the app's `Info.plist` usage descriptions and its
   code-signing entitlements, then lists the permissions it found:
   - **Likely**: the app declares that it uses the permission. These are ticked by default.
   - **Possible**: weaker hints. These are left unticked for you to decide.
4. **Choose what to grant.** Tick the permissions to include and set each one to **Allow**,
   **Deny** or **User Can Allow**.
5. **Save Profile…** writes a `.mobileconfig` that you can upload to your MDM and scope as normal.

The app's bundle ID and code requirement are read from its signature automatically.

---

## Things worth knowing

**Camera, Microphone, Screen Recording and Input Monitoring can't be pre-approved.** macOS doesn't
let MDM grant these silently, so the only settings offered for them are **Deny** and, for Screen
Recording and Input Monitoring, **User Can Allow**. User Can Allow lets a standard user approve the
permission themselves. PPPC Analyser warns you before you save a Deny for any of these, because a
Deny stops users from ever granting it. For a conferencing app such as Zoom or Teams, that breaks
calls and screen sharing.

**Apple Events needs a receiver.** If you include Apple Events, choose the app being controlled,
such as Finder or System Events. Click **Choose App…** next to the receiver fields to fill in its
bundle ID and code requirement.

**Unsigned apps need a code requirement.** An unsigned app has no designated requirement, and macOS
rejects PPPC entries without a valid one. Enter the requirement yourself. For an in-house tool, you
can instead use the identifier-only option, but it is weaker: any app that claims that bundle ID
will match.

**Full Disk Access is never suggested.** An app can't declare that it needs Full Disk Access, so
PPPC Analyser never proposes it. Add it in your MDM if the app needs it.

**Re-saving the same app gives the same profile.** The profile's identifiers come from the app, so
uploading a new copy replaces the earlier profile on devices instead of adding a second one.

---

## Privacy

PPPC Analyser runs sandboxed and makes no network connections. It reads only the app you choose
and writes only the profile you save.

---

## Uninstall

Drag **PPPC Analyser** from `/Applications` to the Bin.

---

<div align="center">

**MDM Magic** · [mdmmagic.au](https://mdmmagic.au)

</div>
