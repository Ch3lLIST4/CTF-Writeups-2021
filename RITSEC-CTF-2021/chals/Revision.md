# Revision

> > ... They aren’t necessarily obvious but are helpful to know.
>
> ```
> http://git.ritsec.club:7000/Revision.git/
> ```
>
> ~knif3

Another git challenge, cloning the repository to local obviously is the first step

After taking quite a long time, I think this could be a quite large repo they used to hide the flag, and I was right

![image-20210412141046916](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/RITSEC-CTF-2021/images/Revision.png?raw=true)

As the title of the challenge is `Revision`, I thought of `git rev-list` so I gave it a try

```bash
Admin@DESKTOP-ONTGILH MINGW64 ~/Downloads/ctf-git (master)
$ git rev-list --objects --all --reverse | grep flag
```

```
331bae08fb73b73f95252c1cf434d8b2b3a01d4b flag.txt
37622491df3f4aa9c9d05a03275ae5d5f5263bef flag.txt
98232c64fce9360c79f119cf6de8f670f69f1c44 flag.txt
db1a5a09f7ddd42f3ce395a761725516593fc4ff flag.txt
31354ec1389994b5f6708c7d915fdcc6bb76ba6e flag.txt
6e9f0da13f19b444ec3a9c3d6e795ad35c0554a2 flag.txt
573541ac9702dd3969c9bc859d2b91ec1f7e6e56 flag.txt
1a9cc2b7fbfa834924f4c03780d767ccbecf0c9c flag.txt
00750edc07d6415dcc07ae0351e9397b0222b7ba flag.txt
975fbec8256d3e8a3797e7a3611380f27c49f4ac flag.txt
4ae8ef021bf6fcfff43a13be5abfa52bb6fb5dbc flag.txt
b4785957bc986dc39c629de9fac9df46972c00fc flag.txt
f2ad6c76f0115a6ba5b00456a849810e7ec0af20 flag.txt
4286f428e3b19fe84de503916ce0e7dc8deefea1 flag.txt
d00491fd7e5bb6fa28c517a0bb32b8b506539d4d flag.txt
718f4d2ff533cf8ead8d3556cf43912bd245fbc4 flag.txt
d905d9da82c97264ab6f4920e20242e088850ce9 flag.txt
4bcfe98e640c8284511312660fb8709b0afa888e flag.txt
01058d844a98d293a3b03a8615a34700e4ed2be3 flag.txt
0ddf2bae71d08623786db120996eea00b75f8237 flag.txt
28ce6a8b26aa170e1de65536fe8abe1832bd3242 flag.txt
5c34318c2147fb2285de5a1513f46168e33e6baf flag.txt
```

I found the flag file but after `git show` them, I realize there's only 1 character in the file and they keep changing it. Those characters could be in order. After concating all those characters into a string i got this

```
RS{I_h0p3yuscr1tedgim}
```

It doesn't look like the correct flag yet maybe because of duplicate characters when they're making commits. So I tried a different approach

```sh
Admin@DESKTOP-ONTGILH MINGW64 ~/Downloads/ctf-git (master)
$ git log --reverse --follow -- flag.txt
```

```
commit 2a769ddc9f4bfdfcdce753068497ca251996f7db
Author: knif3 <knif3@mail.rit.edu>
Date:   Wed Feb 6 18:52:23 2019 -0500

    NDg1YmRiYWNlZmUyMjM0NGY2ZTc4Y2E1OGE2NjkyNDIK

commit 2092ddb909befa6ceee7449e4ce9433ba8bc8d57
Author: knif3 <knif3@mail.rit.edu>
Date:   Wed Feb 6 18:52:23 2019 -0500

    NjVkYjI3MzA3YWEwY2RmMGIzYzAzMjM0MzFlMDhhMTUK

commit 331c43d1166915dd6e10994d531de9f3d986d616
Author: knif3 <knif3@mail.rit.edu>
Date:   Wed Feb 6 18:52:23 2019 -0500

    ZDliZWQzYjdlMTUxZjExYjhmZGFkZjc1ZjFkYjk2ZDkK

commit f23c83288b5f594a595aef47a7c5cb37213f31dd
Author: knif3 <knif3@mail.rit.edu>
Date:   Wed Feb 6 18:52:23 2019 -0500

    MzJmOGUwYmI2OTQ0YTZlZmU4YjEzNTFiNzJiOGZhY2MK
...
```

Folllowing all of those commits I finally found the flag

Flag :

```
RS{I_h0p3_y0u_scr1pted_c0ms}
```

