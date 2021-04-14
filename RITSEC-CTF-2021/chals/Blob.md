# Blob

> Ha. Blob. Did you get the reference?
>
> ```
> http://git.ritsec.club:7000/blob.git/
> ```
>
> ~knif3

After cloning and checking all of the branches and included files. I found nothing other than `That pesky flag should be around here somewhere...` appeared in `README.md` and `these aren't the droids you're looking for` in `flag.txt`

As the title of the challenge is `Blob` so I was thinking about *Git blobs* or [Git objects](https://git-scm.com/book/en/v2/Git-Internals-Git-Objects)

```bash
Admin@DESKTOP-ONTGILH MINGW64 ~/Downloads/ctf-git (master)
$ find .git/objects -type f
```

```
.git/objects/a6/9cb6306e8b75b6762d6aa1b0279244cacf3f3b
.git/objects/b9/d6753be80df863c3656aa6389418d3213c96f2
.git/objects/d0/644363aa853a17c9672cefff587580a43cf45e
.git/objects/df/576e13e1ca1c4310d3260f63bef4db41218ba0
.git/objects/e5/97cc86a0881ab3028dba090f88c1cbd33ad9a4
```

I tried reading out the first object but no luck

```bash
Admin@DESKTOP-ONTGILH MINGW64 ~/Downloads/ctf-git (master)
$ git cat-file -p a69cb6306e8b75b6762d6aa1b0279244cacf3f3b
```

```
tree b9d6753be80df863c3656aa6389418d3213c96f2
author knif3 <knif3@mail.rit.edu> 1617947351 +0000
committer knif3 <knif3@mail.rit.edu> 1617947351 +0000

Initial Commit
```

Reading the 2nd object I found the flag file

```bash
Admin@DESKTOP-ONTGILH MINGW64 ~/Downloads/ctf-git (master)
$ git cat-file -p b9d6753be80df863c3656aa6389418d3213c96f2
```

```
100644 blob e597cc86a0881ab3028dba090f88c1cbd33ad9a4    README.md
100644 blob df576e13e1ca1c4310d3260f63bef4db41218ba0    flag.txt
```

I tried to read it but it was actually the same content as when I opened the file after cloning the repository so it wasn't this one

```bash
Admin@DESKTOP-ONTGILH MINGW64 ~/Downloads/ctf-git (master)
$ git cat-file -p df576e13e1ca1c4310d3260f63bef4db41218ba0
```

```
these aren't the droids you're looking for
```

Moving on to the third object, this time fortunately I found the real flag

```bash
Admin@DESKTOP-ONTGILH MINGW64 ~/Downloads/ctf-git (master)
$ git cat-file -p d0644363aa853a17c9672cefff587580a43cf45e
```

Flag :

```
RS{refs_can_b3_secret_too}
```

