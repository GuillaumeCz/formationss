# Git - Cours 2/2

## Session du 10/02/2021

### Rebase

Rebase pour "réorganiser un peu les commits", permet de réécrire l'historique d'un repo. 

`-i` --> Mode interactif, choix de ce qu'on veut faire de chaque commit:

- pick: le chope tel quel
- edit: pick + edition du commit 
- squash: fusion avec le commit precedent + edition du message
- fixup: squash sans l'édition du message
- reword: edition du message
- `exec <cmd>`: execution de <cmd> shell (pour execution de test, par exemple)


*** Ne jamais rebase une branche `master/main`.*** 
Ca devient le boxon avec toutes les branches dérivées.


`git rebase -i HEAD~2` --> rebase interactif des 2 derniers commits.

Les commits sont affichés dans une sorte de todolist dans l'orde d'execution / application, l'inverse de celui d'un `git log`.

Pour ajouter des modifications dans un commit<A> passé (qui n'est pas le dernier):

```
git commit --fixup=<A>
```
Ce qui va créer un commit avec le prefix `fixup! <A>`.

```
git commit -i --autosquash ...
```
Squash automatiquement les commits marqués `fixup!`. Plus précisement, Git chope les fixup et les place avant les commits à fixer dans la todolist de rebase et les marque `fixup`.

### Tag

Marqueur de commit. Mode de nommage d'un commit pour rapidement y acceder, "en substitution d'un sha1".

Possibilité de signer un tag w/ GPG ainsi que d'y ajouter un message.

### Stash

Choper modif non stagées et les stocke (temporairement) dans une pile en mode LIFO (Last-In-First-Out).

`git stash` --> Fait rentrer dans la pile, et lui attribue un ID sous la forme `stash@{ID}`.

`git stash apply [stash@{ID}]` --> Applique le stash ID (ou le dernier si !ID).
`git stash pop [stash@{ID}]` --> `apply` et remove le stash ID (ou dernier) de la pile.

### Cherry-pick

"Transplantation de commit". `-x` pour ajouter une ligne dans message du commit cherry-pické pour préciser que c'en est un et d'où il provient.

### Revert

Produit "commit inverse". 

`git revert <ID>` --> Produit EXACTEMENT l'inverse du commit <ID>. Utile pour supprimer une modif sans devoir réecrire un historique.

### Bisect

Méthode d'investigation dichotomique pour trouver le commit qui introduit une regression / bug / ...

Fonctionnement par étape, on lui précise un commit avant l'apparition de l'anomalie et un commit après. Il se charge du reste. 

```
git bisect start
git bisect good <commitSain>  // l'anomalie n'est pas présente
git bisect bad <commitBug> // l'anomalie est présente
```
A chaque étape, Git propose de tester si la modif est présente ou non sur un certain commit.

```
git bisect good // Elle n'est pas présente
```

```
git bisect bad // Elle est présente
```

Il te sort la réponse plutot rapidement ! 

### Git flow

Procédure / ensemble de pratiques qui permettent d'éviter que ça soit le boxon sur le répo. Organisation de projet relativement bien rodée... ! 

### Patch

Ensemble de diff (1..* commits) sous la forme d'un fichier. Ce qui a été utilisé par les anciens avant les systemes de versionnings pour s'échanger des améliorations / dev via mail (d'où l'éxistance de `git am`, `apply mailbox`).


### Hooks

Execution de scripts (non versionnés avec le projet, sauf si utilisation de package comme `Husky`) avec actions git. 

Par exemple en `pre-commit` ou `pre-push` pour faire tourner des tests.

