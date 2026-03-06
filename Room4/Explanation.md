# Natas — Level 3

**URL:** http://natas3.natas.labs.overthewire.org  
**Username:** `natas3`  
**Password:** `3gqisGdR0pjm6tpkDKdIWO2hSvchLeYH`

---

## Goal
Find the password for the next level.

---

## Solution

The page displays *"There is nothing on this page"*. Inspecting the source code reveals a hint:

```html
<!-- No more information leaks!! Not even Google will find it this time... -->
```

The mention of **Google not finding it** is a hint towards `robots.txt` — a file used to tell search engine crawlers which directories they should **not** index. Navigating to it:

```
http://natas3.natas.labs.overthewire.org/robots.txt
```

The file reveals a hidden directory:

```
User-agent: *
Disallow: /s3cr3t/
```

Navigating to that directory:

```
http://natas3.natas.labs.overthewire.org/s3cr3t/
```

Directory listing is enabled, exposing a `users.txt` file. Opening it reveals the password for the next level:

```
http://natas3.natas.labs.overthewire.org/s3cr3t/users.txt
```

---

## Concept
> **`robots.txt` is not a security mechanism.** It is a convention that well-behaved crawlers follow voluntarily — anyone can read the file and access the listed directories. Sensitive directories should never be referenced in `robots.txt`, as it essentially acts as a map of hidden content for attackers.
