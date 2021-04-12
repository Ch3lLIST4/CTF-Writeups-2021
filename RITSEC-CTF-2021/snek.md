# snek

> No step on snek
>
> ~knif3
>
> [snek](https://ctf.ritsec.club/files/7499aedbcfa15e66d15a95e90165eae0/snek?token=eyJ1c2VyX2lkIjo0NzksInRlYW1faWQiOjMwMywiZmlsZV9pZCI6N30.YHMU0A.RxJJLlds3mPoUjivVAmwuKHbflk)

Right after I downloaded the file, I checked what kind of file type it was

```bash
ch3l@DESKTOP-ONTGILH:/mnt/d/ch3l$ file snek
```

```
snek: data
```

So it's a data file, I tried to inspect further

```bash
ch3l@DESKTOP-ONTGILH:/mnt/d/ch3l$ xxd snek
```

```
00000000: 420d 0d0a 0000 0000 85a1 6e60 4203 0000  B.........n`B...
00000010: e300 0000 0000 0000 0000 0000 0004 0000  ................
00000020: 0040 0000 0073 4a00 0000 6400 5a00 4700  .@...sJ...d.Z.G.
00000030: 6401 6402 8400 6402 6501 8303 5a02 6503  d.d...d.e...Z.e.
00000040: 6403 8301 5a04 6502 6504 8301 5a05 6505  d...Z.e.e...Z.e.
00000050: 6504 6b02 723e 6506 6404 8301 0100 6506  e.k.r>e.d.....e.
00000060: 6405 8301 0100 6e08 6506 6406 8301 0100  d.....n.e.d.....
00000070: 6407 5300 2908 7a57 0a57 7269 7474 656e  d.S.).zW.Written
00000080: 2066 6f72 2052 4954 5345 4320 4354 4620   for RITSEC CTF
00000090: 3230 3231 0a41 7574 686f 723a 206b 6e69  2021.Author: kni
000000a0: 6633 0a46 6c61 673a 2052 4954 5345 437b  f3.Flag: RITSEC{
000000b0: 7d0a 0a54 4f44 4f3a 2046 696e 6973 6820  }..TODO: Finish
000000c0: 7468 6973 2063 6861 6c6c 656e 6765 0a63  this challenge.c
000000d0: 0000 0000 0000 0000 0000 0000 0200 0000  ................
000000e0: 4000 0000 731c 0000 0065 005a 0164 005a  @...s....e.Z.d.Z
...
000002f0: 0000 e97d 0000 0029 03da 0665 6e63 6f64  ...}...)...encod
00000300: 65da 0870 6173 7377 6f72 64da 0764 6563  e..password..dec
00000310: 7279 7074 2902 da04 7365 6c66 723d 0000  rypt)...selfr=..
00000320: 00a9 0072 4000 0000 fa07 736e 656b 2e70  ...r@.....snek.p
00000330: 79da 085f 5f69 6e69 745f 5f0a 0000 0073  y..__init__....s
00000340: 0400 0000 0001 0a01 7a0a 642e 5f5f 696e  ........z.d.__in
00000350: 6974 5f5f 6302 0000 0000 0000 0002 0000  it__c...........
00000360: 0003 0000 0043 0000 0073 2000 0000 7c00  .....C...s ...|.
00000370: 6a00 7401 7c00 6a02 8301 6b02 721c 7403  j.t.|.j...k.r.t.
00000380: 6401 8301 0100 6402 5300 6403 5300 2904  d.....d.S.d.S.).
00000390: 4e7a 0521 666c 6167 5446 2904 723d 0000  Nz.!flagTF).r=..
000003a0: 00da 0562 7974 6573 723e 0000 00da 0570  ...bytesr>.....p
000003b0: 7269 6e74 2902 723f 0000 00da 056f 7468  rint).r?.....oth
000003c0: 6572 7240 0000 0072 4000 0000 7241 0000  err@...r@...rA..
000003d0: 00da 065f 5f65 715f 5f0e 0000 0073 0800  ...__eq__....s..
000003e0: 0000 0001 1001 0801 0401 7a08 642e 5f5f  ..........z.d.__
000003f0: 6571 5f5f 4e29 05da 085f 5f6e 616d 655f  eq__N)...__name_
00000400: 5fda 0a5f 5f6d 6f64 756c 655f 5fda 0c5f  _..__module__.._
00000410: 5f71 7561 6c6e 616d 655f 5f72 4200 0000  _qualname__rB...
00000420: 7246 0000 0072 4000 0000 7240 0000 0072  rF...r@...r@...r
00000430: 4000 0000 7241 0000 0072 0100 0000 0900  @...rA...r......
00000440: 0000 7304 0000 0008 0108 0472 0100 0000  ..s........r....
00000450: 7a0f 456e 7465 7220 6d79 206e 616d 653a  z.Enter my name:
00000460: 207a 1249 535f 5448 4953 5f54 4845 5f46   z.IS_THIS_THE_F
00000470: 4c41 473f 3f5a 044e 4f50 455a 0557 524f  LAG??Z.NOPEZ.WRO
00000480: 4e47 4e29 07da 075f 5f64 6f63 5f5f da06  NGN)...__doc__..
00000490: 6f62 6a65 6374 7201 0000 00da 0569 6e70  objectr......inp
000004a0: 7574 da01 78da 0161 7244 0000 0072 4000  ut..x..arD...r@.
000004b0: 0000 7240 0000 0072 4000 0000 7241 0000  ..r@...r@...rA..
000004c0: 00da 083c 6d6f 6475 6c65 3e07 0000 0073  ...<module>....s
000004d0: 0e00 0000 0402 100b 0801 0801 0801 0801  ................
000004e0: 0a02
```

It looks like there is python code inside of the file so at first I thought it was a python serialized object, but it wasn't. Turns out it was just a bunch of compiled python bytecode. Therefore, I look for an online python decompiler and I found [a really good one](https://www.toolnb.com/tools-lang-en/pyc.html)

After uploading the file there was some kind of Chinese error pop-up and the progress bar was frozen so I thought there was something wrong with the uploaded file

![image-20210411224112142](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/RITSEC-CTF-2021/images/snek.png?raw=true)

I thought it was the file extension so I changed the filename to `snek.pyc` and uploaded it once again and it worked

Decompiled results :

```python
# uncompyle6 version 3.5.0
# Python bytecode 3.7 (3394)
# Decompiled from: Python 2.7.5 (default, Aug  7 2019, 00:51:29) 
# [GCC 4.8.5 20150623 (Red Hat 4.8.5-39)]
# Embedded file name: snek.py
# Size of source mod 2**32: 834 bytes
"""
Written for RITSEC CTF 2021
Author: knif3
Flag: RITSEC{}

TODO: Finish this challenge
"""

