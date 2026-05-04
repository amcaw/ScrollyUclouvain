# ScrollyFlourish

Un modèle minimal pour créer des articles de **scrollytelling** combinant du texte
défilant à gauche et une visualisation [Flourish](https://flourish.studio/)
interactive à droite. Construit avec [SvelteKit](https://kit.svelte.dev/).

Au fur et à mesure que le lecteur fait défiler les panneaux de texte, la
visualisation Flourish avance automatiquement vers la diapositive correspondante.

---

## Démarrer le projet

Installer les dépendances puis lancer le serveur de développement :

```bash
npm install
npm run dev
```

Ouvrir ensuite [http://localhost:5173](http://localhost:5173) dans le navigateur.

Pour générer la version finale (statique) à publier :

```bash
npm run build
```

---

## Structure du projet

Seuls deux fichiers sont à modifier pour créer votre propre histoire :

```
src/
├── routes/
│   └── +page.svelte      ← votre article (texte + appel au composant)
└── lib/
    └── Scrolly.svelte    ← le composant scrollytelling (à ne pas modifier en général)
```

Les autres fichiers (`app.html`, `app.css`, `+layout.svelte`, configs) sont la
plomberie SvelteKit et n'ont pas besoin d'être touchés.

---

## Ce qu'il faut modifier

Tout se passe dans [`src/routes/+page.svelte`](src/routes/+page.svelte).

### 1. L'identifiant Flourish

Récupérez l'**ID** de votre story Flourish depuis l'URL de partage Flourish
(par exemple, dans `https://public.flourish.studio/story/3279466/`, l'ID est
`3279466`).

```js
const FlourishID = 3279466; // ← remplacez par votre propre ID
```

### 2. Les étapes (steps)

Chaque chaîne de caractères du tableau `Steps` correspond à un panneau de texte.
**L'ordre des panneaux doit correspondre à l'ordre des diapositives de votre
story Flourish** (1ʳᵉ chaîne = 1ʳᵉ diapositive, etc.).

```js
const Steps = [
    "Texte du premier panneau.",
    "Texte du <mark>deuxième</mark> panneau, avec mise en évidence.",
    "Texte du troisième panneau."
];
```

Vous pouvez utiliser du **HTML** dans chaque chaîne :

- `<mark>...</mark>` pour surligner
- `<strong>...</strong>` pour mettre en gras
- `<em>...</em>` pour mettre en italique
- `<a href="...">...</a>` pour ajouter un lien

⚠️ Attention aux apostrophes dans les chaînes en `'simple quote'` :
écrivez `"Aujourd'hui"` (guillemets doubles) plutôt que `'Aujourd\'hui'`.

### 3. Le texte autour de la partie interactive

Le contenu éditorial avant et après la section scrollytelling se modifie
directement dans le HTML de la page :

```svelte
<div class="article">
    <h2>Votre titre</h2>
    <p>Votre paragraphe d'introduction.</p>
</div>

<Scrolly flourishID={FlourishID} steps={Steps} />

<div class="article">
    <h2>La suite</h2>
    <p>Texte qui apparaît après la section interactive.</p>
</div>
```

Vous pouvez ajouter autant de blocs `<div class="article">` que vous voulez,
avant ou après le composant `<Scrolly>`.

---

## Exemple complet

```svelte
<script lang="ts">
    import Scrolly from '$lib/Scrolly.svelte';

    const FlourishID = 3279466;

    const Steps = [
        "En 1950, les émissions mondiales de <mark>CO₂</mark> atteignaient environ 6 milliards de tonnes par an.",
        "Dans les années 1980, ce chiffre avait <mark>triplé</mark>, dépassant les 19 milliards de tonnes annuelles.",
        "Aujourd'hui, nous émettons plus de <mark>36 milliards de tonnes</mark> de CO₂ chaque année."
    ];
</script>

<div class="article">
    <h2>Un exemple de scrollytelling avec Flourish</h2>
    <p>Introduction à l'article…</p>
</div>

<Scrolly flourishID={FlourishID} steps={Steps} />

<div class="article">
    <h2>La suite</h2>
    <p>Suite de l'article…</p>
</div>
```

---

## Personnaliser l'apparence

Les styles globaux de l'article (police, couleurs, largeur de colonne, etc.) se
trouvent dans [`src/app.css`](src/app.css). Les variables CSS principales sont
définies tout en haut :

```css
:root {
    --color-bg:        #FFFFFF;
    --color-text:      #000000;
    --color-accent:    #F3C14D;
    --font-body:       'Montserrat', sans-serif;
    --article-width:   620px;
}
```

Les styles propres au composant scrollytelling (panneaux, fond figé) sont dans
[`src/lib/Scrolly.svelte`](src/lib/Scrolly.svelte) à l'intérieur de la balise
`<style>`.

---

## Comment ça marche (pour les curieux)

Le composant [`Scrolly.svelte`](src/lib/Scrolly.svelte) utilise un
[`IntersectionObserver`](https://developer.mozilla.org/fr/docs/Web/API/Intersection_Observer_API)
pour détecter quel panneau de texte est actuellement visible au centre de
l'écran. L'index de ce panneau est ensuite injecté dans l'URL de l'iframe
Flourish (`#slide-N`), ce qui fait avancer la story vers la bonne diapositive.

---

## Inspirations

- [Kontinentalist – So you want to code a data story](https://www.linkedin.com/pulse/so-you-want-code-data-story-kontinentalist/)
- [newline.co – Better Data Visualizations with Svelte](https://www.newline.co/courses/better-data-visualizations-with-svelte)
- [jsonkao/svelte-scrollama](https://github.com/jsonkao/svelte-scrollama)
