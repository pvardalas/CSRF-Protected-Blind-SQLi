### CSRF & WAF-Protected Blind SQLi

### Author

- **Panagiotis Vardalas**

# Usage:
```sh
$ python3 exploit.py

Password: when_will_sqli_finally_just_die
[✔] Recovered password!
```

# Overview

### This is the solution to a web CTF challenge that combines SQL Injection (SQLi) with Cross-Site Request Forgery (CSRF) protection. The challenge required extracting an admin password from a database while navigating CSRF-protected requests, bypassing a strict Web Application Firewall (WAF), and implementing blind SQLi via character-by-character enumeration.

## Here’s how the exploit works:

### This exploit works by hijacking a POST request used to react to a picture and sends custom data to the server. The request includes a CSRF token and an id parameter, which is vulnerable to blind SQL injection.
### To bypass the strict WAF, I carefully crafted payloads to trigger different server responses:
* When the SQL condition was true, the server responded normally with a json message (indicating success or failure).
* When the condition was false, the WAF returned a custom error message.
* When the payload was invalid, the server returned a 500 error.
* By observing these distinct responses, I was able to infer the correctness of each guessed character and enumerate the admin password character-by-character despite the protections.
