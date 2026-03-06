# OverTheWire — Natas

> **URL:** http://natas.labs.overthewire.org  
> **Type:** Web Security  
> **Focus:** Server-side web security fundamentals

---

## Level 0

**URL:** http://natas0.natas.labs.overthewire.org  
**Username:** `natas0`  
**Password:** `natas0`

### Goal
Find the password for the next level.

### Solution

Upon accessing the page, the following message is displayed:

> *"You can find the password for the next level on this page."*

The password is hidden in plain text inside the **page source code**. To find it, open the browser inspector:

- **Chrome/Firefox:** `F12` → **Elements** tab (or `CTRL+U` to view the raw source directly)
- Look for an HTML comment `<!--`

```html
<!--The password for natas1 is <PASSWORD> -->
```

### Concept
> Never store sensitive information in HTML source code — any user can view the page source without any special tools.
