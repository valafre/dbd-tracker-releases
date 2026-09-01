# DBD Tracker — binaires

Ce depot ne contient pas de code source : il sert uniquement a distribuer les
versions installables de DBD Tracker et les fichiers dont la mise a jour
automatique a besoin. Le code vit dans un depot separe.

## Installer

Prends le fichier de la derniere version dans l'onglet **Releases**.

| Fichier | A quoi il sert |
| --- | --- |
| `DBD-Tracker-Setup-<version>.exe` | Installation classique. Se met a jour toute seule. |
| `DBD-Tracker-<version>-portable.exe` | Sans installation. A remplacer a la main pour mettre a jour. |
| `latest.yml` | Lu par les applications installees pour detecter une nouvelle version. |
| `.blockmap` | Permet de ne telecharger que ce qui a change d'une version a l'autre. |

Windows affichera un avertissement SmartScreen : l'application n'est pas signee
par un certificat payant. *Informations complementaires* puis *Executer quand
meme*.

Les donnees vivent dans `%APPDATA%` : une reinstallation ou une mise a jour ne
les efface jamais.

## Publier une version

Les versions sont compilees par GitHub Actions depuis le depot du code, a
chaque tag `v*`. Elles arrivent ici **en brouillon**, jamais publiees
directement : c'est volontaire, cela laisse le temps de relire avant de
diffuser a tout le monde.

Un brouillon est invisible pour les applications installees — l'API GitHub ne
le renvoie pas comme derniere version, et elles affichent « aucune version
publiee ». Il reste donc une etape manuelle :

1. ouvrir le brouillon et verifier que `latest.yml` figure parmi les fichiers ;
2. mettre *Release label* sur **None** — une pre-release n'est jamais proposee
   comme derniere version, elle serait ignoree tout aussi silencieusement ;
3. cliquer **Publish release**.

Les applications deja installees proposent la mise a jour dans les six heures,
ou immediatement via *Parametres -> Rechercher une mise a jour*.

## Pourquoi un depot separe

Le code reste prive. Pour interroger un depot prive, l'application doit
presenter un jeton, et ce jeton est lisible par toute personne qui recoit le
`.exe`. Il est donc en **lecture seule** et limite a ce depot-ci : s'il fuite,
il ne donne acces qu'aux executables deja distribues, jamais au code source.
