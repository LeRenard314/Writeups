# Information Disclosure in Error Messages

Выберите язык / Choose your language: 
 
- 🇷🇺 [Русский](WRITEUP.ru.md)  
- 🇬🇧 [English](WRITEUP.en.md)

## Disclaimer

**⚠️ All actions described in this document were performed in an environment intended for authorized testing (CTF/test platform), without violating the rights of third parties or applicable laws.**

**Unauthorized interference with computer systems, violation of data storage and processing rules, and other forms of so-called “black hat” hacking contradict the law and the ethics of information security.**

**I adhere to the principles of ethical research and responsible disclosure of vulnerabilities.**

## Objective

![placeholder](images/labCard.png)

Based on the brief, it is necessary to trigger an application error and determine the version of the framework running under the hood.

After launching the instance, we see a web store with amusing products:

![placeholder](images/labTarget.png)


## Functionality

The user has access to a product viewing function, which returns items using the `productID` parameter:

![placeholder](images/labProduct.png)

## Exploitation

The `productID` parameter most likely expects an integer value as input, so we will try to trigger an application error by passing unexpected input:

``` Shell
https://LAB_ID?productID=blahblahblah
```

As a result, an error was displayed that reveals a lot of information about the backend:

![placeholder](images/labErrorMsg.png)

The data of interest to us is `Apache Struts 2 2.3.31`. Disclosure of this information is dangerous because it allows an attacker to expand the attack surface by searching for relevant CVEs. As an example for the mentioned version of Apache Struts - `CVE-2017-5638`.

Using the `Submit Solution` button, we submit the "flag", solving the lab:

![placeholder](images/labSolved.png)

## Mitigation

If errors occur during serving, they should be raised locally and under no circumstances rendered on the client side.

Thank you for your attention! ^^