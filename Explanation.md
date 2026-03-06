# OverTheWire — Natas

> **URL:** http://natas.labs.overthewire.org  
> **Type:** Web Security  
> **Focus:** Server-side web security fundamentals

---

## Level 1

**URL:** http://natas1.natas.labs.overthewire.org  
**Username:** `natas1`  
**Password:** `0nzCigAq7t2iALyvU9xcHlYN4MlkIwlq`

### Goal
Find the password for the next level.

### Solution

Same as Level 0, the password is hidden in the page source code. However, this time **right-click is blocked** via JavaScript.

Right-click being disabled is purely a client-side restriction and can be bypassed in several ways:

- **Keyboard shortcut:** `CTRL+U` — opens the raw page source directly in a new tab, bypassing the right-click block entirely
- **F12** → **Elements** tab — browser devtools are never blocked by the page
- **Address bar:** type `view-source:http://natas1.natas.labs.overthewire.org` manually

Once in the source, look for the HTML comment:

```html
<!--The password for natas2 is <PASSWORD> -->
```

### Concept
> Blocking right-click is a **client-side control** — it only affects the mouse event and can always be bypassed using keyboard shortcuts or browser built-in tools. It provides zero security and should never be relied upon to hide sensitive information.
