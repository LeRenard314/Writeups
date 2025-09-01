## Insecure Direct Object Reference (IDOR) (Tickets)
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

![[images/IdorTicketsTarget.png]]

# Functionality
---

The application allows to place an order:

![[images/IdorTicketsFunction.png]]

# Exploitation (Low security level)
---

The application passes `ticket_quantity` and `ticket_price` parameters, which can be easily modified to an absurd condition ^^:

![[images/IdorTicketsSuccess.png]]

# Exploitation (Meduim securtiy level)
---

On the medium security level, the `ticket_price` parameter is likely hard-coded, and not passed via http:

![[images/IdorTicketsMedium.png]]

Although it is still possible to trick the application by adding the missing parameter to the request with the desired value (the I symbol added by accident to the `order` value):

![[images/IdorMediumSucess.png]]
