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
2. Créer la branche du hotfix: 
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

8. Je poursuis le développement du hotfix et je répète les étapes 4. 5. 6. 7. autant de fois que nécessaire

9. <à venir>