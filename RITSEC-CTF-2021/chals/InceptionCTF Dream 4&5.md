# InceptionCTF Dream 4

> Note: This challenge builds off of InceptionCTF: Dream 3
>
> Don’t lose yourself within the dreams, it’s critical to have your totem. Take a close look at the facts of the file presented to you. Please note the flag is marked with an “RITSEC=” rather than {} due to encoding limitations.
>
> The flag will need to be converted to RITSEC{}
>
> Author: Brandon Martin

`InceptionCTF Dream 4` is the fourth challenge in the `InceptionCTF Dream` series so we need to accomplish previous challenges before heading to this challenge

So after finishing `InceptionCTF Dream 3`, you'll get a flag which is the password to extract `SnowFortress.zip`

Taking a look at the new files

```sh
ch3l@DESKTOP-ONTGILH:/mnt/d/ch3l/InceptionCTFRITSEC/Reality/VanChase/SnowFortress$ ll
```

```
total 248
drwxrwxrwx 1 ch3l ch3l   4096 Apr 15 15:34 ./
drwxrwxrwx 1 ch3l ch3l   4096 Apr 15 15:34 ../
-rwxrwxrwx 1 ch3l ch3l   3848 Feb 25 01:34 Limbo.7z*
-rwxrwxrwx 1 ch3l ch3l 246867 Feb 25 01:32 PasswordP‮exe.hta*
```

```sh
ch3l@DESKTOP-ONTGILH:/mnt/d/ch3l/InceptionCTFRITSEC/Reality/VanChase/SnowFortress$ file *
```

```
Limbo.7z:         7-zip archive data, version 0.4
PasswordP‮exe.hta: PE32+ executable (GUI) x86-64, for MS Windows
```

I used `strings` command I found a JavaScript tag at the end which seems to be a source code encoded in hex format

```sh
ch3l@DESKTOP-ONTGILH:/mnt/d/ch3l/InceptionCTFRITSEC/Reality/VanChase/SnowFortress$ strings PasswordP‮exe.hta
```

