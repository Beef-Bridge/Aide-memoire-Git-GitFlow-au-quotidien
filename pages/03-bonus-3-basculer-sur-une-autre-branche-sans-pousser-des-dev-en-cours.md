# Bonus 3 : Basculer sur une autre branche sans pousser des dev en cours

Si durant mon développement j'ai besoin, pour une raison ou une autre, de basculer sur une autre branche alors que j'ai des fichiers modifiés non poussés (car ils ne sont pas encore aboutis, par exemple), je peux mettre ces fichiers de coté, en gardant leur états actuels grace à la commande `git stash`.

Exemple :
Je suis entrain de travailler sur une feature (`feature/toto`) avec un certain nombre de fichiers créés/modifiés, lorsque tout d'un coup je dois basculer sur une autre branche (`master`) afin d'effectuer un hotfix. 
Mon travaille n'est pas dans un état assez avancé pour pouvoir les publier sur ma branche, je vais donc les mettre de coté, basculer sur `master` pour faire ce qu'on attends de moi et revenir sur ma feature, et récupérer mes développements que j'ai mis de coté plutot :
```sh
mon-poste:bibi$ /Users/bibi/Workspaces/projets/mon-projet > feature_toto ✘ ✹ ✭
# Vérification du status de ma branche actuelle
# J'ai des fichiers modifié/créé encours
$ git status

# Je créé mon stash qui va capter et mettre de coté tous ses fichiers
mon-poste:bibi$ /Users/bibi/Workspaces/projets/mon-projet > feature_toto ✘ ✹ ✭
$ git stash
saved working directory

# Contrôle de la bonne création du stash (avec mon travaille)
mon-poste:bibi$ /Users/bibi/Workspaces/projets/mon-projet > feature_toto ✔
$ git stash list

# Vérification du status de ma branche actuelle
# Je n'ai plus aucun fichier modifié/créé encours
mon-poste:bibi$ /Users/bibi/Workspaces/projets/mon-projet > feature_toto ✔
$ git status

# Bascule sur ma branche master pour effectuer la tache urgente
mon-poste:bibi$ /Users/bibi/Workspaces/projets/mon-projet > feature_toto ✔
$ git checkout master

...

# Je reviens sur ma feature pour reprendre le cours de mon développement
mon-poste:bibi$ /Users/bibi/Workspaces/projets/mon-projet > master ✔
$ git checkout feature/toto

# Comme je n'ai que un stash disponible, je récupère le seul stash présent
mon-poste:bibi$ /Users/bibi/Workspaces/projets/mon-projet > feature_toto ✔
$ git stash pop

# Vérification du status de ma branche actuelle
# Les fichiers créés/modifiés durant mon développement sont de retour sur ma branche
mon-poste:bibi$ /Users/bibi/Workspaces/projets/mon-projet > feature_toto ✘ ✹ ✭
$ git status

# Je contrôle la liste des stash présents
# Mon stash n'est plus présent car il a été utilisé
mon-poste:bibi$ /Users/bibi/Workspaces/projets/mon-projet > feature_toto ✘ ✹ ✭
$ git stash list
`````



