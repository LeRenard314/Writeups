# Basic server-side template injection (code context)

Выберите язык / Choose your language:

- 🇷🇺 [Русский](WRITEUP.ru.md)  
- 🇬🇧 [English](WRITEUP.en.md)

## Disclaimer
---

**The text was written and translated by the author manually. A language model was used for formatting and stylistic editing.**

**This material is provided for educational and research purposes only. I do not encourage or call for unauthorized access to information systems or violation of the law. In my opinion, one of the most effective ways to combat cybercrime is to educate both everyday users and managers, as well as developers of digital products about common vulnerabilities that could potentially be exploited by malicious actors to carry out unlawful acts.**

**⚠️ All actions described in this document were performed within an authorized research environment (CTF/test platform), without violating the rights of third parties or current legislation.**

**Unauthorized interference with computer systems, violation of data storage and processing rules, and other forms of so-called "black-hat" hacking are contrary to law and the ethics of information security.**

**I adhere to the principles of ethical research and responsible vulnerability disclosure.**


## Target

![placeholder](images/lab2SSTIcard.png)

The instance seems to be a blogging application:

![placeholder](images/lab2SSTITarget.png)

## Functionality

Once logged in with the given credentials, it can be discovered that apart from creating comments, each user has the option to select how would they to be displayed in the comment section (the `Prefferred name` box):

![placeholder](images/lab2SSTIdisplayFunc.png)

This is how our account name will be visible by default:

![Lab](images/lab2SSTIName.png)

When the `Name` selection is chosen:

![Lab](images/lab2SSTIfullName.png)

Finally, the `Nickname` option:

![placeholder](images/lab2SSTInickname.png)


The chosen variables are passed like so:

![placeholder](images/lab2SSTIdisplayRequest.png)

All of these factors are alarming symptoms of a possible `SSTI (Server-Side Template Injection)` vulnerability! This must be further investigated

## Exploitation

Knowing that the application runs with a `Tornado` python-powered template engine (from the lab description) it is possible to pass `Torando`-specific payloads to detect and exploit the vulnerability.

It is a good practice to start with a `Proof-of-Concept (PoC)` string:

``` Python
{{ 7 * 7 }}
```

![placeholder](images/lab2SSTIpoc1.png)

And, it works! The app rendered the result of the pythonic expression. We have confirmed `RCE`!

![placeholder](images/lab2SSTIpoc2.png)

However, while attempting further exploitation, I hit an unexpected problem:

I found a publicly available payload, which leverages operating system command execution via python:

``` Python
{% import os %} {{ os.system("whoami") }}
```

The app has no trouble in accepting the query, however once it gets processed, an internal server error is thrown: 

![placeholder](images/lab2SSTIpublicPayload.png)

![placeholder](images/lab2SSTIpublicPayloadError.png)


Thank you for you attention! ^^

