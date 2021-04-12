# Finding Geno

>We know that our missing person’s name is Geno and that he works for a local firm called Bridgewater. What is his last name? (Wrap the answer in RS{})
>
>Author: t0uc4n

After looking at the challenge all I think of was OSINT People Search Engines. And the first technique that I tried was Google Dorking using `Geno` and `bridgewater` as keywords

After a few tried I found [his profile on Linkedin](https://www.linkedin.com/in/geno-ikonomov), and his last name is `ikonomov`

Flag :

```
RS{ikonomov}
```



# Data Breach

> Oh no! Geno’s email was involved in a data breach! What was his password? Author: t0uc4n

Geno's Linkedin profile gave us a lot of intel especially all of his social medias on http://about.me/genoikonomov, along with the About session :

```
https://about.me/genoikonomov
Email: incogeno@gmail.com
Phone: 1 (845) 702-4914 
```

As the challenge description says, his email `incogeno@gmail.com` was involved in a data breach. So again, I tried Google Dorking with his email as the exact string :

```
"incogeno@gmail.com"
```

![image-20210412001142488](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/RITSEC-CTF-2021/images/DataBreach-1.png?raw=true)

There is the data breach and his leaked password

![image-20210412001307276](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/RITSEC-CTF-2021/images/DataBreach-2.png?raw=true)

Flag :

```
RS{StartedFromTheBottom!}
```



