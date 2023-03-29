# Tableaux

## Ajouter et retirer des valeurs

```javascript
// Crée un tableau vide
const monPremierTab = [];

// Crée un tableau avec valeurs. Peut contenir différents types
const monTab = [monPremierTab, 33, true, 'une chaine'];

// Retourne un élément spécifique du tableau
monTab[1]; // Retourne 33

// Changer une valeur
monTab[1] = "ok";

// Ajouter une valeur à la fin d'un tableau
monTab[monTab.length] = 'nouvelle valeur';

// Ajouter une ou plusieurs valeurs à la fin d'un tableau
monTab.push('fromage', 'pain');

//Ajouter une ou plusieurs valeur au début du tableau
monTab.unshift('poivre', 'sel');

// Récupérer et supprimer le dernier élément d'un tableau
let dernier = monTab.pop();

// Récupérer et supprimer le premier élément du tableau
let premier = monTab.shift();

// Récupérer et supprimer un sous tableau
// Premier paramètre postion de départ, 2e paramètre le nombre d'éléments
monTab.splice(3, 2); //Reourne et supprime le 4e et 5e élément
```

## Parcourir un tableau

### **instruction** for

```javascript
const animaux = [ '🐔', '🐷', '🐑', '🐇'];

// Boucle for classique (éviter i++ et utiliser ++i ou i+=1)
for (let i = 0; i < animaux.length; ++i) {
    console.log(animaux[i]);
}

// 🐔
// 🐷
// 🐑
// 🐇
```

#### Avec index

```javascript
const animaux = [ '🐔', '🐷', '🐑', '🐇'];

for (const [index, animal] of animaux.entries()) {  
	console.log(index, animal);
}

// 0 🐔
// 1 🐷
// 2 🐑
// 3 🐇
```

### **instruction** for...of

```javascript
const animaux = ["🐔", "🐷", "🐑", "🐇"];

// Itération avec for..of
for (let animal of animaux) {
   console.log(animal);
}

// 🐔
// 🐷
// 🐑
// 🐇
```

### Méthode forEach()

```javascript
const animaux = ["🐔", "🐷", "🐑", "🐇"];

// Méthode forEach avec fontion anonyme (depsui ES5 seulement)
animaux.forEach(function(animal) {
   console.log(animal);
});

// 🐔
// 🐷
// 🐑
// 🐇
```

### Exemples

{% embed url="https://codepen.io/fallinov/pen/BqEJgp?editors=0011" %}

## Retourner le contenu d'une tableau sous forme de chaîne

### Array.prototype.join()

La méthode **`join()`** crée et renvoie une nouvelle chaîne de caractères en concaténant tous les éléments d'un tableau (ou d'[un objet semblable à un tableau](https://developer.mozilla.org/fr/docs/Web/JavaScript/Guide/Indexed\_collections#manipuler\_des\_objets\_semblables\_%c3%a0\_des\_tableaux)). La concaténation utilise la virgule ou une autre chaîne, fournie en argument, comme séparateur.

```javascript
const elements = ['Fire', 'Air', 'Water'];

console.log(elements.join());
// "Fire,Air,Water"

console.log(elements.join(''));
// "FireAirWater"

console.log(elements.join('-'));
// "Fire-Air-Water"
```
