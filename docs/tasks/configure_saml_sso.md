# Task 7: Configure SAML Single Sign-On (SSO)

## Objective

Simulate the configuration of SAML-based Single Sign-On (SSO) to enforce centralized authentication for GitHub Enterprise Managed Users (EMU). This task outlines the metadata exchange between GitHub and the Identity Provider (IdP), simulating an enterprise SSO enforcement policy.

---

## Environment Context

- Enterprise Account: `emu-testing`
- Simulated IdP: `idp.emulabs.com` (Custom/Okta)
- Admin Username: `test1emu_admin`
- GitHub SSO URL (Simulated): `https://github.com/enterprises/emu-testing/settings/authentication`

---

## Step-by-Step: Simulated SAML Configuration

### 1. Prepare IdP Metadata (Simulated Example)

A real IdP (e.g., Okta, Azure AD) would provide a metadata file like:

```xml
<EntityDescriptor entityID="https://idp.emulabs.com"
                  xmlns="urn:oasis:names:tc:SAML:2.0:metadata">
  <IDPSSODescriptor>
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect"
                         Location="https://idp.emulabs.com/sso"/>
  </IDPSSODescriptor>
</EntityDescriptor>
```

---

### 2. GitHub Configuration (Manual Entry for Simulation)

Fields entered in GitHub Enterprise Authentication settings:

| Field              | Value                                      |
|--------------------|--------------------------------------------|
| Sign on URL        | `https://idp.emulabs.com/sso`              |
| Issuer             | `https://idp.emulabs.com`                  |
| Public Certificate | Simulated X.509 certificate                |

**Public Certificate:**
(Paste simulated or test X.509 PEM-encoded certificate)

---

### 3. Save and Test Configuration

**Test Output (Simulated CLI Interaction):**

```bash
Test initiated... failed
Reason: Cannot contact IdP
```

**Note:** This failure is expected in simulation mode. You may bypass testing to complete the configuration visually.

---

### 4. Enforce SSO for All Users (Simulated)

In a real environment, you would then:
- Enforce SSO for all members
- Restrict logins to SAML-authenticated identities only
- Provide IdP-administered recovery methods

**Simulated Setting Enabled:**

```bash
All users must authenticate through SAML-based SSO
```

---

## What Was Simulated

- Manual entry of SAML SSO metadata
- Bypassed IdP validation due to demo environment
- GitHub now "thinks" SAML is enabled

---

