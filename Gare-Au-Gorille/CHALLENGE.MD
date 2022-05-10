# Gare Au Gorille
![Chall](https://github.com/Numb3rsProprety/FCSC2022/blob/main/Gare-Au-Gorille/gareaugorille.PNG?raw=true)


- Category: `Web`
- Points: `490` => `101`
- Difficulty: :star:
- Solves: `300`


**Description**

> J'ai construit un site sans prétention pour stocker ma collection de memes !
>
> `https://gare-au-gorille.france-cybersecurity-challenge.fr/` 
>
>


**Attachments**

- `none`

### :book: Introduction

 Ce CTF etait plutot interessant et introduisait une faille que j'avait assez peu experimente auparavant

**Recon**

- Lors de l'arrivee sur le site on remarque un field pour chercher des memes



### :arrows_counterclockwise: Reversing the program

We can starts analyzing the binary with some utilities:

```
$ file formatage
formatage: ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, interpreter /home/n7student/Documents/CTF/FCSC2022/pwn/formatage/lib/ld-2.34.so, BuildID[sha1]=39a11f9a8688c39d7943b084fb7a6f81617573b9, for GNU/Linux 3.2.0, stripped

The remote exploit takes some time, as we need to bruteforce 12 bits of ASLR to get a valid `printf` return address pointer.



Flag: `FCSC{8f1038be95c111447ed7a77492a7c03d465439119c084cf8d867e2d9b8bafcc4}`


```
### :checkered_flag: Conclusion

`formatage` was a very cool challenge about format strings, that really helped me to deeply understand the tricks about format string vulnerabilities. Thanks to its creator!
