# Apprentissage-par-Renforcement-avec-l-quation-de-Bellman-sur-GridWorld


## Description

Ce programme implémente un algorithme d'itération sur les valeurs pour résoudre un problème de planification de politique dans une grille. Le but est de trouver la politique optimale pour un agent qui se déplace dans une grille, en maximisant la récompense totale en suivant les meilleures actions possibles.

Le programme prend en compte différents éléments de la grille, tels que les états cibles (reward), les dangers (penalty), et les cellules bloquées. L'algorithme calcule les valeurs des états et extrait la politique optimale en fonction de ces valeurs.

## Configuration

La grille est définie par ses dimensions (3x4) avec les éléments suivants :

- **Cellule cible (G)** : La cellule (0, 3) dans la grille, où une récompense de 1 est attribuée.
- **Cellule dangereuse (🔥)** : La cellule (1, 3) dans la grille, où une pénalité de -1 est attribuée.
- **Cellule bloquée (█)** : La cellule (1, 1) dans la grille, qui est inaccessible.
- **Récompense par pas** : Chaque mouvement dans la grille donne une récompense de 0 (c'est-à-dire qu'il n'y a pas de coût par mouvement).

Les mouvements disponibles pour l'agent sont :
- Haut (↑)
- Bas (↓)
- Gauche (←)
- Droite (→)

## Fonctionnement du Code

### 1. **`compute_values`** : Calcul des valeurs des états

Cette fonction effectue l'itération sur les valeurs pour calculer les valeurs des états dans la grille. À chaque itération, elle met à jour les valeurs des états en fonction des récompenses actuelles et des valeurs estimées des voisins, en utilisant un facteur de réduction (`discount_factor`) pour pondérer les récompenses futures.

#### Processus :
- La fonction commence par une copie des valeurs des états actuels.
- Pour chaque état (cellule de la grille), elle évalue les valeurs possibles des états voisins dans les quatre directions (haut, bas, gauche, droite).
- Si un état voisin est valide (dans les limites de la grille et non bloqué), sa valeur est calculée comme étant la somme de la récompense actuelle de cet état et du produit du facteur de réduction et de la valeur estimée de cet état voisin.
- La fonction met à jour les valeurs des états à chaque itération jusqu'à ce que le nombre maximal d'itérations soit atteint.

### 2. **`derive_policy`** : Extraction de la politique optimale

Cette fonction dérive la politique optimale en choisissant pour chaque état l'action qui conduit à l'état voisin ayant la valeur la plus élevée.

#### Processus :
- Pour chaque cellule de la grille, la fonction évalue les quatre directions possibles (haut, bas, gauche, droite).
- Elle choisit la direction qui maximise la somme de la récompense actuelle et de la valeur estimée de l'état voisin.
- Si un état est terminal (cible, danger, ou bloqué), il reçoit un symbole spécifique (G, 🔥, ou █).

La politique optimale est ensuite retournée sous forme d'une grille de symboles représentant les mouvements à effectuer pour maximiser les récompenses.

### 3. **Affichage des résultats**

Une fois les valeurs des états calculées et la politique optimale dérivée, le programme affiche :
- La politique optimale sous forme de symboles : 
  - `G` pour la cellule cible
  - `🔥` pour la cellule dangereuse
  - `█` pour la cellule bloquée
  - `↑`, `↓`, `←`, `→` pour les directions optimales
- Les valeurs des états (récompenses estimées) sous forme de matrice.

## Exemple d'Exécution

Voici un exemple de ce à quoi ressemble l'affichage de la politique optimale :

![image](https://github.com/user-attachments/assets/5b11c550-f1bf-41f6-8ef0-39a1bb1c0498)
