# tbox / t411.sh

Petite boite a outil bash pour t411.

A la premiere utilisation se loguer: `t411 login <user> <password>`<br>
un fichier contenant les cookies d'authentification sera cree et reutilise par la suite.<br>
le fichier de configuration `~/.t411/cookies` sera egalement cree.

Dans le fichier de configurartion `watchDir` permet de definir le repertoire de telechargement des torrents.

Categories supportees pour l'upload: `video/*` `ebook/presse`<br>
Actuellement uniquement teste pour la categorie: `video/emissionTV`

Dependances: `bash` `curl`

Note: teste sur OS X

## Usage

```
login <user> <password>
logout
info
deleteEmail <mailId>
cleanInbox
dl <torrentId | prezUrl> [toDir]
dlm <inputFile> [toDir]
up <dir>
```

### login

A faire la premiere fois.
2 fichiers seront crees:
* `~/.t411/cookies` contient les cookies pour l'authentification
* `~/.t411/conf` fichier de configuration

### info

Affiche: ratio, upload, download, nombre d'email

### cleanInbox

Supprime de la premiere page de la boite de reception les messages: *telechargement complete ...*<br>
Trouve tout son sens dans un cron.

### dl

Telecharge un torrent dans le repertoire:
* `toDir` s'il est specifie
* `watchDir` s'il est specifie dans le fichier de conf
* le repertoire courant

### up

upload / edit un torrent.

Categories supportees: `video/*` `ebook/presse`<br>
Lors d'un upload reussi le torrent sera telecharge dans le repertoire passe en parametre ainsi que dans `watchDir` s'il est specifie dans la conf.<br>
Le repertoire passe en parametre doit contenir 4 fichiers nommes: `torrent` `nfo` `prez` `upload`<br>
La prez doit etre encodee en `windows-1252`<br>
Le fichier `upload` contient les valeurs du formulaire d'upload.<br>
La meme commande permet d'editer un torrent, l'identifiant de celui-ci etant sauve dans le fichier `upload` apres le premier upload. Lors d'une edition le torrent n'est pas retelecharge<br>

**Exemple de fichier `upload` pour une video**
```
nom="Mirabelles et Chocolat s02e07 HDTV tout ca"
categorie=433

## video. categories: 637 639 433 455 634 631 635 633 636 402
video_format=21
video_langue=541
video_qualite=12
video_systeme=684
video_type=22

## video + genre. categories: 637 639 433 455 634 631 635
video_genre="60 54 44"

## video + genre + episode. categories: 637 639 433
video_saison=969
video_episode=943
```

**Exemple  de fichier `upload` pour la presse**
```
nom="Le journal du Lundi 2014.02.15 PDF"
categorie=410
presse_format=1056
presse_langue=729
presse_genre="1124 1015"
```

**Identifiants**
* [Categorie](https://github.com/ylon/tbox/wiki/id-categorie)
* [Formulaire d'upload Video](https://github.com/ylon/tbox/wiki/id-upform-video)
* [Formulaire d'upload Presse](https://github.com/ylon/tbox/wiki/id-upform-presse)
