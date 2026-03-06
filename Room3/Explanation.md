# Natas — Level 2

**URL:** http://natas2.natas.labs.overthewire.org  
**Username:** `natas2`  
**Password:** `TguMNxKo1DSa1tujBLuZJnDUlCcUAPlI`

---

## Goal
Find the password for the next level.

---

## Solution

The page displays *"There is nothing on this page"*, but inspecting the source code reveals an `<img>` tag referencing a file:

```html
<img src="files/pixel.png">
```

This tells us there is a `files/` directory on the server. Navigating to it directly:

```
http://natas2.natas.labs.overthewire.org/files/
```

The directory listing is exposed, showing two files:

```
pixel.png
users.txt
```

Opening `users.txt` reveals a list of credentials, including the password for the next level:

```
http://natas2.natas.labs.overthewire.org/files/users.txt
```

---

## Concept
> **Directory listing** should always be disabled on web servers. When enabled, anyone can browse the contents of a directory and access files that were never meant to be public. Additionally, sensitive files like `users.txt` should never be stored in a web-accessible directory.
