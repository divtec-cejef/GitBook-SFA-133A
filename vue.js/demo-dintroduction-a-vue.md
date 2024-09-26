# Démo d'introduction à Vue

Création d'un dépôt pour la démo : [https://classroom.github.com/a/wbeFruIa](https://classroom.github.com/a/wbeFruIa)

## Étape 1 : Initialisation de Vue.js

**🚀 Objectif :** Créer une première application Vue.js et afficher un message réactif.

### **Ajouter Vue 3 via un CDN**

{% embed url="https://aws.amazon.com/fr/what-is/cdn/" %}
Pour ceux qui ignorent ce qu'est un CDN
{% endembed %}

Ajouter le code suivant dans le fichier `index.html`  juste avant l'inclusion du fichier `script.js`, qui contiendra le code de notre application Vue.

```html
<!-- Inclusion de Vue 3 dernière version -->
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
```

### **Créer une instance Vue**

Nous allons créer une nouvelle application Vue dans le fichier `script.js`.

Le code suivant va créer cette nouvelle application et la _crocher_ sur la div `#poke-app`.

Cela veut-dire que tout ce qui est contenu dans `<div id="poke-app">...</div>`  sera contrôlé par Vue.

```javascript
const { createApp } = Vue; // Récupère la méthode pour créer un nouvelle app Vue

const app = createApp({
  setup() {
    // Déclaration des données (data) Vue
    const message = "Bienvenue dans PokeCount!";
    
    // Toutes les données retournées seront accessible dans le HTML
    return { 
      message
    };
  }
}).mount("#poke-app"); // Monte l'application sur la div #poke-app
```

### **Utiliser l'interpolation dans le HTML**

Maintenant que l'application Vue existe, on peut accéder aux données retournées directement dans le HTML.

Dans le HTML, utilisez la syntaxe `{{ message }}` n'importe où à l'intérieur de  `<div id="poke-app">` pour afficher le contenu de la donnée `message`.

On peut, par exemple, remplacer le contenu du titre principal `<h1>` avec la donnée `message`.

```html
<h1>{{ message }}</h1>
```

#### Afficher le contenu d'une donnée dans la console du navigateur

Pour afficher le contenu de la donnée message dans la console, taper cette commande.

```javascript
app.message; // "Bienvenue dans PokeCount!"
```

***

## Étape 2 : Réactivité avec `ref`

**🚀 Objectif :** Ajouter un compteur réactif pour capturer des Pokémon.

La donnée message que nous venons de créer n'est pas réactive. Si on modifie sa valeur, elle ne se met pas à jour automatiquement dans le HTML.

Pour essayer, taper cette commande dans la console du navigateur.

```javascript
app.message = "Bulbizarre"; 
```

Rien ne se passe, le contenu de notre `<h1>` n'a pas changé 😢.

### Déclarer une valeur réactive avec `ref()`

C'est bien la valeur qui sera réactive et non la donnée elle-même.

Pour déclarer une valeur réactive, nous avons besoin de la méthode `ref()`. Cela va référencer une valeur qui sera analysée en permanence par Vue. Vue répercutera immédiatement les modifications de cette valeur partout dans l'application, que ce soit dans le JavaScript ou le HTML.

#### Importer `ref()` depuis Vue

Comme pour `createApp`, nous allons importer `ref` depuis Vue. Il faut donc ajouter `ref` à la ligne des importation Vue, sans oublier de séparer les méthodes avec une virgule.

```javascript
const { createApp, ref } = Vue; // importe createApp et ref de Vue
```

**Créer une donnée réactive**

Nous allons créer une nouvelle donnée `compteur` et lui affecter une **valeur réactive** initialisée à `0`.

Ajouter ce code juste après la création de la donnée `message`.

```javascript
const compteur = ref(0); // Donnée avec valeur réactive initialisée avec 0
```

**Afficher le compteur et ajouter un bouton**

