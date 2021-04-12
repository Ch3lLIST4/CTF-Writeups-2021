# Music Signs

> Geno occasionally keeps up with his ex’s music interests. What do they say about her personality?
>
> Author: Brendy

`Music Signs` is the next challenge in the OSINT series after `Finding Geno` and `Data Breach` 

As we already found [all Geno's social medias](http://about.me/genoikonomov) on the previous challenges. Let's take a look at those accounts to see if there's any info related to his ex

As my country uses Facebook a lot so that was the first platform I used to search for information. On [his Facebook profile](https://www.facebook.com/geno.ikonomov) I found 2 of his friends, `Claire Alexa` whose profile has a female as their avatar and says that they are having a complicated relationship, and another one is `David Petterson` who I believed to be his colleague as I already saw this avatar on Bridgewater's LinkedIn

![image-20210412132810896](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/RITSEC-CTF-2021/images/MusicSigns-1.png?raw=true)

I took a look at all of them posts on Facebook and unfortunately I found nothing related to her music interests. I moved on to the next platform, which is Twitter, and I found Claire again as one of Geno's followers

![image-20210412133039703](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/RITSEC-CTF-2021/images/MusicSigns-2.png?raw=true)

We even found her Spotify account URL laying right in her Twitter description. And this is a jackpot as this challenge is about `music interests`

![image-20210412133314545](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/RITSEC-CTF-2021/images/MusicSigns-3.png?raw=true)

So far we know that she follows `Taylor Swift`, `Ariana Grande` and `Ed Sheeran` but this wasn't very helpful

As I'm already using Spotify, I know one thing that in order to view a user's public playlists, we have to first sign in, and I found it

![image-20210412133530666](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/RITSEC-CTF-2021/images/MusicSigns-4.png?raw=true)

Taking a look at the playlist we found out that this is where the flag could be as I can see `RS{}` as its playlist's name

![image-20210412133654163](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/RITSEC-CTF-2021/images/MusicSigns-5.png?raw=true)

At first I thought `her personality` was `Unstable` (as the name of a song in the playlist), but I wasn't right. Turns out I have to take the first letters of all the songs' names and make it an in-order string

I got `SAGITTARIUS` which is a zodiac sign, so it could be related to `her personality`, and I was right

Flag :

```
RS{SAGITTARIUS}
```

