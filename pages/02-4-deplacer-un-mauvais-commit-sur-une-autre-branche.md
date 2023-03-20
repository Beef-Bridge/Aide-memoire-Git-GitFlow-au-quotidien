# Déplacer un mauvais commit, non publié, sur une autre branche

Je viens d'effectuer un commit de mes développements courants sur la branche `develop` en pensant être placé sur ma branche `feature/toto`.
Le commit n'est pas encore pousser sur le dépot distant !

Je souhaite annuler cette action, en déplacant mon commit de ma branche `develop` vers `feature/toto`.

1. Je commece par me placer sur ma branche `develop` :
```sh
$ git checkout develop
````

1. J'identifie le numero du commit que je souhaite déplacer dans une autre branche :
```sh
$ git log --oneline
7be9bf59 (HEAD -> develop) feat: [Sid] WIP modifs
2e59e386 us_feat: [Commun] commande perso pour exposer les routes de l'application
4d40c29e fix: [Common] fix log
bc5657ff Merge branch 'feature/titi' into 'develop'
28ec9c42 fix: [Titi] fix transaction
d395937a feat: [Titi] refacto
1d77709b feat: [Titi] commande d'export + ajout cron
21dd2b5a Merge branch 'curl-sftp-logs' into 'develop'
54972512 [WIP] CURL/FTP/SFTP Logger
e91f306c fix: [Titi] namespace commande
06804073 fix: [Titi] commande import prix epexspot
f0e52ca6 fix: [Tutu] fix merge
fa724b11 Merge branch 'feature/tata' into 'develop'
f82dd0ad feat: [Tata] ajout des AbstractRequest et AbstractRequestService
813275ab feat: [Tata] service spécifique au Rest
9b96d035 feat: [Tata] renommage global Paas
87950e78 feat: [Tata] utilisation du composant Alert
80436435 feat: [Tata] suppression code inutilisé
...
````

Le numéro de mon commit érroné est le suivant : `7be9bf59`.

3. Je bacule sur la branche de ma feature
```sh
$ git checkout feature/toto
````

4. Je déplace le commit qui m'interesse sur ma branche courante (`feature/toto`) en réalisant un cherry-pick :
>Note: le cherry-pick ne peut être réalisé uniquement si la branche `feature/toto` ne contient aucun changement local en cours. Si c'est le cas, il faut soit les envoyés par un commit ou les mettre de coté avec un stash.
```sh
$ git cherry-pick 7be9bf59
[feature/toto 9394b742] feat: [Tutu] WIP modifs    
 Date: Fri Mar 17 15:05:17 2023 +0100
 3 files changed, 511 insertions(+)
 create mode 100644 assets/styles/main.scss 
 create mode 100644 templates/index.html.twig
````

5. Je contrôle la liste de mes commits depuis la branche de ma `feature/toto`
```sh
git log --oneline
9394b742 (HEAD -> feature/tutu) feat: [Tutu] WIP modifs
86c64af7 (origin/feature/tutu) feat: [Tutu] WIP modifs
cd6c6097 feat: [Tutu] expose urls
1501a33e feat: [Tutu] correction
2ae9e509 us_feat: [Tutu] MAJ branche feature/tutu vis à vis de develop
2e59e386 us_feat: [Commun] commande perso pour exposer les routes de l'application
4d40c29e fix: [Common] fix log
bc5657ff Merge branch 'feature/toto' into 'develop'
28ec9c42 fix: [Toto] fix transaction
d395937a feat: [Toto] refacto
1d77709b feat: [Toto] commande d'export + ajout cron
21dd2b5a Merge branch 'curl-sftp-logs' into 'develop'
54972512 [WIP] CURL/FTP/SFTP Logger
b7175aaf feat: [Tutu] modif
````

6. Je vérifie le nouvel état de mes modifs sur la branche de ma feature
```sh
$ git status
On branch feature/toto
Your branch is ahead of 'origin/feature/toto' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
````

Je constate bien que j'ai un commit qu'il me reste à publier sur le dépot distant

7. Je publie le commit que je viens de déplacer sur la branche de ma `feature/toto`
```sh
$ git push
Enumerating objects: 16, done.
Counting objects: 100% (16/16), done.
Delta compression using up to 12 threads
Compressing objects: 100% (9/9), done.
Writing objects: 100% (10/10), 3.28 KiB | 559.00 KiB/s, done.
Total 10 (delta 5), reused 0 (delta 0), pack-reused 0
To https://...
   86c64af7..9394b742  feature/tutu -> feature/tutu
````

1. Je m'assure que le commit récupérer sur ma branche se retrouve bien en tête de liste de mes commits
```sh
git log --oneline
9394b742 (HEAD -> feature/tutu, origin/feature/tutu) feat: [Tutu] WIP modifs
86c64af7 feat: [Tutu] WIP modifs
cd6c6097 feat: [Tutu] expose urls
1501a33e feat: [Tutu] correction
2ae9e509 us_feat: [Tutu] MAJ branche feature/tutu vis à vis de develop
2e59e386 us_feat: [Commun] commande perso pour exposer les routes de l'application
4d40c29e fix: [Common] fix log
bc5657ff Merge branch 'feature/tata' into 'develop'
28ec9c42 fix: [tata] fix transaction
d395937a feat: [tata] refacto
````

1.  Je contrôle la liste de mes commits depuis la branche `develop`
```sh
git log --oneline
7be9bf59 (HEAD -> develop) feat: [Tutu] WIP modifs
2e59e386 us_feat: [Commun] commande perso pour exposer les routes de l'application
4d40c29e fix: [Common] fix log
bc5657ff Merge branch 'feature/toto' into 'develop'
28ec9c42 fix: [Toto] fix transaction
d395937a feat: [Toto] refacto
1d77709b feat: [Toto] commande d'export + ajout cron
21dd2b5a Merge branch 'curl-sftp-logs' into 'develop'
54972512 [WIP] CURL/FTP/SFTP Logger
e91f306c fix: [Toto] namespace commande
06804073 fix: [Toto] commande import prix epexspot
f0e52ca6 fix: [Titi] fix merge
````

On constate que le mauvais commit est toujours présent

10. Je supprime le mauvais commit de ma branche `develop`
```sh
git reset --hard HEAD~1
HEAD is now at 2e59e386 us_feat: [Commun] commande perso pour exposer les routes de l'application
````

11. Je contrôle une derniere fois que le mauvais commit ne soit plus présent sur ma branche `develop`
```sh
git log --oneline
2e59e386 (HEAD -> develop) us_feat: [Commun] commande perso pour exposer les routes de l'application
4d40c29e fix: [Common] fix log
bc5657ff Merge branch 'feature/toto' into 'develop'
28ec9c42 fix: [Toto] fix transaction
d395937a feat: [Toto] refacto
1d77709b feat: [Toto] commande d'export + ajout cron
21dd2b5a Merge branch 'curl-sftp-logs' into 'develop'
54972512 [WIP] CURL/FTP/SFTP Logger
e91f306c fix: [Toto] namespace commande
````

Enjoy!