# PleaseClickAllTheThings 1

> Note: this challenge is the start of a series of challenges. The purpose of this CTF challenge is to bring real world phishing attachments to the challengers and attempt to find flags (previously executables or malicious domains) within the macros. This is often a process used in IR teams and becomes an extremely valuable skill. In this challenge we’ve brought to the table a malicious html file, GandCrab/Ursnif sample, and a IceID/Bokbot sample. We’ve rewritten the code to not contain malicious execution however system changes may still occur when executing, also some of the functionalities have been snipped and will likely not expose itself via dynamic analysis.
>
> ```
> • Outlook helps, with proper licensing to access necessary features
>     ◦ Otherwise oledump or similar would also help but isn’t necessary
> • CyberChef is the ideal tool to use for decoding
> ```
>
> Part 1: Start with the HTML file and let’s move our way up, open and or inspect the HTML file provide in the message file. There is only one flag in this document.
>
> This challenge is brought to you by SRA
>
> [ Please_Click_all_the_Things.7z](https://ctf.ritsec.club/files/40447a17c9f327c941206ef0c3adb451/Please_Click_all_the_Things.7z?token=eyJ1c2VyX2lkIjo0NzksInRlYW1faWQiOjMwMywiZmlsZV9pZCI6MzV9.YHU8Og.rYV548HbI--zaF9oT-A5AxKt0-A)

After downloading the file, I extracted it and found `Please Click all the Things.msg`. A quick look at the file, I found out that it is a Microsoft Outlook Message file

```bash
ch3l@DESKTOP-ONTGILH:/mnt/d/ch3l/Please_Click_all_the_Things$ ls
```

```
'Please Click all the Things.msg'
```

```bash
ch3l@DESKTOP-ONTGILH:/mnt/d/ch3l/Please_Click_all_the_Things$ file Please\ Click\ all\ the\ Things.msg
```

```
Please Click all the Things.msg: CDFV2 Microsoft Outlook Message
```

I used an online .msg viewer at https://msgeml.com/

I found a short message and 3 attachments inside of the file

![image-20210413134437669](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/RITSEC-CTF-2021/images/PleaseClickAllTheThings-1-1.png?raw=true)

For this first challenge we need to take a look at the `BeginnersRITSEC.html` file

Opening the file I got this weird looking website

![image-20210413134653272](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/RITSEC-CTF-2021/images/PleaseClickAllTheThings-1-2.png?raw=true)

Source code :

```html

<script language="javascript">document.write(unescape('3c%68%74%6d%6c%3e%0a%3c%62%6f%64%79%3e%0a%0a%3c%21%44%4f%43%54%59%50%45%20%68%74%6d%6c%3e%0a%3c%68%74%6d%6c%3e%0a%3c%68%65%61%64%3e%0a%20%20%20%20%3c%74%69%74%6c%65%3e%49%74%73%20%6a%75%73%74%20%61%6e%6f%74%68%65%72%20%66%72%69%65%6e%64%6c%79%20%66%69%6c%65%20%66%72%6f%6d%20%79%6f%75%27%72%65%20%6c%6f%63%61%6c%20%43%54%46%3c%2f%74%69%74%6c%65%3e%0a%20%20%20%20%3c%73%74%79%6c%65%20%74%79%70%65%3d%22%74%65%78%74%2f%63%73%73%22%3e%0a%20%20%20%20%20%20%20%20%68%74%6d%6c%20%7b%0a%20%20%20%20%20%20%20%20%20%20%20%20%68%65%69%67%68%74%3a%20%31%30%30%25%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%77%69%64%74%68%3a%20%31%30%30%25%3b%0a%20%20%20%20%20%20%20%20%7d%0a%0a%20%20%20%20%20%20%20%20%23%66%65%61%74%75%72%65%20%7b%0a%20%20%20%20%20%20%20%20%20%20%20%20%77%69%64%74%68%3a%20%39%38%30%70%78%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%6d%61%72%67%69%6e%3a%20%39%35%70%78%20%61%75%74%6f%20%30%20%61%75%74%6f%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%6f%76%65%72%66%6c%6f%77%3a%20%61%75%74%6f%3b%0a%20%20%20%20%20%20%20%20%7d%0a%0a%20%20%20%20%20%20%20%20%23%63%6f%6e%74%65%6e%74%20%7b%0a%20%20%20%20%20%20%20%20%20%20%20%20%66%6f%6e%74%2d%66%61%6d%69%6c%79%3a%20%22%53%65%67%6f%65%20%55%49%22%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%66%6f%6e%74%2d%77%65%69%67%68%74%3a%20%6e%6f%72%6d%61%6c%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%66%6f%6e%74%2d%73%69%7a%65%3a%20%32%32%70%78%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%63%6f%6c%6f%72%3a%20%23%66%66%66%66%66%66%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%66%6c%6f%61%74%3a%20%6c%65%66%74%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%77%69%64%74%68%3a%20%34%36%30%70%78%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%6d%61%72%67%69%6e%2d%74%6f%70%3a%20%36%38%70%78%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%6d%61%72%67%69%6e%2d%6c%65%66%74%3a%20%30%70%78%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%76%65%72%74%69%63%61%6c%2d%61%6c%69%67%6e%3a%20%6d%69%64%64%6c%65%3b%0a%20%20%20%20%20%20%20%20%7d%0a%0a%20%20%20%20%20%20%20%20%20%20%20%20%23%63%6f%6e%74%65%6e%74%20%68%31%20%7b%0a%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%66%6f%6e%74%2d%66%61%6d%69%6c%79%3a%20%22%53%65%67%6f%65%20%55%49%20%4c%69%67%68%74%22%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%63%6f%6c%6f%72%3a%20%23%66%66%66%66%66%66%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%66%6f%6e%74%2d%77%65%69%67%68%74%3a%20%6e%6f%72%6d%61%6c%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%66%6f%6e%74%2d%73%69%7a%65%3a%20%36%30%70%78%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%6c%69%6e%65%2d%68%65%69%67%68%74%3a%20%34%38%70%74%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%77%69%64%74%68%3a%20%39%38%30%70%78%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%7d%0a%0a%20%20%20%20%20%20%20%20%70%20%61%2c%20%70%20%61%3a%76%69%73%69%74%65%64%2c%20%70%20%61%3a%61%63%74%69%76%65%2c%20%70%20%61%3a%68%6f%76%65%72%20%7b%0a%20%20%20%20%20%20%20%20%20%20%20%20%63%6f%6c%6f%72%3a%20%23%66%66%66%66%66%66%3b%0a%20%20%20%20%20%20%20%20%7d%0a%0a%20%20%20%20%20%20%20%20%23%63%6f%6e%74%65%6e%74%20%61%2e%62%75%74%74%6f%6e%20%7b%0a%20%20%20%20%20%20%20%20%20%20%20%20%62%61%63%6b%67%72%6f%75%6e%64%3a%20%23%30%44%42%43%46%32%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%62%6f%72%64%65%72%3a%20%31%70%78%20%73%6f%6c%69%64%20%23%46%46%46%46%46%46%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%63%6f%6c%6f%72%3a%20%23%46%46%46%46%46%46%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%64%69%73%70%6c%61%79%3a%20%69%6e%6c%69%6e%65%2d%62%6c%6f%63%6b%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%66%6f%6e%74%2d%66%61%6d%69%6c%79%3a%20%53%65%67%6f%65%20%55%49%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%66%6f%6e%74%2d%73%69%7a%65%3a%20%32%34%70%78%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%6c%69%6e%65%2d%68%65%69%67%68%74%3a%20%34%36%70%78%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%6d%61%72%67%69%6e%2d%74%6f%70%3a%20%31%30%70%78%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%70%61%64%64%69%6e%67%3a%20%30%20%31%35%70%78%20%33%70%78%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%74%65%78%74%2d%64%65%63%6f%72%61%74%69%6f%6e%3a%20%6e%6f%6e%65%3b%0a%20%20%20%20%20%20%20%20%7d%0a%0a%20%20%20%20%20%20%20%20%20%20%20%20%23%63%6f%6e%74%65%6e%74%20%61%2e%62%75%74%74%6f%6e%20%69%6d%67%20%7b%0a%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%66%6c%6f%61%74%3a%20%72%69%67%68%74%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%70%61%64%64%69%6e%67%3a%20%31%30%70%78%20%30%20%30%20%31%35%70%78%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%7d%0a%0a%20%20%20%20%20%20%20%20%20%20%20%20%23%63%6f%6e%74%65%6e%74%20%61%2e%62%75%74%74%6f%6e%3a%68%6f%76%65%72%20%7b%0a%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%62%61%63%6b%67%72%6f%75%6e%64%3a%20%23%31%43%37%35%42%43%3b%0a%20%20%20%20%20%20%20%20%20%20%20%20%7d%0a%0a%2f%2a%20%6c%6f%61%64%69%6e%67%20%64%6f%74%73%20%2a%2f%0a%0a%2e%6c%6f%61%64%69%6e%67%3a%61%66%74%65%72%20%7b%0a%20%20%63%6f%6e%74%65%6e%74%3a%20%27%2e%27%3b%0a%20%20%61%6e%69%6d%61%74%69%6f%6e%3a%20%64%6f%74%73%20%31%73%20%73%74%65%70%73%28%35%2c%20%65%6e%64%29%20%69%6e%66%69%6e%69%74%65%7d%0a%0a%40%6b%65%79%66%72%61%6d%65%73%20%64%6f%74%73%20%7b%0a%20%20%30%25%2c%20%32%30%25%20%7b%0a%20%20%20%20%63%6f%6c%6f%72%3a%20%72%67%62%61%28%30%2c%30%2c%30%2c%30%29%3b%0a%20%20%20%20%74%65%78%74%2d%73%68%61%64%6f%77%3a%0a%20%20%20%20%20%20%2e%32%35%65%6d%20%30%20%30%20%72%67%62%61%28%30%2c%30%2c%30%2c%30%29%2c%0a%20%20%20%20%20%20%2e%35%65%6d%20%30%20%30%20%72%67%62%61%28%30%2c%30%2c%30%2c%30%29%3b%7d%0a%20%20%34%30%25%20%7b%0a%20%20%20%20%63%6f%6c%6f%72%3a%20%77%68%69%74%65%3b%0a%20%20%20%20%74%65%78%74%2d%73%68%61%64%6f%77%3a%0a%20%20%20%20%20%20%2e%32%35%65%6d%20%30%20%30%20%72%67%62%61%28%30%2c%30%2c%30%2c%30%29%2c%0a%20%20%20%20%20%20%2e%35%65%6d%20%30%20%30%20%72%67%62%61%28%30%2c%30%2c%30%2c%30%29%3b%7d%0a%20%20%36%30%25%20%7b%0a%20%20%20%20%74%65%78%74%2d%73%68%61%64%6f%77%3a%0a%20%20%20%20%20%20%2e%32%35%65%6d%20%30%20%30%20%77%68%69%74%65%2c%0a%20%20%20%20%20%20%2e%35%65%6d%20%30%20%30%20%72%67%62%61%28%30%2c%30%2c%30%2c%30%29%3b%7d%0a%20%20%38%30%25%2c%20%31%30%30%25%20%7b%0a%20%20%20%20%74%65%78%74%2d%73%68%61%64%6f%77%3a%0a%20%20%20%20%20%20%2e%32%35%65%6d%20%30%20%30%20%77%68%69%74%65%2c%0a%20%20%20%20%20%20%2e%35%65%6d%20%30%20%30%20%77%68%69%74%65%3b%7d%7d%0a%20%20%20%20%3c%2f%73%74%79%6c%65%3e%0a%3c%2f%68%65%61%64%3e%0a%3c%62%6f%64%79%20%62%67%63%6f%6c%6f%72%3d%22%23%30%30%61%62%65%63%22%3e%0a%20%20%20%20%3c%64%69%76%20%69%64%3d%22%66%65%61%74%75%72%65%22%3e%0a%20%20%20%20%20%20%20%20%20%20%20%20%3c%64%69%76%20%69%64%3d%22%63%6f%6e%74%65%6e%74%22%3e%0a%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%3c%68%31%20%69%64%3d%22%75%6e%61%76%61%69%6c%61%62%6c%65%22%20%63%6c%61%73%73%3d%22%6c%6f%61%64%69%6e%67%22%3e%54%72%79%20%48%61%72%64%65%72%3c%2f%68%31%3e%0a%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%3c%70%20%69%64%3d%22%74%72%79%41%67%61%69%6e%22%20%63%6c%61%73%73%3d%22%6c%6f%61%64%69%6e%67%22%3e%54%68%65%20%44%65%66%65%6e%64%65%72%20%54%68%61%74%20%43%6f%75%6c%64%3c%2f%70%3e%0a%20%20%20%20%20%20%20%20%3c%2f%64%69%76%3e%0a%20%20%20%20%3c%2f%64%69%76%3e%0a%3c%2f%62%6f%64%79%3e%0a%0a%0a%20%20%3c%68%65%61%64%3e%20%0a%3c%66%6c%61%67%3d%22%55%6b%6c%55%55%30%56%44%65%30%67%7a%63%6a%4d%68%64%43%45%6b%66%51%3d%3d%22%3e%0a%3c%2f%62%6f%64%79%3e%0a%20%20%3c%2f%68%74%6d%6c%3e'));</script>
```

The site is built using JS DOM and the source code is all encoded

All we need to do is `unescape()` the encoded string using JavaScript itself

Decoded string source code :

```html
3chtml>
<body>

<!DOCTYPE html>
<html>
<head>
    <title>Its just another friendly file from you're local CTF</title>
    <style type="text/css">
        html {
            height: 100%;
            width: 100%;
        }

        #feature {
            width: 980px;
            margin: 95px auto 0 auto;
            overflow: auto;
        }

        #content {
            font-family: "Segoe UI";
            font-weight: normal;
            font-size: 22px;
            color: #ffffff;
            float: left;
            width: 460px;
            margin-top: 68px;
            margin-left: 0px;
            vertical-align: middle;
        }

            #content h1 {
                font-family: "Segoe UI Light";
                color: #ffffff;
                font-weight: normal;
                font-size: 60px;
                line-height: 48pt;
                width: 980px;
            }

        p a, p a:visited, p a:active, p a:hover {
            color: #ffffff;
        }

        #content a.button {
            background: #0DBCF2;
            border: 1px solid #FFFFFF;
            color: #FFFFFF;
            display: inline-block;
            font-family: Segoe UI;
            font-size: 24px;
            line-height: 46px;
            margin-top: 10px;
            padding: 0 15px 3px;
            text-decoration: none;
        }

            #content a.button img {
                float: right;
                padding: 10px 0 0 15px;
            }

            #content a.button:hover {
                background: #1C75BC;
            }

/* loading dots */

.loading:after {
  content: '.';
  animation: dots 1s steps(5, end) infinite}

@keyframes dots {
  0%, 20% {
    color: rgba(0,0,0,0);
    text-shadow:
      .25em 0 0 rgba(0,0,0,0),
      .5em 0 0 rgba(0,0,0,0);}
  40% {
    color: white;
    text-shadow:
      .25em 0 0 rgba(0,0,0,0),
      .5em 0 0 rgba(0,0,0,0);}
  60% {
    text-shadow:
      .25em 0 0 white,
      .5em 0 0 rgba(0,0,0,0);}
  80%, 100% {
    text-shadow:
      .25em 0 0 white,
      .5em 0 0 white;}}
    </style>
</head>
<body bgcolor="#00abec">
    <div id="feature">
            <div id="content">
                <h1 id="unavailable" class="loading">Try Harder</h1>
                <p id="tryAgain" class="loading">The Defender That Could</p>
        </div>
    </div>
</body>


  <head> 
<flag="UklUU0VDe0gzcjMhdCEkfQ==">
</body>
  </html>
```

There's a `<flag="UklUU0VDe0gzcjMhdCEkfQ==">` tag which the value part looks like a base64 encoded string. I tried to [decode it](https://www.base64decode.org/) and of course I found the flag

Flag :

```
RITSEC{H3r3!t!$}
```



