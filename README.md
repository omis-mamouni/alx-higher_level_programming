Pour compter le nombre d’entiers distincts dans un ensemble de \( n \) entiers en utilisant une table de hachage, vous pouvez suivre la méthode suivante :

### Étapes à Suivre

1. **Initialisation de la Table de Hachage :**
   - Créez une table de hachage vide. Cette table servira à stocker chaque entier rencontré dans l'ensemble, en évitant les doublons.

2. **Parcours de l’Ensemble d’Entiers :**
   - Parcourez chaque entier de l'ensemble un par un.

3. **Insertion dans la Table de Hachage :**
   - Pour chaque entier \( x \) :
     - **Vérification de l’Existence :**
       - Utilisez une fonction de hachage pour déterminer la position où \( x \) pourrait être stocké dans la table de hachage.
       - Vérifiez si \( x \) est déjà présent à cette position ou dans la liste de collision (si la table utilise le chaînage).
     - **Ajout si Nécessaire :**
       - Si \( x \) n’est pas présent, insérez-le dans la table de hachage.
       - Si \( x \) est déjà présent, ignorez-le (car il s'agit d'un doublon).

4. **Comptage des Éléments Distincts :**
   - Après avoir inséré tous les entiers, le nombre d’éléments distincts correspond au nombre d’entrées uniques dans la table de hachage.

### Exemple Illustratif

Supposons que l'ensemble d'entiers soit : [3, 5, 3, 2, 5, 7, 2]

- **Initialisation :** Table de hachage vide.
- **Insertion :**
  - Insérer 3 → Table : {3}
  - Insérer 5 → Table : {3, 5}
  - Insérer 3 → Déjà présent, ignorer.
  - Insérer 2 → Table : {3, 5, 2}
  - Insérer 5 → Déjà présent, ignorer.
  - Insérer 7 → Table : {3, 5, 2, 7}
  - Insérer 2 → Déjà présent, ignorer.
- **Résultat :** 4 entiers distincts (3, 5, 2, 7)

### Complexité

- **Temps :** En moyenne, l'insertion et la recherche dans une table de hachage se font en temps \( O(1) \). Ainsi, pour \( n \) entiers, la complexité temporelle est \( O(n) \).
- **Espace :** La table de hachage nécessite un espace proportionnel au nombre d’éléments distincts, au pire \( O(n) \).

### Remarques

- **Gestion des Collisions :** Il est important de choisir une bonne fonction de hachage pour minimiser les collisions, ce qui maintient l’efficacité des opérations.
- **Types de Tables de Hachage :** Selon l’implémentation, vous pouvez utiliser des tables de hachage avec chaînage (listes liées pour gérer les collisions) ou avec adressage ouvert (comme le probing linéaire ou quadratique).

### Conclusion

L’utilisation d’une table de hachage est une méthode efficace pour compter le nombre d’entiers distincts dans un ensemble, grâce à sa capacité à insérer et rechercher des éléments en temps constant moyen. Cette approche est particulièrement adaptée pour de grands ensembles de données où les performances sont cruciales.
