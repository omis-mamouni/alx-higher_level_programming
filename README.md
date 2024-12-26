Bien sûr ! Voici un exemple de code en C qui utilise une table de hachage pour compter le nombre d’entiers distincts dans un ensemble de \( n \) entiers. Le code inclut des commentaires détaillés pour expliquer chaque partie du processus.

### Code en C avec Commentaires

```c
#include <stdio.h>
#include <stdlib.h>

// Définition de la taille de la table de hachage
#define HASH_TABLE_SIZE 10007  // Utilisation d'un nombre premier pour réduire les collisions

// Structure pour représenter un élément dans la table de hachage (chaînage)
typedef struct Node {
    int key;            // Valeur de l'entier
    struct Node* next;  // Pointeur vers le prochain élément en cas de collision
} Node;

// Fonction de hachage simple
int hashFunction(int key) {
    // Utilisation de la fonction modulo
    return abs(key) % HASH_TABLE_SIZE;
}

// Fonction pour créer un nouveau nœud
Node* createNode(int key) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    if (!newNode) {
        printf("Erreur d'allocation mémoire.\n");
        exit(EXIT_FAILURE);
    }
    newNode->key = key;
    newNode->next = NULL;
    return newNode;
}

// Fonction pour insérer un élément dans la table de hachage
// Retourne 1 si l'élément a été inséré (n'était pas présent), 0 sinon
int insert(Node** hashTable, int key) {
    int hashIndex = hashFunction(key);
    Node* current = hashTable[hashIndex];

    // Parcourir la chaîne pour vérifier si l'élément existe déjà
    while (current != NULL) {
        if (current->key == key) {
            // L'élément existe déjà, pas besoin de l'insérer
            return 0;
        }
        current = current->next;
    }

    // Si l'élément n'existe pas, l'insérer au début de la chaîne
    Node* newNode = createNode(key);
    newNode->next = hashTable[hashIndex];
    hashTable[hashIndex] = newNode;
    return 1;
}

// Fonction pour libérer la mémoire allouée à la table de hachage
void freeHashTable(Node** hashTable) {
    for (int i = 0; i < HASH_TABLE_SIZE; i++) {
        Node* current = hashTable[i];
        while (current != NULL) {
            Node* temp = current;
            current = current->next;
            free(temp);
        }
    }
    free(hashTable);
}

int main() {
    // Exemple d'ensemble d'entiers
    int arr[] = {3, 5, 3, 2, 5, 7, 2};
    int n = sizeof(arr) / sizeof(arr[0]);

    // Allocation de la table de hachage (initialisée à NULL)
    Node** hashTable = (Node**)calloc(HASH_TABLE_SIZE, sizeof(Node*));
    if (!hashTable) {
        printf("Erreur d'allocation mémoire pour la table de hachage.\n");
        return EXIT_FAILURE;
    }

    int countDistinct = 0;

    // Parcourir chaque entier de l'ensemble
    for (int i = 0; i < n; i++) {
        // Tenter d'insérer l'élément dans la table de hachage
        // Si l'insertion réussit, c'est un élément distinct
        if (insert(hashTable, arr[i])) {
            countDistinct++;
        }
    }

    // Afficher le nombre d'éléments distincts
    printf("Nombre d'entiers distincts : %d\n", countDistinct);

    // Libérer la mémoire allouée à la table de hachage
    freeHashTable(hashTable);

    return 0;
}
```

### Explications du Code

1. **Définition de la Table de Hachage :**
   - La table de hachage est définie comme un tableau de pointeurs vers des nœuds (`Node*`). Chaque index de la table représente une "bulle" où les éléments ayant le même index de hachage seront chaînés en liste liée.

2. **Fonction de Hachage :**
   - `hashFunction` calcule l'index de hachage en utilisant le modulo de la clé avec la taille de la table. L'utilisation de `abs` assure que l'index est toujours positif.

3. **Insertion dans la Table de Hachage :**
   - La fonction `insert` vérifie si l'élément existe déjà dans la chaîne correspondante. Si l'élément n'est pas présent, il est ajouté au début de la chaîne, et la fonction retourne `1` pour indiquer une insertion réussie (élément distinct). Sinon, elle retourne `0`.

4. **Comptage des Éléments Distincts :**
   - Chaque fois qu'un élément est inséré avec succès (c'est-à-dire qu'il n'était pas déjà présent), le compteur `countDistinct` est incrémenté.

5. **Libération de la Mémoire :**
   - Après le comptage, la fonction `freeHashTable` libère toute la mémoire allouée à la table de hachage pour éviter les fuites de mémoire.

6. **Exécution de l'Exemple :**
   - L'exemple fourni utilise l'ensemble `[3, 5, 3, 2, 5, 7, 2]` et affiche le nombre d'entiers distincts, qui est `4` (3, 5, 2, 7).

### Compilation et Exécution

Pour compiler et exécuter ce programme, vous pouvez utiliser les commandes suivantes dans un terminal :

```bash
gcc -o distinct_count distinct_count.c
./distinct_count
```

**Sortie attendue :**
```
Nombre d'entiers distincts : 4
```

### Remarques Supplémentaires

- **Choix de la Taille de la Table de Hachage :** La taille de la table de hachage (`HASH_TABLE_SIZE`) est choisie comme un nombre premier pour réduire la probabilité de collisions. Pour des ensembles de données plus grands, vous pouvez augmenter cette taille.

- **Gestion des Collisions :** Ce code utilise le chaînage (listes liées) pour gérer les collisions. Une alternative pourrait être l'adressage ouvert, mais le chaînage est généralement plus simple à implémenter.

- **Performance :** En moyenne, les opérations d'insertion et de recherche dans une table de hachage ont une complexité en temps \( O(1) \), ce qui rend cette méthode efficace pour de grands ensembles de données.

- **Optimisation :** Pour améliorer les performances, surtout avec de grands ensembles, vous pouvez implémenter des fonctions de hachage plus sophistiquées ou redimensionner dynamiquement la table de hachage en fonction de la charge.

J'espère que ce code et ces explications vous seront utiles pour comprendre comment utiliser une table de hachage en C pour compter les entiers distincts dans un ensemble !
