# Tableaux

## Créer et manipuler des tableaux

```javascript
// Créer un tableau vide
const animaux = [];

// Créer un tableau avec des valeurs de différents types
const tableauHétérogène = [zoo, 33, true, 'une chaine', '🐷'];

// Créer un tableau avec des valeurs (émojis animaux)
const zoo = ['🐔', '🐷', '🐑', '🐇'];

// Retourner un élément spécifique du tableau
zoo[1]; // Retourne 🐷

// Changer une valeur
zoo[1] = '🦄'; // Change 🐷 en 🦄

// Ajouter une valeur à la fin d'un tableau
zoo[zoo.length] = '🦊'; // Ajoute 🦊 à la fin

// Ajouter une ou plusieurs valeurs à la fin d'un tableau (push)
zoo.push('🐼', '🐻'); // Ajoute 🐼 et 🐻 à la fin

// Ajouter une ou plusieurs valeurs au début du tableau (unshift)
zoo.unshift('🐸', '🐒'); // Ajoute 🐸 et 🐒 au début

// Récupérer et supprimer le dernier élément d'un tableau (pop)
let dernier = zoo.pop(); // Retire 🐻 du tableau

// Récupérer et supprimer le premier élément du tableau (shift)
let premier = zoo.shift(); // Retire 🐸 du tableau

// Récupérer et supprimer un sous-tableau (splice)
// Premier paramètre : position de départ, 2e paramètre : nombre d'éléments
let sousTableau = zoo.splice(3, 2); // Retourne et supprime les 4e et 5e éléments du tableau

console.log(sousTableau); // Affiche le sous-tableau retiré : ['🐇', '🦊']
console.log(zoo); // Affiche le tableau modifié : ['🐒', '🦄', '🐑', '🐼']

```

***

## Parcourir un tableau

### Instruction `for`

```javascript
const animaux = ['🐔', '🐷', '🐑', '🐇'];

// Boucle for classique pour parcourir le tableau
for (let i = 0; i < animaux.length; i++) {
    // Affiche l'index et l'élément actuel du tableau
    console.log(`Index ${i}: ${animaux[i]}`);
}

// Résultat attendu :
// Index 0: 🐔
// Index 1: 🐷
// Index 2: 🐑
// Index 3: 🐇

```

### Instruction `for...of`

```javascript
const animaux = ["🐔", "🐷", "🐑", "🐇"];
​
// Itération avec for..of
for (let animal of animaux) {
   console.log(animal);
}
​
// 🐔
// 🐷
// 🐑
// 🐇
```

#### **Avec index**

```javascript
const animaux = ['🐔', '🐷', '🐑', '🐇'];

// Utiliser la méthode entries() pour obtenir l'index et l'élément
for (const [index, animal] of animaux.entries()) {  
  console.log(index, animal);
}

// Résultat attendu :
// 0 🐔
// 1 🐷
// 2 🐑
// 3 🐇

```

### Méthode `forEach()`

```javascript
const animaux = ["🐔", "🐷", "🐑", "🐇"];
​
// Méthode forEach avec fonction anonyme (depuis ES5 seulement)
animaux.forEach(function(animal) {
   console.log(animal);
});
​
// 🐔
// 🐷
// 🐑
// 🐇
```

***



## Retourner le contenu d'un tableau sous forme de chaîne

### **Méthode `join()`**

La méthode `join()` permet de concaténer tous les éléments d'un tableau en une seule chaîne de caractères. On peut spécifier un séparateur entre chaque élément (par défaut, une virgule).

```javascript
const elements = ['Fire', 'Air', 'Water'];

console.log(elements.join());    // "Fire,Air,Water"
console.log(elements.join(''));   // "FireAirWater"
console.log(elements.join('-'));  // "Fire-Air-Water"
```

***

## Filtrer un tableau

### **Méthode `filter()`**&#x20;

{% hint style="danger" %}
#### Retourne un nouveau tableau
{% endhint %}

La méthode `filter()` crée un nouveau tableau avec tous les éléments qui passent le test implémenté par la fonction fournie.

```javascript
const nombres = [1, 2, 3, 4, 5, 6];
const pairs = nombres.filter(nombre => nombre % 2 === 0);
​
console.log(pairs); // [2, 4, 6]
```

#### Pour un tableau d'objets

```javascript
const utilisateurs = [
  { nom: 'Alice', age: 25 },
  { nom: 'Bob', age: 30 },
  { nom: 'Charlie', age: 35 }
];
​
const utilisateursJeunes = utilisateurs.filter(utilisateur => utilisateur.age < 30);
​
console.log(utilisateursJeunes); // [{ nom: 'Alice', age: 25 }]
```

***

## Trier un tableau

### **Méthode `sort()`**&#x20;

{% hint style="danger" %}
Modifie le tableau traité
{% endhint %}

La méthode `sort()` trie les éléments d'un tableau en place et retourne le tableau. La fonction de comparaison peut être utilisée pour définir l'ordre de tri.

