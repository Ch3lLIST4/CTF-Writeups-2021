# Session

> Find the flag.
>
> [http://34.69.61.54:4777](http://34.69.61.54:4777/)
>
> Author: f1rehaz4rd

The index page is a login page

```html
<html>
<head>
  <title>Iroh - Login</title>
  <!--#remove comment later: login iroh:iroh-->
</head>

<body style="background-color:orange;">
<h2> Login </h2>
<form action="" method="post">
       <input type="text" placeholder="Username" name="username" value="">
        <input type="password" placeholder="Password" name="password" value="">
       <input class="btn btn-default" type="submit" value="Login">
     </form>
     

</body>

</html>
```

Inspecting the source code we found the pair of login credentials `login iroh:iroh` that was accidentally forgot to be removed

After logging in, it looked like just a normal static webpage so I moved on to check for the site cookies, as the challenge title was `Session` and found this pair of cookie values : `sessiontoken=UlN7MG5seV9PbmVfczNzc2lvbl90b2szbn0=`

Looks like a base64 encoded string so all I did was copy and paste in on the decoding site again and got the flag

Flag :

```
RS{0nly_One_s3ssion_tok3n}
```

