# lorem ipsum

> ![hint.jpg](https://ctf.ritsec.club/files/7a05d1622690c7b5d5f4b149a0ece3fa/hint.jpg)
>
> Flag is case sensitive.author: raydan
>
> [ cipher.txt](https://ctf.ritsec.club/files/152105ec4b3c4d447fac627d3d80b57d/cipher.txt?token=eyJ1c2VyX2lkIjo0NzksInRlYW1faWQiOjMwMywiZmlsZV9pZCI6NDR9.YHMumA.0avEbFbZxc1ajX1FldT9mx3rCHo)

Opening the text file 

```
Incompraehensibilis Conseruator.
Redemptor optimus
Iudex omnipotens
Sapientissimus omnipotens
Redemptor fabricator
Iudex redemptor
Optimus magnus
Aeternus iudex
Auctor omnipotens.
```

Looks like Latin language. I tried to search those text on Google and found out it was **Trithemius Ave Maria Cipher** along with it's [cipher decoder site](https://www.dcode.fr/trithemius-ave-maria)

| A    | deus, clemens                  | B    | creator,clementissimus    |
| ---- | ------------------------------ | ---- | ------------------------- |
| C    | conditor,pius                  | D    | opifex,piissimus          |
| E    | dominus,magnus                 | F    | dominator,excelsus        |
| G    | consolator,maximus             | H    | arbiter,optimus           |
| I    | iudex,sapientissimus           | K    | illuminator,inuisibilis   |
| L    | illustrator,immortalis         | M    | rector,aeternus           |
| N    | rex,sempiternus                | O    | imperator,gloriosus       |
| P    | gubernator,fortissimus         | Q    | factor,sanctissimus       |
| R    | fabricator,incompraehensibilis | S    | conseruator,omnipotens    |
| T    | redemptor,pacificus            | U    | auctor,misericors         |
| X    | princeps,misericordissimus     | Y    | pastor,conctipotens       |
| Z    | moderator,magnificus           | ß    | saluator,excellentissimus |

Decoding the text I found the string ` RSTHISISTRITHEMIUS` and it should be the flag that we need

Flag :

```
RS{RSTHISISTRITHEMIUS}
```

