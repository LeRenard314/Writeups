# Information Disclosure on debug page

Выберите язык / Choose your language:

- 🇷🇺 [Русский](WRITEUP.ru.md)
- 🇬🇧 [English](WRITEUP.en.md)

## Disclaimer!!!

**The text was written and translated manually by the author. A language model was used for formatting and stylistic editing.**

**This material is provided exclusively for educational and research purposes. I do not encourage or endorse unauthorized access to information systems or violation of the law. In my opinion, one of the most effective ways to combat cybercrime is to educate ordinary users and managers, as well as developers of digital products, about common vulnerabilities that can potentially be used by malicious actors to commit unlawful actions.**

**⚠️ All actions described in this document were performed in an environment intended for authorized testing (CTF/test platform), without violating the rights of third parties or applicable legislation.**

**Unauthorized interference with computer systems, violation of data storage and processing rules, and other forms of so-called "black" hacking contradict the law and the ethics of information security.**

**I adhere to the principles of ethical research and responsible disclosure of vulnerabilities.**

---

## Objective

![placeholder](images/labCard.png)

Wow! maybe we will be fuzzing^^

The launched application is a store with amusing products

![placeholder](images/labTarget.png)

---

## Functionality

The user has access to viewing the storefront and products, but judging by the brief, we will be dealing with the `debug` endpoint, so in this case the functionality is not very interesting to us.

---

## Exploitation

Specifically in this case, there are only three ways to discover the `debug` page:

### Studying the source code

By digging into DevTools, you can easily find the path we are interested in:

![placeholder](images/labDebug.png)

---

### Fuzzing

A fuzzer with the default wordlist will pick up this path, since it is often found in legacy `CGI` configurations:

```shell
dirb https://0a3d0049043b193181e13ed600460019.web-security-academy.net
```

```shell
---- Scanning URL: https://0a3d0049043b193181e13ed600460019.web-securityacademy.net/ ----
	+ https://0a3d0049043b193181e13ed600460019.web-security-academy.net/analytics (CODE:200|SIZE:0)
	+ https://0a3d0049043b193181e13ed600460019.web-security-academy.net/cgi-bin (CODE:200|SIZE:410)
	+ https://0a3d0049043b193181e13ed600460019.web-security-academy.net/cgi-bin/ (CODE:200|SIZE:410)
	+ https://0a3d0049043b193181e13ed600460019.web-security-academy.net/favicon.ico (CODE:200|SIZE:15406)
	+ https://0a3d0049043b193181e13ed600460019.web-security-academy.net/filter (CODE:200|SIZE:11134)
	+ https://0a3d0049043b193181e13ed600460019.web-security-academy.net/product (CODE:400|SIZE:30)
```

In this case, `dirb` was not able to recursively pick up `phpinfo.php`, however this file can be discovered by navigating to the identified path `/cgi-bin`:

![placeholder](images/labFreeEndpoint.png)

Or you can fuzz `/cgi-bin` specifically:

```shell
---- Scanning URL: https://0a3d0049043b193181e13ed600460019.web-security-academy.net/cgi-bin/ ----
	+ https://0a3d0049043b193181e13ed600460019.web-security-academy.net/cgi-bin/phpinfo.php (CODE:200|SIZE:69811)
```

After identifying a valid endpoint, you can navigate to it:

![palceholder](images/labDebugPHP.png)

This is a real treasure trove of information about the application! Let's find the `SECRET_KEY` field:

![placeholder](images/labDebugPhpSecret.png)

Submit it:

![placeholder](images/labDebugPhpSecretValid.png)

And we get a pleasant message about successfully solving the lab:

![placeholder](images/labSolved.png)

---

## Mitigation

A case where multiple service endpoints are exposed to the outside is a serious security threat, since it provides the attacker with valuable information to expand the attack surface.

If for some reason this endpoint is needed, protection against this vulnerability is to return `403` to all "ordinary" users trying to access both `/cgi-bin/` and any of its contents (to prevent Broken Access Control). In the context of this lab, this implementation is possible, since cookie tokens are transmitted:

![placeholder](images/labCookieUsage.png)

And even better — simply do not deploy debug pages^^

Thank you for your attention! ^^