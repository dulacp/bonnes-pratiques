# Conseils pour utiliser git

## Nouvelle version du projet

### Récupérer les dernières informations du serveur git

récupération des nouveautés depuis le serveur 
> si la console n'affiche rien c'est qu'il n'y a pas eu de modifications
```sh
$ git fetch <nom du remote>
```

afficher l'arbre des modifications
> pour par exemple voir les grandes lignes des modifications apportées (et voir qui les a réalisé)
```sh
$ git hist 
```

## Alias utiles

### hist

la commande `$ git logs` n'est pas très user-friendly, on peut donc préférer l'alias suivant à définir
dans le fichier `~/.gitconfig`
```sh
$ git config --global alias.hist="log --graph --all --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(bold white)— %an%C(reset)%C(bold yellow)%d%C(reset)' --abbrev-commit --date=relative"
```

## Workflows habituels

### Pusher des modifications vers le serveur 

1. Identifier l'état du repository local (quels sont les fichiers modifiers, ceux prêt à être commités, etc)
```sh
$ git status
```

2. Ajouter les fichier à "commiter"
> la commmande `$ git add .` permet d'ajouter tous les fichiers modifiers pour le prochain commit
> **MAIS** il est préférable, quand cela est possible (cf. Mauvaises habitudes)
```sh
$ git add chemin/vers/le/fichier/ou/dossier/a/ajouter
```

3. Réaliser le commit
```sh
$ git commit
```

Cela ouvrira un fichier contenant les informations du commit (sous l'éditeur par défaut configuré, cad vim le plus souvent, ou nano sur certains ubuntu)

* Enregistrer le fichier aura pour conséquence de finaliser le commit
* Quitter le fichier sans enregistrer annulera le commit

4. Contrôler le commit
```sh
$ git hist
```

5. pusher les commits ajoutés sur le serveur git
```sh
$ git push <nom du remote> <nom de la branche>
```
> pour Github, le plus souvent ça s'écrira donc `$ git push origin master`
> pour Heroku cette commande prend la forme `$ git push heroku <nom de la branche>` puisque le remote responsable de recevoir le push s'appelle 'heroku' (par défaut)

### Importer les nouveaux commits depuis le serveur

#### Télécharger les données
```sh
$ git fetch <nom du remote>
```

#### Fusionner les modifications
Pour fusionner les modifications apportées à une branche `X` dans la branche `Y`, on doit d'abord s'assurer que la branche `Y` soit bien la branche courante
```sh
$ git checkout Y
```

On est maintenant en mesure de fusionner les modifications que contient la branche X dans notre branche Y
```sh
$ git merge X
```

## Tips & Tricks

1. Création d'une nouvelle branche
```sh
$ git branch <nom de la branche>
```

2. Changement de branche
```sh
$ git checkout <nom de la branche>
```

3. Informations sur les branches
Seulement les branches locales
```sh
$ git branch
```

Les branches sur tous les remotes
```sh
$ git branch -r
```

4. renomer une branche 
```sh
$ git branch -m <nom de la branche actuellement> <nouveau nom de la branche>
```
