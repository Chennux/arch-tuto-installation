   * [Annexe dédiée à la configuration du réseau](#annexe-dédiée-à-la-configuration_du-réseau)
      * [I) Configurer une connexion Wi-Fi](#i-configurer-une-connexion-wi-fi)<br>
      * [II) Configurer le réseau derrière un serveur proxy](#ii-configurer-le-réseau-derrière-un-serveur-proxy)
      * [III) Se connecter au média d'installation via SSH](#iii-installons-lenvironnement-de-bureau)<br>


Annexe dédiée à la configuration du réseau
=================================================

I) Configurer une connexion Wi-Fi
------------------------------------

Sur les dernières versions de l'image d'installation d'ArchLinux, la connexion au réseau Wi-Fi se configure comme ceci :

On lance l'utilitaire permettant d'établir la connexion sans fil :

```
iwctl
```

Une fois dans iwctl, on liste les cartes Wi-Fi disponibles :

```
device list
```

Ensuite, après identification de la bonne carte Wi-Fi (dans notre exemple, wlan0), on scanne à la recherche de réseaux puis les listons :

```
station wlan0 scan
station wlan0 get-networks
````

Enfin, pour se connecter à son réseau :

```
station wlan0 connect NOM-DU-RÉSEAU
```

Pour quitter iwctl, on saisit simplement :

```
exit
``` 

**Note :** Il peut être nécessaire de "débloquer" la carte réseau que l'on souhaite utiliser. Ce peut être notamment le cas si on s'aperçoit que notre carte réseau a la propriété "Powered" à "off".

Si c'est le cas, on sort de iwctl et on liste les interfaces réseau avec la commande suivante :

```
rfkill list
```
Si la carte réseau est "soft-blocked", il est possible de la débloquer avec la commande suivante (pour l'interface wlan, à adapter selon celle que l'on souhaite débloquer) :

```
rfkill unblock wlan
```

II) Configurer le réseau derrière un serveur proxy
------------------------------------------------------

Si vous êtes derrière un serveur proxy, il suffit de saisir la ligne suivante en la complétant avec les bonnes valeurs. Merci à Nicolas pour l'info :)

```
export http_proxy=http://leproxy:leport/
```

III) Se connecter au média d'installation via SSH
-----------------------------------------------------------------

Suggestion de **Dolorem :** si vous souhaitez utiliser SSH, voici la procédure à suivre :  
On définit d'abord un mot de passe au superutilisateur :

```
passwd
```

Pour obtenir l'ip locale :

```
ip a
```

On lance le service ssh :

```
systemctl start sshd
```

Vous pouvez désormais vous connecter en ssh à votre machine.
