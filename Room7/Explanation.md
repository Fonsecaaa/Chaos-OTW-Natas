# Natas — Level 6

**URL:** http://natas6.natas.labs.overthewire.org  
**Username:** `natas6`  
**Password:** `0RoJwHdSKWFTYR5WuiAewauSuNaBXned`

---

## Goal
Find the password for the next level.

---

## Solution

The page presents a form asking for a **secret**. Viewing the page source reveals the server-side PHP code:

```php
<?include "includes/secret.inc";

if(array_key_exists("submit", $_POST)) {
    if($secret == $_POST['secret']) {
        print "Access granted. The password for natas7 is <censored>";
    } else {
        print "Wrong secret";
    }
}?>
```

The secret is loaded from an included file: `includes/secret.inc`. Navigating to it directly:

```
http://natas6.natas.labs.overthewire.org/includes/secret.inc
```

The file exposes the secret in plain text:

```php
<?
$secret = "FOEIUWGHFEEUHOFUOIU";
?>
```

Enter `FOEIUWGHFEEUHOFUOIU` into the form and submit — access is granted and the password for the next level is revealed.

---

## Concept
> **Never store secrets in web-accessible files.** The `includes/` directory was not protected, allowing anyone to access `secret.inc` directly. Sensitive files like this should either be stored outside the web root, or the web server should be configured to deny direct access to them (e.g. via `.htaccess`). Additionally, secrets should never be hardcoded in source files — use environment variables instead.
