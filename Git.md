[Accueil](README.md) [Commandes Git](Git.md) [TypeScript](Typescript.md) 

# Commandes Git

| Commande                              | Description                                                                                                          |
| ------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| git branch NOMBRANCHE                 | Créer branche                                                                                                        |
| git checkout NOMBRANCHE               | Bascule                                                                                                              |
| git branch -d NOMBRANCHE              | Supprimer branche locale                                                                                             |
| git checkout -b NOMBRANCHE            | Créer et Basculer vers branche                                                                                       |
| git add -A                            | Ajoute tous les fichiers en staging                                                                                  |
| git commit -m "commentaire du commit" | Commit les fichiers en staging                                                                                       |
| git log --oneline                     | Historique du dépôt                                                                                                  |
| git push -u origin HEAD               | Pousse la branche courante vers le serveur distant.                                                                  |
|                                       | Après le 1er push un lien est créé entre la branche local et l'origine un git push sera suffisant pour les prochains |
| git fetch                             | Synchro la branche local avec l'origine mais ne se positionne pas sur le dernier commit                              |
| git fetch --prune                     | Synchro avec suppression des branches locales qui n'existent plus à distance (identique à git pull --prune)          |
| git pull                              | Se positionne sur le dernier commit                                                                                  |
| git push -d origin NOMBRANCHE         | Suppression de la branche à distance                                                                                 |
| git rebase master NOMBRANCHE          | Injecte le contenu de la branche dans le master (au dessus des commits précédents)                                   |
| git rebase -i HEAD~2 master           | Rebase sur lui-même avec possibilité de fusionner les commits                                                        |
| git reset HEAD~1                      | Revient en arrière en local sur la branche d'un cran                                                                 |
| git stash "nomdustash"                | Mise de côté du dev en cours                                                                                         |
| git stash pop "nomdustash"            | Réapplique le code mis de côté et supprime le stash                                                                  |
| git stash list                        | Liste les devs mis de côté                                                                                           |
## Revert un commit sur une mauvaise branche
| Commande                                                             | Description                                                                                  |
| -------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| git branche hotfixMauvaiseBranche                                    | Crée une branche qui va porter le commit à la mauvaise cible                                 |
| git reset --hard HEAD~1                                              | Revert le commit                                                                             |
| git push -f                                                          | Pousse le revert sur la branche                                                              |
| git rebase --onto branchecible mauvaisebranche hotfixMauvaiseBranche | rebaser tous les commits après mauvaisebranche jusqu'à horfixmauvaisebranche sur branchcible |
| git checkout branchecible                                            | Bascule sur la bonne branche                                                                 |
| git merge --ff-only hotfixMauvaiseBranche                            | Fusion du hotfix sur la bonne branche                                                        |
| git branch -d hotfixMauvaiseBranche                                  | Suppression de la branche de hotfix                                                          |
## Supprimer les branches locales orphelines de branche distantes 
Prune supprime uniquement les branche du dossier origin local
```ps1
git branch -vv | Select-String -Pattern  ': gone]'  |  % {$_.ToString()} | Select-String -Pattern '(?:\s*)([\w\-\/]*)'| % {$_.Matches}| %{$_.Groups[1]}| %{$_.Value} | % { git branch -D $_}
```


## Rebase vs Merge
  * Rebase est une méthode de travail qui permet de récupérer les commits d'une branche dans une autre.
    * Syntaxe:
        ```
        git rebase <branche>
        git push -f
        ```
    * Avantage : ne duppliquera pas les commits
    * Inconvenient : pas de travail en parallèle sur la même branche (le push -f écrase l'historique)
  * Merge est une méthode de travail qui permet de fusionner les commits d'une branche dans une autre.
    * Syntaxe:
        ```
        git merge <branche>
        git push
        ```
    * Avantage : permet de travailler en parallèle sur la même branche
    * Inconvenient : dupppliquera les commits et ne permet pas une lecture simple de l'historique

# Outils
## Softs
https://git-fork.com/
https://www.sourcetreeapp.com/
## Ligne de commande enrichie : PoshGit

Pour ceux utilisant Git en ligne de commande sous powershell, il existe un utilitaire permettant de connaitre la branche courante, les commits en retard et d'avoir l'intellisense sur les commandes Git 

* Pour l'installer, depuis la ligne de commande  powershell:
```
Install-Module posh-git -Scope CurrentUser
Install-Module oh-my-posh -Scope CurrentUser
```
Optionnel (normalement déjà installé ):
```
Install-Module -Name PSReadLine -Scope CurrentUser
```

* Configuration :
Une fois les modules installés, toujours dans powershell :
```
Notepad $PROFILE
```
Dans le fichier copier le contenu suivant pour activer les modules à chaque ouverture de powershell :
```
Import-Module posh-git
Import-Module oh-my-posh
Set-Theme Paradox
```
Dans la commande, il faut une font + riche que celle par défaut.
Si vous avez déjà fira code ou cascadia code dans VS Code elle doit s'appliquer à la console

Pour le nouveau terminal de MS:
Paramètres=> Ouvre un fichier json de configuration
* Modifier la partie powershell:
```
{
    // Make changes here to the powershell.exe profile.
    "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
    "name": "Windows PowerShell",
    "commandline": "powershell.exe",
    "fontFace": "Cascadia Code PL", <== fira code chez moi, celle-ci c'est celle de ms
    "hidden": false
},
```