```
...
M6W}6kY
aP?9'
=`rU
1X5%
%GLZ
vCNo
u]ax
F8}-
^c?Q
zT<2
cT$z
G+{c
c(aM
B!U~8Hg
IEND
&@@>x
 774_kki
=YVU
4ida
LD?]
SHC3
KDE&
4543!! B
Hcdc}
$%!/
00,w
yur:QNO[
f_]'
MML%BBBQ
XXWB
A>?2
<script language="javascript">document.write(unescape('3c%68%74%6d%6c%3e%0a%3c%62%6f%64%79%3e%0a%0a%3c%21%44%4f%43%54%59%50%45%20%68%74%6d%6c%3e%0a%3c%68%74%6d%6c%3e%0a%3c%68%65%61%64%3e%0a%20%20%20%20%3c%74%69%74%6c%65%3e%4e%6f%6e%2c%20%6a%65%20%6e%65%20%72%65%67%72%65%74%74%65%20%72%69%65%6e%3c%2f%74%69%74%6c%65%3e%0a%3c%48%54%41%3a%41%50%50%4c%49%43%41%54%49%4f%4e%0a%20%20%41%50%50%4c%49%43%41%54%49%4f%4e%4e%41%4d%45%3d%22%4e%6f%6e%2c%20%6a%65%20%6e%65%20%72%65%67%72%65%74%74%65%20%72%69%65%6e%22%0a%20%20%49%44%3d%22%49%6e%63%65%70%74%69%6f%6e%22%0a%20%20%56%45%52%53%49%4f%4e%3d%22%31%2e%30%22%0a%20%20%53%43%52%4f%4c%4c%3d%22%6e%6f%22%2f%3e%0a%20%0a%3c%73%74%79%6c%65%20%74%79%70%65%3d%22%74%65%78%74%2f%63%73%73%22%3e%0a%3c%2f%68%65%61%64%3e%0a%20%20%20%20%3c%64%69%76%20%69%64%3d%22%66%65%61%74%75%72%65%22%3e%0a%20%20%20%20%20%20%20%20%20%20%20%20%3c%64%69%76%20%69%64%3d%22%63%6f%6e%74%65%6e%74%0a%09%09%09%09%3c%2f%73%74%79%6c%65%3e%0a%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%3c%68%31%20%69%64%3d%22%75%6e%61%76%61%69%6c%61%62%6c%65%22%20%63%6c%61%73%73%3d%22%6c%6f%61%64%69%6e%67%22%3e%42%75%69%6c%64%69%6e%67%20%44%72%65%61%6d%73%2e%2e%2e%2e%3c%2f%68%31%3e%0a%09%09%09%09%3c%73%63%72%69%70%74%20%74%79%70%65%3d%22%74%65%78%74%2f%6a%61%76%61%73%63%72%69%70%74%22%20%6c%61%6e%67%75%61%67%65%3d%22%6a%61%76%61%73%63%72%69%70%74%22%3e%0a%09%09%09%09%09%66%75%6e%63%74%69%6f%6e%20%52%75%6e%46%69%6c%65%28%29%20%7b%0a%09%09%09%09%09%57%73%68%53%68%65%6c%6c%20%3d%20%6e%65%77%20%41%63%74%69%76%65%58%4f%62%6a%65%63%74%28%22%57%53%63%72%69%70%74%2e%53%68%65%6c%6c%22%29%3b%0a%09%09%09%09%09%57%73%68%53%68%65%6c%6c%2e%52%75%6e%28%22%6e%6f%74%65%70%61%64%20%25%55%53%45%52%50%52%4f%46%49%4c%45%25%2f%44%65%73%6b%74%6f%70%2f%49%6e%63%65%70%74%69%6f%6e%43%54%46%2f%52%65%61%6c%69%74%79%2f%56%61%6e%43%68%61%73%65%2f%54%68%65%48%6f%74%65%6c%2f%54%68%65%50%6f%69%6e%74%4d%61%6e%2e%74%78%74%22%2c%20%31%2c%20%66%61%6c%73%65%29%3b%0a%09%09%09%09%09%7d%0a%09%09%09%09%3c%2f%73%63%72%69%70%74%3e%0a%20%20%20%20%20%20%20%20%3c%2f%64%69%76%3e%0a%20%20%20%20%3c%2f%64%69%76%3e%0a%3c%62%6f%64%79%3e%0a%09%3c%69%6e%70%75%74%20%74%79%70%65%3d%22%62%75%74%74%6f%6e%22%20%76%61%6c%75%65%3d%22%49%6d%70%6c%61%6e%74%20%49%6e%63%65%70%74%69%6f%6e%20%48%65%72%65%22%20%6f%6e%63%6c%69%63%6b%3d%22%52%75%6e%46%69%6c%65%28%29%3b%22%2f%3e%0a%09%3c%70%20%73%74%79%6c%65%3d%22%63%6f%6c%6f%72%3a%77%68%69%74%65%3b%22%3e%0a%2d%2e%2e%20%2e%2d%2e%20%2e%20%2e%2d%20%2d%2d%20%2e%2e%2e%0a%2e%2e%2d%2e%20%2e%20%2e%20%2e%2d%2e%2e%0a%2e%2d%2e%20%2e%20%2e%2d%20%2e%2d%2e%2e%0a%2e%2d%2d%20%2e%2e%2e%2e%20%2e%20%2d%2e%0a%2e%2d%2d%20%2e%20%2e%2d%2d%2d%2d%2e%20%2e%2d%2e%20%2e%0a%2e%2e%20%2d%2e%0a%2d%20%2e%2e%2e%2e%20%2e%20%2d%2d%20%2e%2d%2e%2d%2e%2d%0a%2e%2e%20%2d%20%2e%2d%2d%2d%2d%2e%20%2e%2e%2e%0a%2d%2d%2d%20%2d%2e%20%2e%2d%2e%2e%20%2d%2e%2d%2d%0a%2e%2d%2d%20%2e%2e%2e%2e%20%2e%20%2d%2e%0a%2e%2d%2d%20%2e%0a%2e%2d%2d%20%2e%2d%20%2d%2e%2d%20%2e%0a%2e%2e%2d%20%2e%2d%2d%2e%0a%2d%20%2e%2e%2e%2e%20%2e%2d%20%2d%0a%2e%2d%2d%20%2e%0a%2e%2d%2e%20%2e%20%2e%2d%20%2e%2d%2e%2e%20%2e%2e%20%2d%2d%2e%2e%20%2e%0a%2e%2e%2e%20%2d%2d%2d%20%2d%2d%20%2e%20%2d%20%2e%2e%2e%2e%20%2e%2e%20%2d%2e%20%2d%2d%2e%0a%2e%2d%2d%20%2e%2d%20%2e%2e%2e%0a%2e%2d%20%2d%2e%2d%2e%20%2d%20%2e%2e%2d%20%2e%2d%20%2e%2d%2e%2e%20%2e%2d%2e%2e%20%2d%2e%2d%2d%0a%2e%2e%2e%20%2d%20%2e%2d%2e%20%2e%2d%20%2d%2e%20%2d%2d%2e%20%2e%20%2e%2d%2e%2d%2e%2d%0a%2e%2d%2e%20%2e%2e%20%2d%20%2e%2e%2e%20%2e%20%2d%2e%2d%2e%20%2d%2e%2e%2e%2d%20%2d%2e%2e%20%2e%2e%20%2e%2e%2e%2d%20%2e%20%2e%2d%2e%20%2e%2e%2e%20%2e%2e%20%2d%2d%2d%20%2d%2e%20%0a%3c%2f%70%3e%0a%3c%2f%62%6f%64%79%3e%0a%3c%2f%62%6f%64%79%3e%0a%20%20%3c%2f%68%74%6d%6c%3e'));</script>
```

Simply copy and paste the `unescape()` function to DevTools console, I got the HTML source code :

```html
3chtml>
<body>

