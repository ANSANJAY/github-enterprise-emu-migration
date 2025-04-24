# Task 6: Request EMU Enablement

## Objective

Initiate the process of enabling GitHub Enterprise Managed Users (EMU) for the enterprise account. This is the first formal step toward enforcing centralized identity through a supported Identity Provider (IdP) and transitioning the organization into a managed environment.

---

## Prerequisites

Before submitting the request to GitHub Support or Account Team, ensure the following are prepared:

| Requirement                           | Status    |
|--------------------------------------|-----------|
| GitHub Enterprise Cloud subscription | Active    |
| Verified domain                      | emulabsdemo.com (simulated) |
| Enterprise admin access              | test1emu_admin (confirmed)  |
| Chosen IdP                           | Custom (simulated) or Okta  |

---

## Step-by-Step: EMU Request Process

### 1. Log In as Enterprise Owner

Access:
```
https://github.com/enterprises/emu-testing
```

Ensure you’re logged in as `test1emu_admin`.

---

### 2. Navigate to Enterprise Settings → Authentication Security

```
https://github.com/enterprises/emu-testing/settings/authentication
```

This page provides the UI to initiate SAML/SCIM configuration or download metadata to send to your IdP.

---

### 3. Submit Request to GitHub Support


## Outcome

The simulation assumes EMU features were approved, and identity enforcement via SAML and SCIM is now permitted.

You may now proceed to configure your IdP and enforce SSO.