class d(object):

    def __init__(self, password):
        self.password = password.encode()
        self.decrypt = [97, 98, 99, 100, 101, 102, 103, 104, 105, 106, 107, 108, 109, 110, 111, 112, 113, 114, 115, 116, 117, 118, 119, 120, 121, 122, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 95, 82, 83, 123, 97, 108, 108, 95, 104, 105, 36, 36, 95, 97, 110, 100, 95, 110, 48, 95, 98, 105, 116, 51, 125]

    def __eq__(self, other):
        if self.password == bytes(self.decrypt):
            print('!flag')
            return True
        else:
            return False


x = input('Enter my name: ')
a = d(x)
if a == x:
    print('IS_THIS_THE_FLAG??')
    print('NOPE')
else:
    print('WRONG')
```

Those numbers in the array looks like Decimal converted ASCII characters so I gave it a try

First I extracted all the unnecessary `,` characters using JavaScript on Chrome Dev-tools

```javascript
'97, 98, 99, 100, 101, 102, 103, 104, 105, 106, 107, 108, 109, 110, 111, 112, 113, 114, 115, 116, 117, 118, 119, 120, 121, 122, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 95, 82, 83, 123, 97, 108, 108, 95, 104, 105, 36, 36, 95, 97, 110, 100, 95, 110, 48, 95, 98, 105, 116, 51, 125'.replaceAll(',','')
```

```
97 98 99 100 101 102 103 104 105 106 107 108 109 110 111 112 113 114 115 116 117 118 119 120 121 122 65 66 67 68 69 70 71 72 73 74 75 76 77 78 79 80 81 82 83 84 85 86 87 88 89 90 95 82 83 123 97 108 108 95 104 105 36 36 95 97 110 100 95 110 48 95 98 105 116 51 125
```

Then I used [rapidtables website](https://www.rapidtables.com/convert/number/ascii-hex-bin-dec-converter.html) to convert those decimal values to readable text, and it works

```
abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ_RS{all_hi$$_and_n0_bit3}
```

Flag :

```
RS{all_hi$$_and_n0_bit3}
```







