# OS Command injection, simple case

Choose your language / Выберите язык:

- 🇷🇺 [Русский](WRITEUP.ru.md)
- 🇬🇧 [English](WRITEUP.en.md)

## Disclaimer

**The text was written and translated by the author manually. A language model was used for formatting and stylistic editing.**

**This material is provided exclusively for educational and research purposes. I do not encourage or promote unauthorized access to information systems or violation of the law. In my opinion, one of the most effective ways to combat cybercrime is to educate both ordinary users and managers, as well as developers of digital products, about common vulnerabilities that could potentially be exploited by malicious actors to commit unlawful acts.**

**⚠️ All actions described in this document were performed in an authorized research environment (CTF/test platform), without violating the rights of third parties or applicable legislation.**

**Unauthorized interference with computer systems, violation of data storage and processing rules, and other forms of so-called "black hat" hacking contradict the law and the ethics of information security.**

**I adhere to the principles of ethical research and responsible disclosure of vulnerabilities.**

## Objective

![placeholder](images/labCard.png)

We are required to trigger a `whoami` call, confirming the presence of `OS Command Injection`.

![placeholder](images/labTarget.png)

The application is a standard PortSwigger online store layout. The products, as always, are quite amusing^^

## Functionality

Users can browse the products displayed in the store, and view their descriptions. There is also a "check stock" function. Upon clicking the button, the user receives the quantity of the product available for sale:

![placeholder](images/labCheckStock.png)

Since we know the context of the task, we can proceed directly on testing for `OS Command Injection`. However, it is worth noting that this is done only because the lab serves an educational purpose. Additionally, there are no distinctive behavior patterns on which we could form a hypothesis about the possible presence of the vulnerability (for example, visible involvement of a `Shell` script in data processing). In a real pentest, it is important to assess the full context before bombing the app with payloads.

## Exploitation

### Manual Testing

Let's intercept the request going to the stock check endpoint (`/product/stock`):

![placeholder](images/labRequest.png)

Now let's try to squeeze in arbitrary code into the processed querry, for example using command chaining with the `;` character, and as an honor of  tradition, let's impersonate Jesse Pinkman:

```shell
productId=1&storeId=1; echo "Yo, Mr.White!!! Command injection!"
```

![placeholder](images/labPoC.png)

It worked! The application is vulnerable to command injection!

^^

![placeholder](images/jesse.gif)

Now, to complete the task, we can call any OS command - the application will detect the call and display success:

![placeholder](images/labExecution.png)

![placeholder](images/labSolved.png)

### Automated Testing

Now for the most interesting part: a way to solve the lab without opening `BurpSuite` or manually editing requests. For this we'll fire up `commix`.

```shell
commix -r request.txt --os-cmd="whoami"
```

The `-r` flag reads input from a text file containing the raw HTTP request. `--os-cmd="whoami"` will execute the specified command by injecting it into the payload immediately after heuristic confirmation of the vulnerability.

In the context of this lab we are not interested in additional `HTTP` headers, and for convenience we can make `commix` ignore them:

```shell
commix -u "https://instance-link" --data="productId=1&storeId=1" --os-cmd="whoami"
```

![placeholder](images/labCommixParam1.png)

First the tool examined the `productId` parameter, then moved on to `storeId`:

![placeholder](images/labCommixParam2.png)

As we can see, in both cases `commix` found potential to exploit the vulnerability, selected working payloads, and verified itself. And it didn't forget to additionally execute `whoami`!

After finishing the payload selection, you can invoke a pseudo-shell (all commands written here will be sent to the target wrapped in a payload, and the result of execution will be returned to the researcher):

![placeholder](images/labCommixPsuedoShell.png)

I decided to look around the root and current directories, and also viewed the contents of that very unfortunate script responsible for data processing:

```shell
#!/bin/bash
set -u eval cksum <<< "$1 $2" | cut -c 2-3 | rev | sed s/0/1/
```

The problem is obvious. The `eval` function (converts received text into executable code — smell that?^^) directly substitutes parameters received from the request without proper sanitization. The script also sheds light on why the vulnerability can be triggered through both parameters, not just the last one (which is the most convenient).

Let's verify this visually. Here is the result of a request with a normal `productID` value:

![placeholder](images/labNormal.png)

And here with a modified one - in this case I appended a `pwd` call:

![placeholder](images/labAltered.png)

## Mitigation

To avoid vulnerabilities related to command injection, direct concatenation of unvalidated user input into executable code strings must not be permitted. Ideally, such operations should be redirected to dedicated language functions that are guaranteed not to invoke a shell. Input validation mechanisms must meet all security standards and prevent bypass techniques. Processes of this kind should always be run under a low-privilege user. This way, even if `RCE` does occur, the attacker's further maneuvers will have less freedom and thus, less possible to cause serious harm.

Thank you for your attention! ^^