```javascript
const fruits = ['banane', 'pomme', 'orange', 'ananas'];
fruits.sort();
​
console.log(fruits); // ['ananas', 'banane', 'orange', 'pomme']
```

#### Pour un tableau d'objets

```javascript
const utilisateurs = [
  { nom: 'Alice', age: 25 },
  { nom: 'Bob', age: 30 },
  { nom: 'Charlie', age: 35 }
];
​
utilisateurs.sort((a, b) => a.age - b.age);
​
console.log(utilisateurs);
// [
//   { nom: 'Alice', age: 25 },
//   { nom: 'Bob', age: 30 },
//   { nom: 'Charlie', age: 35 }
// ]
```

### Utilisation de `localeCompare()`&#x20;

Lorsque vous travaillez avec des chaînes de caractères, en particulier dans des langues différentes ou avec des accents, la méthode `localeCompare()` est très utile pour un tri plus précis et conforme aux conventions locales.

**`a.localeCompare(b)`** : Cette méthode compare deux chaînes de caractères (ici `a` et `b`) en tenant compte de la langue et des règles de tri locales. Elle retourne :

* `-1` si `a` doit précéder `b` dans l'ordre de tri,
* `1` si `a` doit suivre `b`,
* `0` si les deux chaînes sont considérées comme égales dans l'ordre de tri.

```javascript
const fruits = ['pomme', 'Épinard', 'Orange', 'abricot'];

// Trier les fruits sans utiliser localeCompare
fruits.sort();
console.log(fruits);
// ['Orange', 'abricot', 'pomme', 'Épinard']

// Trier les fruits par ordre alphabétique 
// en tenant compte des accents et de la casse (français)
fruits.sort((a, b) => a.localeCompare(b, 'fr'));
console.log(fruits);
// ['abricot', 'Épinard', 'Orange', 'pomme']

```

* **Sans `localeCompare()`** :
  * Le tri se fait selon les valeurs Unicode.
  * Les majuscules comme `É` peuvent apparaître à des positions inattendues, par exemple, `Épinard` peut être placé après `pomme`.
* **Avec `localeCompare('fr')`** :
  * Le tri respecte les règles linguistiques françaises.
  * Les accents sont correctement considérés, plaçant par exemple `Épinard` après `abricot` mais avant `pomme`.

#### **Même chose avec un tableau d'objets**

```javascript
const fruits = [
    { nom: 'pomme', prix: 2.5 },
    { nom: 'Épinard', prix: 3.0 },
    { nom: 'Orange', prix: 1.5 },
    { nom: 'abricot', prix: 4.0 }
];

// Trier les objets sans utiliser localeCompare
fruits.sort((a, b) => a.nom > b.nom ? 1 : -1);
console.log("Sans localeCompare:");
fruits.forEach(fruit => console.log(`${fruit.nom} - ${fruit.prix}€`));
// Résultat potentiel : ['Orange - 1.5€', 'abricot - 4.0€', 'pomme - 2.5€', 'Épinard - 3.0€']

// Trier les objets par ordre alphabétique
// en tenant compte des accents et de la casse (français)
fruits.sort((a, b) => a.nom.localeCompare(b.nom, 'fr'));
console.log("Avec localeCompare ('fr'):");
fruits.forEach(fruit => console.log(`${fruit.nom} - ${fruit.prix}€`));
// Résultat attendu : ['abricot - 4.0€', 'Épinard - 3.0€', 'Orange - 1.5€', 'pomme - 2.5€']

```

***

## Recherche de sous-chaîne dans un tableau de chaînes de caractères

#### Utilisation de `includes()`

{% hint style="danger" %}
**Retourne un nouveau tableau**
{% endhint %}

```javascript
// Créer un tableau simple de chaînes de caractères
const noms = ['Alice', 'Bob', 'Charlie', 'David', 'Eve'];
​
// Rechercher les noms qui contiennent la lettre 'a'
const nomsAvecA = noms.filter(nom => nom.toLowerCase().includes('a'));
​
console.log(nomsAvecA);
// Résultat :
// ["Alice", "Charlie", "David"]
```

#### Alternative avec `indexOf()`

{% hint style="danger" %}
**Retourne un nouveau tableau**
{% endhint %}

```javascript
// Créer un tableau simple de chaînes de caractères
const noms = ['Alice', 'Bob', 'Charlie', 'David', 'Eve'];
​
// Rechercher les noms qui contiennent la lettre 'a'
const nomsAvecA = noms.filter(nom => nom.toLowerCase().indexOf('a') !== -1);
​
console.log(nomsAvecA);
// Résultat :
// ["Alice", "Charlie", "David"]
```

***

### Résumé des fonctions

* **Modifie le tableau en place :** `push`, `pop`, `shift`, `unshift`, `splice`, `sort`.
* **Retourne un nouveau tableau :** `filter`, `slice`, `map`, `concat`, `join`, `includes`, `indexOf`.
