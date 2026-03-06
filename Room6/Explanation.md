# Natas — Level 5

**URL:** http://natas5.natas.labs.overthewire.org  
**Username:** `natas5`  
**Password:** `0n35PkggAPm2zbEpOU802c0x0Msn1ToK`

---

## Goal
Find the password for the next level.

---

## Solution

Upon accessing the page, the following message is displayed:

> *"Access disallowed. You are not logged in"*

Inspecting the cookies (browser devtools → **Storage** tab → **Cookies**, or `F12` → **Application** tab in Chrome) reveals:

```
loggedin = 0
```

The server is using a cookie to determine if the user is authenticated. Since the value is `0` (false), access is denied. Simply change it to `1`:

1. Open devtools → **Storage** → **Cookies**
2. Find the `loggedin` cookie
3. Change the value from `0` to `1`
4. Refresh the page — access is granted and the password is revealed

### Using cURL

```bash
curl -u natas5:0n35PkggAPm2zbEpOU802c0x0Msn1ToK \
  -b 'loggedin=1' \
  http://natas5.natas.labs.overthewire.org/
```

---

## Concept
> **Never trust client-side values for authentication or access control.** Cookies are fully controlled by the user and can be modified freely. Authentication state must always be validated server-side — a cookie should store a session ID that the server verifies, never a plain boolean like `loggedin=1`.