Dans le fichier `index.html`, modifier le code de `<div class="captures">` en y ajoutant la donnée `compteur`.

```html
<div class="captures">Pokémons capturés: {{ compteur }}</div>
```

#### Modifier la valeur de la donnée `compteur`

Taper la commande suivante dans la console de votre navigateur et vous devriez voir la compteur changer dans le HTML.

```javascript
app.compteur = 5; 
```

YES 🎉 Le compteur, c'est actualisé 😀



Dans le fichier `index.html`, utilisez `v-on` ou `@click` pour capturer un Pokémon.

```html
<p>Pokémons capturés : {{ compteur }}</p>
<button @click="capturer">Capturer 🐢</button>
```

#### **Incrémenter le compteur**

Créez une fonction pour capturer des Pokémon et incrémenter le compteur.

```javascript
function capturer() {
  compteur.value += 1;
}
```

***

## Étape 3 : Sauvegarder les captures

**🚀 Objectif :** Ajouter une fonctionnalité pour sauvegarder les captures.

1.  **Créer une liste réactive pour stocker les captures**\
    Utilisez `ref` pour créer une liste réactive des captures.

    ```javascript
    const capturesTab = ref([]);
    ```
2.  **Créer la fonction `sauver`**\
    Créez une fonction qui ajoute le compteur à la liste des captures et réinitialise le compteur.

    ```javascript
    function sauver() {
      if (compteur.value > 0) {
        capturesTab.value.push(compteur.value);
        compteur.value = 0;
      }
    }
    ```
3.  **Activer/Désactiver le bouton "Sauver"**\
    Utilisez `v-bind:disabled` pour désactiver le bouton si le compteur est à zéro.

    ```html
    <button @click="sauver" :disabled="compteur === 0">Sauver 💾</button>
    ```

***

## Étape 4 : Afficher les captures dans une liste

**🚀 Objectif :** Afficher les captures dans une liste et gérer le cas où la liste est vide.

1.  **Boucler avec `v-for`**\
    Utilisez `v-for` pour parcourir les éléments de la liste et les afficher.

    ```html
    <ul>
      <li v-for="(capture, index) in capturesTab" :key="index">
        {{ capture }} Pokémon capturé(s)
      </li>
    </ul>
    ```
2.  **Gérer le cas où la liste est vide avec `v-if`**\
    Ajoutez une condition pour afficher un message si la liste est vide.

    ```html
    <p v-if="capturesTab.length === 0">Aucune capture pour le moment.</p>
    ```

***

## Étape 5 : Suppression de toutes les captures

**🚀 Objectif :** Permettre aux utilisateurs de supprimer toutes les captures avec un bouton.

1.  **Ajouter un bouton de suppression**\
    Ajoutez un bouton qui réinitialise la liste des captures.

    ```html
    <button @click="capturesTab = []" :disabled="capturesTab.length === 0">
      Supprimer toutes les captures 🗑️
    </button>
    ```

***

## Étape 6 : Suppression des captures avec un double-clic

**🚀 Objectif :** Permettre aux utilisateurs de supprimer une capture spécifique en double-cliquant dessus.

1.  **Utiliser `@dblclick` pour supprimer une capture**\
    Utilisez l'événement `dblclick` pour supprimer un élément spécifique de la liste.

    ```html
    <li v-for="(capture, index) in capturesTab" :key="index" @dblclick="capturesTab.splice(index, 1)">
      {{ capture }} Pokémon capturé(s)
    </li>
    ```

***

## Étape 7 : Calculer le total des Pokémon capturés avec `computed`

**🚀 Objectif :** Calculer et afficher le total des Pokémon capturés.

1.  **Utiliser `computed` pour calculer le total**\
    Ajoutez une propriété calculée qui retourne la somme des captures.

    ```javascript
    const totalPokemons = computed(() => {
      return capturesTab.value.reduce((total, capture) => total + capture, 0);
    });
    ```
