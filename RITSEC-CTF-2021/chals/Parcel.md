# Parcel

> That's a lot of magick~knif3
>
> [ Parcel](https://ctf.ritsec.club/files/d5a29cd660715d10b342a32a6c1506e2/Parcel?token=eyJ1c2VyX2lkIjo0NzksInRlYW1faWQiOjMwMywiZmlsZV9pZCI6MzF9.YHMwYg.3OGY8sLfSIJZK2Cgid2XXT3aMgo)

After downloading the file I did a few steps as usual to pre-check the file

```bash
ch3l@DESKTOP-ONTGILH:/mnt/d/ch3l$ file Parcel
```

```
Parcel: gzip compressed data, from Unix
```

```bash
ch3l@DESKTOP-ONTGILH:/mnt/d/ch3l$ xxd Parcel | head
```

```
00000000: 1f8b 0800 0000 0000 0003 ec9d 6b73 daba  ............ks..
00000010: d6c7 dff3 297c f69b e7ec 2105 df2f ed74  ....)|....!../.t
00000020: 5a08 9084 4b42 b8e5 f24e d8c2 56b0 6522  Z...KB...N..V.e"
00000030: cb06 e7d3 3f4b 86b4 4dea 7667 9339 cd64  ....?K..M.vg.9.d
00000040: 86cc 9480 2dcb 4b42 fe65 fdb5 96d4 e398  ....-.KB.e......
00000050: 724c f987 49be c21f a528 0d39 5921 c6eb  rL..I....(.9Y!..
00000060: 11d9 60ef 9334 8f53 ea21 967f feeb f3d3  ..`..4.S.!......
00000070: 1fd3 9015 d352 4dd9 5465 53b1 14db d23f  .....RM.TeS....?
00000080: 7ffe ab32 381b b43f cc30 4b48 4c3f 4a4a  ...28..?.0KHL?JJ
00000090: 4dae 8cd3 f91d 76f9 4769 9c52 69f2 904a  M.....v.Gi.Ri..J
```

After confirming it was the gzip file, as I was using Windows, I simply changed the file extension to `Parcel.gz` and extracted it. Inside of the extracted folder I found another `Parcel` named file

```bash
ch3l@DESKTOP-ONTGILH:/mnt/d/ch3l$ cd Parcel/
ch3l@DESKTOP-ONTGILH:/mnt/d/ch3l/Parcel$ ll
```

```
total 744
drwxrwxrwx 1 ch3l ch3l   4096 Apr 12 00:29 ./
drwxrwxrwx 1 ch3l ch3l   4096 Apr 12 00:40 ../
-rwxrwxrwx 1 ch3l ch3l 759456 Apr 12 00:23 Parcel*
```

I checked its filetype again and got

```
Parcel: multipart/mixed; boundary="===============6501672606206171874==", ASCII text, with very long lines
```

Taking a look at it I found that it was a bunch of PNG image files encoded using base64 encoding

```
...
VI. Weak Points and Strong

29. Military tactics are like unto water; for water in its natural course runs away from high places and hastens downwards.
--===============6764736863007653832==
Content-Type: image/png
MIME-Version: 1.0
Content-Transfer-Encoding: base64

iVBORw0KGgoAAAANSUhEUgAAA+gAAAGQAQMAAAAHg9giAAAABGdBTUEAALGPC/xhBQAAACBjSFJN
AAB6JgAAgIQAAPoAAACA6AAAdTAAAOpgAAA6mAAAF3CculE8AAAABlBMVEWt2Ob///9KyreRAAAA
AWJLR0QB/wIt3gAAAAd0SU1FB+UECRI4BuOLpwsAAAAQY2FOdgAAH0AAAASwAAALuAAAAADVYu1s
AAAASElEQVR42u3BMQEAAADCoPVPbQo/oAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
AAAAAAAAAAAAAAAAAAAAAICXAcTgAAGGKhurAAAAJXRFWHRkYXRlOmNyZWF0ZQAyMDIxLTA0LTA5
VDE4OjU2OjAzKzAwOjAwpQr1jQAAACV0RVh0ZGF0ZTptb2RpZnkAMjAyMS0wNC0wOVQxODo1Njow
MyswMDowMNRXTTEAAAAASUVORK5CYII=

--===============6764736863007653832==--
```

I used [this site](https://base64.guru/converter/decode/image/png) to convert base64 values back into images

There are a lot more images but these should be enough for the my writeups

![image-20210412004852385](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/RITSEC-CTF-2021/images/Parcel.png?raw=true)

Flag :

```
RS{Im_doing_a_v1rtual_puzzl3}
```

