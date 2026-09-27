# neurobeats-releases

Artefacts publiés de [NeuroBeats](https://neurobeats.site) — lecteur audio
local, gratuit, sans compte.

Ce dépôt ne contient **pas** les fichiers : il est vide par conception. Les
artefacts pèsent jusqu'à 380 Mo, et GitHub refuse tout fichier de plus de
100 Mo dans un dépôt. Ils sont donc dans les **Releases**, dont la limite est
de 2 Go par asset.

## Où trouver quoi

Les binaires sont des assets de release, téléchargeables directement :

- Linux : [`NeuroBeats-0.1.0-x86_64.AppImage`](../../releases/latest) — un seul fichier à rendre exécutable
- Windows : `NeuroBeats-0.1.0-win-setup.exe` — installateur classique
- Android : `NeuroBeats-0.1.0.apk` — Android 10 ou plus récent

Le manifeste des versions, qui porte la version, les tailles et les empreintes
SHA-256 de chaque artefact, est lui aussi un asset, à une URL stable :

```
https://github.com/sylvainmg/neurobeats-releases/releases/latest/download/versions.json
```

Le mot `latest` est un alias que GitHub recalcule : l'adresse ne change pas
d'une version à l'autre.

## Vérifier un téléchargement

L'application refuse d'installer un fichier dont l'empreinte ne correspond pas
au manifeste. C'est une garantie, pas une contrainte : si le transport altère un
octet, vous obtenez un message d'échec clair plutôt qu'un exécutable d'origine
inconnue.

```bash
curl -sL https://github.com/sylvainmg/neurobeats-releases/releases/latest/download/versions.json \
  | python3 -c "import json,sys; print(json.load(sys.stdin)['artifacts']['linux-x64']['sha256'])"
```

Comparez cette valeur au `sha256sum` du fichier téléchargé.

## À propos de l'APK

L'APK est signé avec la clé de distribution du projet, ce qui lui permet de se
mettre à jour tout seul : Android refuse d'installer un paquet signé par une
autre clé que celle de l'application déjà installée. Un APK signé avec une clé de
debug s'installe, mais ne peut jamais être mis à jour.

## Code source

Le code est dans le dépôt principal : https://github.com/sylvainmg/neurobeats