2.  **Afficher le total dans le HTML**\
    Affichez dynamiquement le total des Pokémon capturés.

    ```html
    <p>Total des Pokémon capturés : {{ totalPokemons }}</p>
    ```

***

## Étape 8 : Persister les données avec `localStorage`

**🚀 Objectif :** Sauvegarder les captures dans `localStorage` pour les récupérer après un rechargement.

1.  **Sauvegarder dans `localStorage` lors de la sauvegarde**\
    Ajoutez la persistance dans `localStorage` à chaque sauvegarde.

    ```javascript
    function sauver() {
      if (compteur.value > 0) {
        capturesTab.value.push(compteur.value);
        localStorage.setItem('captures', JSON.stringify(capturesTab.value));
        compteur.value = 0;
      }
    }
    ```
2.  **Charger les données depuis `localStorage` au chargement**\
    Utilisez `onMounted` pour récupérer les données stockées au chargement de la page.

    ```javascript
    onMounted(() => {
      const savedCaptures = JSON.parse(localStorage.getItem('captures'));
      if (savedCaptures) capturesTab.value = savedCaptures;
    });
    ```

***

## Étape 9 : Utiliser `v-model` pour un champ de saisie

**🚀 Objectif :** Permettre aux utilisateurs d'entrer manuellement le nombre de Pokémon capturés.

1.  **Ajouter un champ de saisie avec `v-model`**\
    Utilisez `v-model` pour lier la valeur du champ de saisie au compteur.

    ```html
    <input v-model.number="compteur" type="number" />
    ```
2.  **Valider l'entrée**\
    Le bouton "Sauver" ne sera activé que si la saisie est correcte.

    ```html
    <button @click="sauver" :disabled="isNaN(compteur) || compteur < 1">Sauver 💾</button>
    <p v-if="isNaN(compteur) || compteur < 1" class="error">
      Veuillez entrer un nombre valide supérieur à 0.
    </p>
    ```

***

## Étape 10 : Utilisation de `localStorage` et `onMounted` pour persister les données

**🚀 Objectif :** Sauvegarder les captures dans le navigateur et récupérer les données à chaque chargement.

1. **Persister les données avec `localStorage`**\
   Sauvegardez chaque capture dans `localStorage` avec `setItem`.
2. **Récupérer les captures lors du chargement**\
   Utilisez `onMounted` pour charger les données.

***

## Étape 11 : Utiliser les **watchers** et le **class binding**

**🚀 Objectif :** Utiliser un `watcher` pour changer la couleur du bouton "Capturer" lorsque le compteur dépasse 5.

1.  **Utiliser un `watch` pour surveiller le compteur**\
    Ajoutez un `watcher` pour observer le compteur et activer une classe CSS conditionnellement.

    ```javascript
    watch(compteur, (newVal) => {
      ilFautSauvegader.value = newVal > 5;
    });
    ```
2.  **Ajouter une classe dynamique**\
    Modifiez la classe du bouton en fonction de la valeur du compteur.

    ```html
    <button @click="capturer" :class="{ chaud: ilFautSauvegader }">
      Capturer 🐢
    </button>
    ```

    Ajoutez un style CSS pour la classe `chaud` :

    ```css
    button.chaud {
      background: #e74c3c; /* Rouge */
    }
    ```

***

## Étape 12 : Confirmation sur clic avec `@click.prevent`

**🚀 Objectif :** Ajouter une confirmation avant de naviguer vers une nouvelle page.

1. **Empêcher la navigation automatique et ajouter une confirmation**\
   Utilisez `@click.prevent` pour intercepter le

clic sur un lien et demander confirmation.

```html
<a href="https://www.pokemon.com/fr/pokedex" @click.prevent="verifierAvantDeQuitter">
  Ouvrir le Pokédex
</a>
```

