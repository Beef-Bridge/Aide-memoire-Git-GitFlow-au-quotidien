# Modifier le message du dernier commit effectué (no pushed)

Si à un moment donné, je me rédige une erreur dans le message de mon commit, j'ai la possibilité de changer le message de ce dernier commit.

>**Note** : La modification du message de commit démontrée ici, **ne fonctionnne que pour les _commit_ non publiés !**

Pour cela, je lance la commande suivante :
```sh
$ git commit --amend -m "mon nouveau message corrigé"
$ git push
```