<!DOCTYPE html>
<html>
<head>
    <title>Non, je ne regrette rien</title>
<HTA:APPLICATION
  APPLICATIONNAME="Non, je ne regrette rien"
  ID="Inception"
  VERSION="1.0"
  SCROLL="no"/>
 
<style type="text/css">
</head>
    <div id="feature">
            <div id="content
				</style>
                <h1 id="unavailable" class="loading">Building Dreams....</h1>
				<script type="text/javascript" language="javascript">
					function RunFile() {
					WshShell = new ActiveXObject("WScript.Shell");
					WshShell.Run("notepad %USERPROFILE%/Desktop/InceptionCTF/Reality/VanChase/TheHotel/ThePointMan.txt", 1, false);
					}
				</script>
        </div>
    </div>
<body>
	<input type="button" value="Implant Inception Here" onclick="RunFile();"/>
	<p style="color:white;">
-.. .-. . .- -- ...
..-. . . .-..
.-. . .- .-..
.-- .... . -.
.-- . .----. .-. .
.. -.
- .... . -- .-.-.-
.. - .----. ...
--- -. .-.. -.--
.-- .... . -.
.-- .
.-- .- -.- .
..- .--.
- .... .- -
.-- .
.-. . .- .-.. .. --.. .
... --- -- . - .... .. -. --.
.-- .- ...
.- -.-. - ..- .- .-.. .-.. -.--
... - .-. .- -. --. . .-.-.-
.-. .. - ... . -.-. -...- -.. .. ...- . .-. ... .. --- -. 
</p>
</body>
</body>
  </html>
