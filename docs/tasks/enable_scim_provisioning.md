# Task 8: Enable SCIM Provisioning

## Objective

Simulate the configuration of SCIM (System for Cross-domain Identity Management) to automate user provisioning and de-provisioning for GitHub Enterprise Managed Users (EMU). SCIM ensures centralized lifecycle control of user accounts via an Identity Provider (IdP) such as Okta or Azure AD.

---

## Prerequisites

| Requirement                  | Status    |
|-----------------------------|-----------|
| SAML SSO Configured         | Completed (Simulated) |
| Domain Verified             | `emulabsdemo.com` (Simulated) |
| GitHub Enterprise Admin     | `test1emu_admin` |
| IdP SCIM Client Available   | Simulated Okta Interface |

---

## Step-by-Step: Simulated SCIM Configuration

### 1. Access SCIM Settings in GitHub

Navigate to:

```
https://github.com/enterprises/emu-testing/settings/authentication
```

Scroll to the **SCIM provisioning** section.

---

### 2. Copy GitHub SCIM Endpoint and Token

In a real environment, GitHub provides:

- **SCIM Base URL:**
  ```
  https://api.github.com/scim/v2/enterprises/emu-testing
  ```

- **Bearer Token:**
  ```
  <secret-token>
  ```

These values are pasted into your IdP's SCIM client.

---

### 3. Simulate IdP-Side Configuration (Okta Example)

Using Okta Developer Console:

- Go to **Applications > SCIM > Provisioning**
- Enter:
  - SCIM Base URL
  - Bearer Token
- Enable:
  - Create Users
  - Deactivate Users
  - Push Groups

> Note: This was not connected live. Configuration was simulated using documented values only.

---

## Example: SCIM Provisioning JSON (Simulated)

```json
{
  "userName": "johnsmith@emulabsdemo.com",
  "name": {
    "givenName": "John",
    "familyName": "Smith"
  },
  "emails": [
    {
      "value": "johnsmith@emulabsdemo.com",
      "primary": true
    }
  ],
  "externalId": "johnsmith"
}
```

---

## SCIM Simulation Outcome

| Feature                | Status        | Notes                                  |
|------------------------|---------------|-----------------------------------------|
| Auto User Creation     | Simulated     | Mapped in identity_mapping.csv          |
| Group Membership       | Simulated     | Using GitHub Teams                      |
| Deprovisioning Logic   | Documented    | Not live — simulated via role removal   |
| Real-Time Sync         | Not connected | Covered in documentation only           |

---

## Notes

- User provisioning/de-provisioning was simulated through CLI-based team assignments.
- Actual SCIM implementation would require a real IdP and verified production domain.

---
