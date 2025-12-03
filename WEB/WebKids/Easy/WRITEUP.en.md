# WebKids Easy

## Language Selection
- 🇷🇺 [Русский](WRITEUP.md)  
- 🇬🇧 [English](WRITEUP.en.md)

I'm finally starting to close the "gestalt" on the WebKids platform tasks. I remember tinkering with a couple of them at the very beginning of my journey and then dropping it. That was a real shame — there are many tasks, they are varied, and all of them are interesting ^^ It's nice to feel the progress, because after some time, it even becomes funny how I struggled with some of them when I was just starting out. Maybe this material will be useful for beginners.

Below, I'll walk through all the tasks in the `easy` category.

# Enjoy the read!

---

## Disclaimer

The text was written and translated by the author manually. A language model was used for formatting and stylistic editing.
This material is prepared solely for educational and research purposes. I do not encourage or call for unauthorized access to information systems or violation of the law.

⚠️ **All actions described in this document were performed within a permitted research environment (CTF/test platform), without infringing on the rights of third parties or violating current legislation.**

Illegal interference with computer systems, violation of rules for storing and processing computer information, and other forms of so-called "black hat" hacking contradict the law and the ethics of information security.

I adhere to the principles of **ethical hacking** and responsible vulnerability disclosure.

Although... There won't be much actual hacking here anyway ^^

---

## Level 1

![placeholder](images/webKidsLevel1Card.png)

Follow the link, grab the easiest flag ever ^^

![placeholder](images/webKidsLevel1Solve.png)

---

## Level 2

![placeholder](images/webKidsLevel2Card.png)

Follow the link, find the flag in the HTML:

![placeholder](images/webKidsLevel2Solve.png)

---

## Level 3

![placeholder](images/webKidsLevel3Card.png)

Oh, a situation.

![placeholder](images/webKidsLevel3Target.png)

Say hello to my little friend, `curl`. Of course, we could try playing with the User-Agent, but we're cool hackers — we do everything in the terminal:

![placeholder](images/webKidsLevel3Solve.png)

Here ^^

---

## Level 4

![placeholder](images/webKidsLevel4Card.png)

Continuing the conversation:

![placeholder](images/webKidsLevel4Target.png)

Again, let's use `curl` and successfully get the flag:

![placeholder](images/webKidsLevel4Solve.png)

---

## Level 5

![placeholder](images/webKidsLevel5Card.png)

Learning URL encoding, no SMS or registration required ^^

![placeholder](images/webKidsLevel5Target.png)

And `curl` comes to the rescue again:

![placeholder](images/webKidsLevel3Solve.png)

---

## Level 6

![placeholder](images/webKidsLevel6Card.png)

![placeholder](images/webKidsLevel6Target.png)

Again, we start curling, sending the required headers:

![placeholder](images/webKidsLevel6Solve.png)

---

## Level 7

![placeholder](images/webKidsLevel7card.png)

I remember this task gave me a lot of headaches, all because of the wrong cookie token format in the file.

![placeholder](images/webKidsLevel7Target.png)

We create a file in a way `curl` can parse it (as shown in the photo) and send the request:

![placeholder](images/webKidsLevel7Solve.png)

---

## Level 8

![placeholder](images/webKidsLevel8card.png)

![placeholder](images/webKidsLevel8Target.png)

This time, I got too lazy to do terminal gymnastics, so I just found the little flag in the dev tools:

![placeholder](images/webKidsLevel8Solve.png)

---

## Level 9

![placeholder](images/webKidsLevel9Card.png)

![placeholder](images/webKidsLevel9Target.png)

Huh? ((

![placeholder](images/webKidsLevel9Cookie.png)

Noticed an interesting cookie with a telling name — we can try to spoof it:

![placeholder](images/webKidsLevel9Solve.png)

And that gives us the flag ^^

---

## Level 10

![placeholder](images/webKidsLevel10Card.png)

![placeholder](images/webKidsLevel10Target.png)

Let's check the contents of `robots.txt`:

![placeholder](images/webKidsLevel10RobotsTxt.png)

Now, let's go to the discovered directory and get the flag:

![placeholder](images/webKidsLevel10Solve.png)

---

## Level 11

![placeholder](images/webKidsLevel11Card.png)

![placeholder](images/webKidsLevel11Target.png)

Let's fuzz the application with a basic `dirbuster` scan:

![placeholder](images/webKidsLevel11Dirb.png)

Surprisingly, it took a very long time (I stopped it when it found something), but it still highlighted the needed endpoint.

![placeholder](images/webKidsLevel11Solve.png)

Going there gives us the flag.

---

## Level 12

![placeholder](images/webKidsLevel12Card.png)

![placeholder](images/webKidsLevel12Target.png)

Let's poke around the application's functionality:

![placeholder](images/webKidsLevel12Alert.png)

Check the dev tools:

![placeholder](images/webKidsLevel12Code.png)

All that's needed to solve this is to carefully trace the code and piece together the flag bit by bit:

![placeholder](images/webKidsLevel12Solve.png)

---

## Level 13

![placeholder](images/webKidsLevel13Card.png)

![placeholder](images/webKidsLevel13Target.png)

If you open the dev tools, you'll see `JsFuck`:

![placeholder](images/webKidsLevel13JSFuck.png)

Let's decode this JsFuckery:

![placeholder](images/webKidsLevel13Decode.png)

Something related to `localStorage` — let's check it, can't hurt ^^

![placeholder](images/webKidsLevel13Solve.png)

Indeed, the flag is there. Wrap it in KSL{} and enjoy life.

---

## Level 14

![placeholder](images/webKidsLevel14Card.png)

So, the final level.

![placeholder](images/webKidsLevel14Target.png)

Hmm, okay, let's call the provided endpoint:

![placeholder](images/webKidsLevel14File.png)

Oi mate, the file is foooooookin raw ^^
Let's download it via `curl`:

![placeholder](images/webKidsLevel14Solve.png)

Here it is:

![placeholder](images/flag.png)

That's all for the `easy` category.

# Thank you for your attention!