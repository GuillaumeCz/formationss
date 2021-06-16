# Introduction aux tests

## 22/05/2021

Le principal objectif des tests repose dans la detection de bugs, non dans la validation du fonctionnement de l'app. 

> Montrer la présence de bugs et non l'absence...

Il existe differentes alternatives: 
- Relecture: Analyse statique, manuelle, longue et statique.
- Architecture: Identification des potentiels problemes en amont, mais tout n'est pas anticipable et c'est complexe. Il faut trouver le juste milieu entre l'`utilisabilité` et la `testabilité`.
- Preuve formelle: Preuve mathématique de l'absence d'erreur mais très complexe.

Toutes ces alternatives sont complementaires, aucunement exhaustives.

2 grands types de méthode test:
- Manuel: "A la mano", haut niveau, test utilisateur (avec scenario et / ou exploration) MAIS long, non deterministique...
- Automatique: Utilisation d'outils, plus rapide MAIS tout n'est pas testable, ça à un coup et necessite des competences.

Le top --> Mix des deux types, automatiser tout ce qui est automatisable.

Il existe des tonnes de types de tests: composant / intégration / système / acceptation / ...

### Boite noire / blanche

1. Boite noire

Se base sur des critères de couverture (execution / données). Voir ça comme un schema de flux.

"Couverture du flot de control" --> ?

"Couverture du flot de données" --> Suivre la données durant l'ensemble de son cycle de vie (definition, utilisation (calculs, predicats), destruction) 

Souvent à la mano

2. Boite blanche

Check si les specs /exigeances sont remplies. Vise la pertinence au lieu de l'exhaustivité.


En général on commence par la boite blanche et on complète avec boite noire.

Caracteristiques testés:
- Fonctionnelle
- Perf / robustesse
- Secu
- Ergonomie
- ...

La `non-regression` est un usage des tests, et NON un type ! Un test unitaire / d'intégration devient un test de non regression.


Prioriser le `fonctionnel` && `boite noire`, a compléter avec d'autres types de test!

### Bonnes pratiques

- Des noms pertinents pour les tests (savoir direct ce qui pete, sans devoir chercher) 
- Utilisation de variables
- Attention particulière sur le nommage des erreurs
- Structuration de test
```
Given --> Condition préalables au test 
...
When --> Ce qui est testé
...
Then --> Assertions permettant de vérifier les resultats
...
```
- Attention aux tests "pastèques" (vert à l'exterieur, rouge à l'interieur).
- Un test doit se soumettre à un impératif de rapidité, pour pouvoir rapidement le faire tourner et avoir un retour.
- Indépendance des tests entre eux
- L'aléatoire n'est pas un bonne idée... !

Comment savoir si les tests sont suffisants ? 

- Couverture de code (Mesure quantitative, non qualitative)
- Mutation: modification de parties random du code source pour voir si ça plante au bon endroit et tests remontent l'erreur.

Méthode FIRST
- Fast
- Independant / Isolated
- Repetable
- Self validating
- Thorough (Couverture de l'ensemble des cas de tests)

Methode ZOMBIES (cas de tests)
- Zero
- One
- Multiple
- Boundaries (limites)
- Interfaces
- Exeptions (genre, coupure de réseau...) / facteurs externes
- Simple scenario (au plus proche de la réalité)