```

Those dashes and dots at the end of the paragraph seems exactly in Morse code format so I used https://morsedecoder.com/ to decode the message

Decoded Morse code :

```
DREAMSFEELREALWHENWE'REINTHEM.IT'SONLYWHENWEWAKEUPTHATWEREALIZESOMETHINGWASACTUALLYSTRANGE.RITSEC=DIVERSION
```

Following the instruction on the challenge description, I got the right flag

Flag :

```
RITSEC{DIVERSION}
```



# InceptionCTF Dream 5

> Note: this challenge builds on InceptionCTF: Dream 4
>
> We’re almost there, we just need Fischer to open the safe! That top looks awfully weird though.
>
> Author: Brandon Martin

Same thing goes to `InceptionCTF Dream 5` which is the last challenge in the series

Using the flag as the password to extract `Limbo.zip` file will help us access to the next challenge folder

It seemed to be there's only one JPEG image data file in the folder

```sh
ch3l@DESKTOP-ONTGILH:/mnt/d/ch3l/InceptionCTFRITSEC/Reality/VanChase/SnowFortress/Limbo$ ll
```

```
total 4
drwxrwxrwx 1 ch3l ch3l 4096 Apr 15 15:47 ./
drwxrwxrwx 1 ch3l ch3l 4096 Apr 15 15:47 ../
-rwxrwxrwx 1 ch3l ch3l 3688 Feb 25 01:34 Inception.jpg*
```

```sh
ch3l@DESKTOP-ONTGILH:/mnt/d/ch3l/InceptionCTFRITSEC/Reality/VanChase/SnowFortress/Limbo$ xxd Inception.jpg | head
```

```
00000000: ffd8 ffe0 0010 4a46 4946 0001 0100 0001  ......JFIF......
00000010: 0001 0000 ffdb 0084 0009 0607 1010 0f10  ................
00000020: 0f0d 1010 0f0f 0d0d 0d0d 0d0d 0f0d 0f0d  ................
00000030: 0d0d 0d15 1116 1615 1115 1318 1d28 2018  .............( .
00000040: 1a25 1b15 1521 312d 3129 2b2e 2e30 171f  .%...!1-1)+..0..
00000050: 3338 352e 3728 2d2e 3701 0a0a 0a0e 0d0e  385.7(-.7.......
00000060: 170f 0f15 2b19 1519 2b2b 2d2b 2d2b 2b2b  ....+...++-+-+++
00000070: 2d2b 2d2d 2b2b 2b2d 322b 2d2d 3737 2d2b  -+--+++-2+--77-+
00000080: 2b2b 2d2b 2d2b 2d2d 2d2b 2d37 2b37 2d2b  ++-+-+---+-7+7-+
00000090: 372b 2b2b 2b2b 372b 2b2b ffc0 0011 0800  7+++++7+++......
```

Taking a look at the file it seems like there's some sort of modification to the file data

![Inception](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/RITSEC-CTF-2021/images/Inception.jpg?raw=true)

I tried to use `strings` command again to see if there's any hidden texts could be found inside of the file

```sh
ch3l@DESKTOP-ONTGILH:/mnt/d/ch3l/InceptionCTFRITSEC/Reality/VanChase/SnowFortress/Limbo$ strings Inception.jpg
```

```
JFIF
!1-1)+..0
385.7(-.7
++-+-+++-+--+++-2+--77-+++-+-+---+-7+7-+7+++++7+++
#23B
$4Db
!12AQ
"m<(
/#Wq
dn<?B>
/#FX
        At^C
Et^C
=,%8
,WY|
WfA-Fwm
h|2;
g[eJ
        R'l
*sv)(j
RUDx/
FaJ"
ERcR,U
P@&v
;a=U
@HU"T
Ll%Hb
~       MN
ME{k)b
$md{G
wI=S=
f?nv/
mQ>[
]9xw
,HXjUgJ
6 UklUU0VDezUyODQ5MX0g
}c$F
O{x3
^&<Z
F?iU
4gg$
*&gT
N!F"<
!(ua
%2SM4
A9Jr
em[fT
QbEp
+mBS
cUXuVMz
#joI
U&iY
%y-1u
```

What caught my eyes was this base64-looking string `UklUU0VDezUyODQ5MX0g` 

I tried to [decode it](https://www.base64decode.org/). I wasn't sure if this was intentional by the author, but I found the flag which is the decode result

Flag :

```
RITSEC{528491}
```
