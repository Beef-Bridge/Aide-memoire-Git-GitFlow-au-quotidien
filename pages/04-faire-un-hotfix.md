# Faire un hotfix

Si aucun développement n'est commencé, alors je dois d'abord créer la branche du hotfix (comme indiquer après ci-dessous).



>Note : Dans le cas où du code est déjà écrit mais non commité, il est possible de récupérer les quelques changements déjà apportés dans une autre branche (`develop` par exemple) en utilisant la commande `stash` de Git :
>```sh
># Met de coté les changements déjà opérés
>$ git stash
>```

1. Se placer sur la branche `master` et vérifier qu'elle est parfaitement à jour :
```sh
$ git checkout master
$ git pull --rebase
```
2. Créer la branche du hotfix depuis la branche `master` : 
```sh
$ git checkout -b hotfix_avec_un_joli_nom
```
3. Ecrire le code du hotfix ou récupérer du code précédement écrit et mis de coté avec la commande `stash` :
```sh
# Récupère le code que l'on a mis de coté précédemment
$ git stash pop
```

>Note : Il est possible de retrouver le code mis de coté plutôt parmis une liste de _stash_ :
>```sh
>$ git stash list
>```

4. S'assurer que le code de notre hotfix est bien présent dans la branche de ce dernier :
```sh
$ git status
On branch hotfix_avec_un_joli_nom
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   src/Controller/TestController.php
        modified:   src/Services/TestService.php

no changes added to commit (use "git add" and/or "git commit -a")
```

5. Je commite le développement :
```sh
# Ajoute tous les fichiers modifiés par le développement du hotfix
$ git add .

# Contrôle de l'état des fichiers modifiés avant le commit
$ git status
On branch hotfix_avec_un_joli_nom
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   src/Controller/TestController.php
        modified:   src/Services/TestService.php

# Effectuer le commit
git commit -m "la description de mon commit"
```

6. Je pousse mes changements vers mon repository distant :
```sh
$ git push
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
```

7. Je m'assure que tous mes changements sont bien poussés :
```sh
$ git status
On branch hotfix_avec_un_joli_nom
Your branch is up to date with 'origin/hotfix_avec_un_joli_nom'.
```

8. Je poursuis le développement du hotfix et je répète les étapes 4. 5. 6. 7. autant de fois que nécessaire jusqu'à ce que son développement soit terminé.

9. Je bascule sur ma branche locale `master` et je la mets à jour :
```sh
$ git checkout master
$ git pull --rebase
```

10. Je bascule sur ma branche locale `develop` et je fais de même :
```sh
$ git checkout develop
$ git pull --rebase
```

11. Puis je place le hotfix dans mes branches locales -à jour- `master` et `develop` :
```sh
$ git checkout master
$ git merge hotfix_avec_un_joli_nom

$ git checkout develop
$ git merge hotfix_avec_un_joli_nom
```

Maintenant mes deux branches locales contiennent le hotfix.

12. Je pousse mes deux branches contenant le hotfix sur le dépot distant :
```sh
$ git checkout master
$ git push

$ git checkout develop
$ git push
```

Je contrôle ces deux branches sur le dépot distant, pour voir si elles contiennnent bien le hotfix.

13. Commme c'est le cas, je supprime la branche distante du hotfix `origin/hotfix_avec_un_joli_nom` :
```sh
$ git push origin --delete hotfix_avec_un_joli_nom
```

14. Enfin je supprime cette branche sur mon dépot local :
```sh
$ git branch -D hotfix_avec_un_joli_nom
```