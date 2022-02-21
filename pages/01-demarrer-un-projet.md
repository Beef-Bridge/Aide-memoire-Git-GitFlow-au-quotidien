# Démarrer un projet

La première étape consiste à compléter la branche `master` par défaut avec une branche `develop`.

Pour cela, je créé une branche `develop` vide en local et de la pousse vers le dépot distant :
```sh
# Sans l'extension git-flow :
$ git branch develop
$ git push -u origin develop

# Avec l'extension git-flow :
$ git flow init
Initialized empty Git repository in ~/project/.git/
No branches exist yet. Base branches must be created now.
Branch name for production releases: [main]
Branch name for "next release" development: [develop]


How to name your supporting branch prefixes?
Feature branches? [feature/]
Release branches? [release/]
Hotfix branches? [hotfix/]
Support branches? [support/]
Version tag prefix? []


$ git branch
* develop
 main
```

Ainsi, la branche `master` stockera l'historique officiel des versions publiées, tandis que la branche `develop` contiendra l'historique complet du projet et servira de branche d'intégration pour les fonctionnalités.

Maintenant que les deux branches principales de mon projet sont créées, je peux [commencer son développement](02-commencer-un-developpement.md).