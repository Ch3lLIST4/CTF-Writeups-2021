# Robots

>Robots are taking over. Find out more.
>
>34.69.61.54:5247
>
>Author: f1rehaz4rd

Taking a look at the site we can find obvious hints like `Robots are Taking Over`, the robot image or even the challenge title itself

I went to http://34.69.61.54:5247/robots.txt and found a lot of rules for URLs :

```
        User-agent: Robot-Queto-v1.2
        Disallow: /search
        Allow: /search/about
        Allow: /search/static
        Allow: /search/howsearchworks
        Disallow: /sdch
        Disallow: /groups
        Disallow: /index.html?
        Disallow: /?
        Allow: /?hl=
        Disallow: /?hl=*&
        Allow: /?hl=*&gws_rd=ssl$
        Disallow: /?hl=*&*&gws_rd=ssl
        Allow: /?gws_rd=ssl$
        Allow: /?pt1=true$
...
        Allow: /flag/UlN7UjBib3RzX2FyM19iNGR9
...
        Disallow: /maps/reserve/partner-dashboard
        Disallow: /about/views/
        Disallow: /intl/*/about/views/
        Disallow: /local/dining/
        Disallow: /local/place/products/
        Disallow: /local/place/reviews/
        Disallow: /local/place/rap/
        Disallow: /local/tab/
        Disallow: /localservices/*
        Allow: /finance
        Allow: /js/
        Disallow: /nonprofits/account/
  
```

I searched for `flag` and found that line of rule in the middle along with a string `UlN7UjBib3RzX2FyM19iNGR9` which I instantly thought was encoded using *base64* encoding

I decoded it using [base64decode site](https://www.base64decode.org/) and found the flag

Flag :

```
RS{R0bots_ar3_b4d}
```