2.  **Ajouter la fonction de confirmation**\
    Utilisez `confirm()` pour demander confirmation avant de naviguer.

    ```javascript
    function verifierAvantDeQuitter(event) {
      const confirmation = confirm("Avez-vous bien sauvegardé vos captures ?");
      if (confirmation) {
        window.location.href = event.target.href;
      }
    }
    ```

***

## Étape 13 : Valider la saisie avec la touche **Entrée**

**🚀 Objectif :** Sauvegarder les Pokémon capturés en appuyant sur la touche **Entrée**.

1.  **Écouter la touche Entrée avec `@keyup.enter`**\
    Ajoutez un écouteur pour la touche **Entrée** sur le champ de saisie.

    ```html
    <input v-model.number="compteur" type="number" @keyup.enter="sauver" />
    ```

***

## Étape 14 : Utiliser `ref` pour récupérer un élément HTML

**🚀 Objectif :** Redonner le focus à l'input après chaque sauvegarde.

### Comment récupérer un élément HTML pour le manipuler en JavaScript ?&#x20;

#### En JavaScript

On met un `id` à l'élément HTML qu'on veut récupérer.

```html
<h1 id="pokedex">Mon Pokédex</h1>
```

Puis on utilise la méthode `document.getElmentById()` ou`document.querySelector()`.&#x20;

```javascript
const h1Pokedex = document.getElementById("pokedex");
```

#### Avec Vue

On n'ajoute pas un `id`, mais un `ref` pour identifier l'élément qu'on veut manipuler.

```html
<h1 ref="pokedex">Mon Pokédex</h1>
```

Ensuite, on récupère l'élément HTML avec la méthode `useTemplateRef()`.

```javascript
<script setup>
import { useTemplateRef } from 'vue';

// Récupère l'élément HMTML grâce à useTemplateRef()
const h1Pokedex = useTemplateRef("pokedex");
</script>
```

#### Attendre que le composant soit monté

{% hint style="info" %}
Il faut **attendre que le composant soit monté** `onMounted` pour pouvoir manipuler l'élément HTML, car avant il n'existera simplement pas.
{% endhint %}

{% hint style="danger" %}
Utiliser `.value` pour récupérer l'élément HTML

Comme pour les autres donnée réactives `ref()` il faut utiliser .value pour accéder à la valeur.

```javascript
h1Pokedex.value.textContent = "Mon Pokédex";
```
{% endhint %}

```html
<script setup>
import { useTemplateRef, onMounted } from 'vue';

// Récupère l'élément HMTML grâce à useTemplateRef()
const h1Pokedex = useTemplateRef("pokedex");

// On doit attendre que le composant soit monté
// avant de pouvoir utiliser l'élément HTML
onMounted(() => {
  // Modifie le contenu texte 
  h1Pokedex.value.textContent = "Mon Pokédex";
  // Modifie le style CSS
  h1Pokedex.value.style.color = "#fac100";
});
</script>
```

### Démo

{% embed url="https://codepen.io/fallinov/pen/eYqNOQY" fullWidth="true" %}

### Application

1.  **Ajouter `ref` à l'input**

    ```html
    <input v-model.number="compteur" ref="inputCapture" type="number" />
    ```
2.  **Importer** `useTemplateRef` **depuis Vue**

    ```javascript
    const { createApp, ref, computed, onMounted, watch, useTemplateRef } = Vue;
    ```
3.  **Récupérer l'input**

    <pre class="language-javascript"><code class="lang-javascript"><strong>const inputCapture = useTemplateRef("inputCapture");
    </strong></code></pre>
4.  **Redonner le focus après la sauvegarde**\
    Utilisez `refs.inputCapture.focus()` après chaque sauvegarde pour redonner le focus à l'input.

    ```javascript
    function sauver() {
      if (!isNaN(compteur.value) && compteur.value > 0) {
        capturesTab.value.push(compteur.value);
        compteur.value = 0;
        inputCapture.value.focus();
      }
    }
    ```

