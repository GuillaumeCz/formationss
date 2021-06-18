# Test Driven Development

## 21/05/2021

Avant ça parlait de `Test first dev` (TFD), ce qui correspond à la rédaction de l'intégralité des tests avant de faire le dev. C'est une méthode de validation de feature avec le client via la rédaction de tests.

- Les plus: Cas de test / definitions claires + couverture pas mal
- Les moins: Necessite un gros investissement et faire preuve de rigueur

Le test driven dev (TDD) est une approche du TFD. ça reprend l'idée d'écrire un test avant le dev + une idée d'itération.

3 lois:
- Ecrire un test qui échoue avant l'écriture du code (pour vérifier qu'i fonctionne et que la fonctionnalité à dev n'existe pas), avec une attention particulière sur le message d'erreur (pour ne pas perdre de temps à chercher);
- Ecrire 1 seule assertion à la fois, qui doit faire planter le test (ou la compilation). En gros ça test une fonction / classe inexistante.
- Ecrire le minimum de code possible pour que l'assertion passe au success !

Les plus:
- Bonne couverture
- Diminution des defauts
- Minimalisme

Les moins:
- Peu répendu
- Problèmatiques liées à la maintenance / évolution des tests

Il faut voir le TDD comme une méthode de dev qui se base sur les tests, qui challenge l'archi, intégre les processus de refacto + implémentation du besoin par petites étapes

Quand est il possible de faire du TDD ?
- En début de projet
- Si il existe de base suffisament de tests

Qu'est-ce qui en rend la pratique compliquée ? 
- Quand il n'y a aucun test dans un projet
- Necessité de formation / intégration des méthodologies dans l'équipe
- Etre capable de découper le boulot en petites étapes

### Ecrire un test: Red / Green / Refacto

1. Red

Ecrire un test qui fail. Se concentrer sur le test par rapport à l'exigence, ce qui permet de valider la compréhension des specs / besoins.

Le fait qu'il foire permet de vérifier que le test fonctionne && lisible.

2. Green

Faire en sorte que le test passe avec l'implementation minimum. Go vers la solution la plus rapide et la moins couteuse. 

Permet de check si les autres tests fonctionnent. 

3. Refacto

Amélioration itérative de la maintenabilité / lisibilité du code.

Toujours refacto du vert au vert.

Faire tourner les tests à chaque étape de refacto (d'où l'idée qu'ils doivent pouvoir s'exec rapidement).

Possibilité de refacto du test (en faisant bien gaffe).

Cycle Red -> Green -> Refacto -> Red -> ... doit être le plus court possible (<5min). 

A la fin de chaque cycle --> "Est-ce que ça aurait pu se découper ?"

### Courbe d'apprentissage

TDD necessite un certain apprentissage / temps d'intégration. Ce qui induit une perte de productivité lorsqu'on l'apprend. C'est bien de le faire en groupe.

### Mob programming

Idée de pair programming à plus de 2. 

Les plus: 
- Revue de code en continue
- Bonne pratique
- Synergie de groupe
- Combinaison de competences individuelles

Les moins:
- Peu adapté à des taches simples (c'est plus interessant de splitter)
- C'est fatigant (Penser à faire des pauses)
- Necessite de faire du relationel / desamorçage de conflit parfois

Possibilité de se répartir 2 roles:
- Conducteur: Au clavier
- Navigateur(s): Exposent les idées, observent et revoient le code.

Il existe 3 sous-roles de navigateur:
- Facilitateur: Donne du rythme et vérifie le cap
- Scout: Part à la recherche d'info
- Scribe: En charge de la Todo list


