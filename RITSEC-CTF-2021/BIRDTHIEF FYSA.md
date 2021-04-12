# BIRDTHIEF: FYSA

> ~knif3
>
> [ BIRDTHIEF_FYSA.pdf](https://ctf.ritsec.club/files/da6836558110e083f9777504def7b588/BIRDTHIEF_FYSA.pdf?token=eyJ1c2VyX2lkIjo0NzksInRlYW1faWQiOjMwMywiZmlsZV9pZCI6OX0.YHMeeg.Y1tlfCaLmqn_zVEKnKcBs34HypM)

After downloading the file I did a few steps as usual to pre-check the file

```bash
ch3l@DESKTOP-ONTGILH:/mnt/d/ch3l$ file BIRDTHIEF_FYSA.pdf
```

```
BIRDTHIEF_FYSA.pdf: PDF document, version 1.4
```

```bash
ch3l@DESKTOP-ONTGILH:/mnt/d/ch3l$ xxd BIRDTHIEF_FYSA.pdf | head
```

```
00000000: 2550 4446 2d31 2e34 0a25 20e2 e3cf d30a  %PDF-1.4.% .....
00000010: 340a 300a 6f62 6a0a 3c3c 0a2f 5479 7065  4.0.obj.<<./Type
00000020: 0a2f 4361 7461 6c6f 670a 2f4e 616d 6573  ./Catalog./Names
00000030: 0a3c 3c0a 2f4a 6176 6153 6372 6970 740a  .<<./JavaScript.
00000040: 330a 300a 520a 3e3e 0a2f 5061 6765 4c61  3.0.R.>>./PageLa
00000050: 6265 6c73 0a3c 3c0a 2f4e 756d 730a 5b0a  bels.<<./Nums.[.
00000060: 300a 3c3c 0a2f 530a 2f44 0a2f 5374 0a31  0.<<./S./D./St.1
00000070: 0a3e 3e0a 5d0a 3e3e 0a2f 4f75 746c 696e  .>>.].>>./Outlin
00000080: 6573 0a32 0a30 0a52 0a2f 5061 6765 730a  es.2.0.R./Pages.
00000090: 310a 300a 520a 3e3e 0a65 6e64 6f62 6a0a  1.0.R.>>.endobj.
```

...

Then I opened the file and see what's inside. There are a few slides gave out hints that I should take a look closer and try to extract all the data from this file

![image-20210411231120992](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/RITSEC-CTF-2021/images/BIRDTHIEF-FYSA-1.png?raw=true)

I searched for `pdf extract objects` on google for an online tool that can hopefully help me extract the data I need. And I found [this](https://www.extractpdf.com/) on the top

After letting the website finish file processing, I found the hidden flag in an image

![image-20210411231430910](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/RITSEC-CTF-2021/images/BIRDTHIEF-FYSA-2.png?raw=true)

Flag :

```
RS{Make_sure_t0_read_the_briefing}
```

