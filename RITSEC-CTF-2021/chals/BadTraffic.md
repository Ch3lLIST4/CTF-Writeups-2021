# BadTraffic

> **Please DO NOT attempt to reset the password for any accounts or social engineer the characters. We have taken action to prevent this in the future and your activity will likely be flagged as malicious by the account providers.**
>
> **Please DO NOT like, follow, connect with, or contact any characters on any platforms. You will not get a response and it will not help you solve the challenge.**
>
> That APT might’ve compromised our networks. We’ve included a PCAP of suspicious activity. What tool is the APT using to steal data? (Wrap the answer in RS{})Author: frozen tundras
>
> [ bad_traffic.pcapng](https://ctf.ritsec.club/files/e2aa32b05377dc714cbe6a0c9c9ceeac/bad_traffic.pcapng?token=eyJ1c2VyX2lkIjo0NzksInRlYW1faWQiOjMwMywiZmlsZV9pZCI6NTB9.YHbrzw.ViPYrsQrxRFbqa8LzvT3Ds4knRE)



In this final OSINT challenge, I needed to investigate the captured network traffic from a pcap file. My go-to tool for this type of network forensics would be Wireshark

![image-20210414205840483](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/RITSEC-CTF-2021/images/BadTraffic-1.png?raw=true)

DNS was the protocol that had the most strange and suspicious network traffics. These encoded queries included very sensitive strings like `shadow`, `group` and `passwd`

![image-20210414210530594](https://github.com/Ch3lLIST4/CTF-Writeups-2021/blob/main/RITSEC-CTF-2021/images/BadTraffic-2.png?raw=true)

I tried to follow and take a look closer some of the DNS query messages. This specific one for example

```
... ........:H4sICLVOVGAAA3NoYWRvdwB9lMtOAzEMRff8RaWukII6QmVo9qx4CcoCs-:UGeiZkxkxdx0mn/npZdpZhsz/Xr2koKIeuFbm7Xmxu90pvT063W*sIAuu-:D1pW7a9ro9Zx0JgA8sAd/XyQAOhSAHQhkbpQCydeJxFoqU0gvZYgr7Qx3-:N86wMZBDsgX4qQlJLnOuEkuSQhyw070MXjNDjcRcZnVEe8xzS9L8oIQe7-.shadow.......).........
........[.............:H4sICLVOVGAAA3NoYWRvdwB9lMtOAzEMRff8RaWukII6QmVo9qx4CcoCs-:UGeiZkxkxdx0mn/npZdpZhsz/Xr2koKIeuFbm7Xmxu90pvT063W*sIAuu-:D1pW7a9ro9Zx0JgA8sAd/XyQAOhSAHQhkbpQCydeJxFoqU0gvZYgr7Qx3-:N86wMZBDsgX4qQlJLnOuEkuSQhyw070MXjNDjcRcZnVEe8xzS9L8oIQe7-.shadow.......).........
........[..........<......
```

It seems like this APT group relating to Geno's missing was using DNS traffics to exfiltrate valuable data (the Unix system files, specifically `passwd` and `shadow` files)

For this challenge, the author wants us to identify that mysterious hacking tool that was being used by the APT group to exfiltrate server data. I tried google dorking with these keywords and found various different tools related to this technique such as `dnsfilexfer `, `DNSExfiltrator`, `dnscat`, ... However, none of them was likely the answer

After quite a few guesses and a bit of time reading articles, a friend of mine [daPwn](https://ctf.ritsec.club/teams/334) successfully found the correct answer which is `DNSteal` 

Source code : https://github.com/m57/dnsteal

One of the related article : https://www.hackingarticles.in/data-exfiltration-using-dnssteal/

We think this was a bit guessy of a challenge and solution, but we got the flag anyways

Flag :

```
RS{DNSteal}
```