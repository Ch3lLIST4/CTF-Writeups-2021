# #OSINTChallenge

> The CEO of Geno’s company loves local art and nature. Where was she when she took the photo in her Twitter background? (Wrap the answer in RS{} and use underscores between each word.)
>
> Author: FrozenTundras

 `#OSINTChallenge` is the next challenge in the OSINT series after `Finding Geno` , `Data Breach` , and `Music Signs`

For the CEO of Geno's company, we must again start the process on the LinkedIn page and found [her LinkedIn profile](https://www.linkedin.com/in/dr-joanne-turner-frey-91b255209/)

So all I had from the LinkedIn profile were her email which is [joanne.m.turner94@gmail.com](mailto:joanne.m.turner94@gmail.com) and her full name. I used the information I got and found her Twitter on the search bar : https://twitter.com/joanne_turner_f

![image-20210412140529162](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/RITSEC-CTF-2021/images/OSINTChallenge-1.png?raw=true)

This is the `Twitter background` they were talking about :

https://twitter.com/joanne_turner_f/header_photo

![Image](https://pbs.twimg.com/profile_banners/1371376496078639106/1617145689/1500x500)

Other pieces of information I got from her Twitter is that she's a `Lover of Lake Ontario` and on March 18 which wasn't long ago, she tweeted about it's `kayaking time`, so I thought the place which she took the picture was somewhere around [Lake Ontario](https://en.wikipedia.org/wiki/Lake_Ontario)

I tried some reverse searchs, metadata, web archives but no luck. So I thought to myself there must be something else I could get out of this image

Looking at the ground I saw an art which looks like a kind of symbol and the area was pretty large. At first I thought it was some kind of a weird steering wheel. Turns out it was a **piece sign** after I googling all the circle related symbols

I tried to search for that "pretty unique" symbol on [Google Earth](https://earth.google.com/web/) and I was lucky. I really found a place near Lake Ontario

![image-20210412140133533](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/RITSEC-CTF-2021/images/OSINTChallenge-2.png?raw=true)

Oh that looks kinda similar

![image-20210412140236708](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/RITSEC-CTF-2021/images/OSINTChallenge-3.png?raw=true)

![image-20210412140340818](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/RITSEC-CTF-2021/images/OSINTChallenge-4.png?raw=true)

Flag :

```
RS{Durand_Eastman_Park}
```