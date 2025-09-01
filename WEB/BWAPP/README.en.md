# Penetration Testing Write-Ups | BWAPP

![BWAPP Logo](other/logo.png)

A collection of practical write-ups on exploiting vulnerabilities in the educational web application BWAPP (Buggy Web Application).

## 📁 Contents

- [Directory Traversal (Files)](Directory%20Traversal%20%28Files%29/WRITEUP.md)
- [Insecure Direct Object Reference (IDOR)](IDOR%20%28Tickets%29/WRITEUP.md)
- [PHP Code Injection](PHP%20Code%20injection/WRITEUP.md)
- [Reflected XSS (GET)](Reflected%20XSS%20%28GET%29/WRITEUP.md)
- [SQL Injection (GET Search)](SQL%20Injection%20%28GET%20Search%29/WRITEUP.md)
- [SQL Injection (GET Select)](SQL%20Injection%20%28GET%20Select%29/WRITEUP.md)

## ⚠️ Disclaimer

**WARNING**: These materials are intended for educational purposes and information security research only. All testing was conducted in a controlled lab environment on a specially designed educational application. The author strongly condemns the use of described techniques for unlawful activities. The main purpose of this content is to document progress in learning web vulnerabilities and to educate readers about common threats.

**DO NOT USE these techniques for unauthorized access to systems without explicit permission from owners!**!!!!!!!!!!!!!!!!!!!

## 🛡️ Responsible Disclosure

I adhere to the principles of ethical hacking and responsible vulnerability disclosure. All research is conducted in accordance with:

- OWASP principles
- Ethical penetration testing standards  
- Local and international legislation

## 📊 Covered Vulnerabilities

| Vulnerability | Difficulty Levels | OWASP Category |
|---------------|-------------------|----------------|
| Directory Traversal | Low, Medium | A01:2021 |
| IDOR | Low, Medium | A01:2021 |
| PHP Code Injection | Low | A03:2021 |
| Reflected XSS | Low, Medium | A03:2021 |
| SQL Injection | Low | A03:2021 |

## 🛠️ Tools Used

- **Burp Suite** - HTTP request interception and modification
- **Python HTTP Server** - HTTP server setup
- **Browser Developer Tools** - analysis and debugging
- **Hashcat** - password recovery tool

## 📝 Structure

```
├── Directory Traversal (Files)
│   ├── images
│   │   ├── DirTravMediumDetect.png
│   │   ├── DirTravMediumSucess.png
│   │   ├── DirTravShadow.png
│   │   ├── DirTravSucess.png
│   │   └── DirTravTarget.png
│   ├── WRITEUP.en.md
│   └── WRITEUP.md
├── IDOR (Tickets)
│   ├── images
│   │   ├── IdorMediumSucess.png
│   │   ├── IdorTicketsFunction.png
│   │   ├── IdorTicketsMedium.png
│   │   ├── IdorTicketsSuccess.png
│   │   └── IdorTicketsTarget.png
│   ├── WRITEUP.en.md
│   └── WRITEUP.md
├── other
│   └── logo.png
├── PHP Code injection
│   ├── images
│   │   ├── PhpiFunction.png
│   │   ├── PhpiPoc.png
│   │   ├── PhpiSucess.png
│   │   └── PhpiTarget.png
│   ├── WRITEUP.en.md
│   └── WRITEUP.md
├── README.en.md
├── README.md
├── Reflected XSS (GET)
│   ├── images
│   │   ├── XssReflectedBrowser.png
│   │   ├── XssReflectedCookieTheftTest.png
│   │   ├── XssReflectedFunction.png
│   │   ├── XssReflectedGetBurp.png
│   │   ├── XssReflectedMamont1.png
│   │   ├── XssReflectedMamont2.png
│   │   ├── XssReflectedMamontCookie.png
│   │   ├── XssReflectedSuccess.png
│   │   └── XssReflectedTarget.png
│   ├── WRITEUP.en.md
│   └── WRITEUP.md
├── SQL Injection (GET Search)
│   ├── images
│   │   ├── SqlGetSearchUnion.png
│   │   ├── SqlietGetSelectTest2.png
│   │   ├── SqliGetSearchFunction.png
│   │   ├── SqliGetSearchSuccess.png
│   │   ├── SqliGetSearchTarget.png
│   │   ├── SqliGetSearchTest.png
│   │   ├── SqliGetSearchUnionPwd.png
│   │   └── SqliGetSearchUnionUsers.png
│   ├── WRITEUP.en.md
│   └── WRITEUP.md
└── SQL Injection (GET Select)
    ├── images
    │   ├── SqliGetSelectFunction.png
    │   ├── SqliGetSelectPwd.png
    │   ├── SqliGetSelectTarget.png
    │   ├── SqliGetSelectTest.png
    │   └── SqliGetSelectUsers.png
    ├── WRITEUP.en.md
    └── WRITEUP.md
```


## 🌐 Languages

Each write-up is available in two languages:
- 🇷🇺 Russian (`WRITEUP.md`)
- 🇬🇧 English (`WRITEUP.en.md`)

## 🔗 Useful Links

- [Official BWAPP Website](http://www.itsecgames.com/)
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)