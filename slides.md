---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# persist drawings in exports and build
drawings:
  persist: false
---

# NextJS

Pourquoi chez nous

---

# Qu'est-ce que NextJS ?

<v-clicks>

- Framework React
- SSR friendly, serveur Node pour la production
- Page driven structure

</v-clicks>

---

# Pourquoi chez nous ?

<v-clicks>

- React
- SSR
- On aime l'experience de dev
- Acteur majeur sur le marché du React SSR

</v-clicks>

---

# Qu'est-ce que ca nous apporte ?

<v-clicks>

- **Géneration statique (et incrémentale)**
- **Routing**
- **API**
- **Rewrites redirect, custom headers CSP**
- **Head**
- **Image optim @lucien**
- **Polyfill injecté automatique @lucien**
- **Sentry @lucien**

</v-clicks>

---

## Géneration statique (et incrémentale)

/data

prechauffe des liens

prégen


---

## Routing

Folder driven
Pages d'erreur

---

## API

NextJS fournit une route particulière pour écrire des routes

- Faire une API Rest
- Un proxy 👀
- De la validation XHR por un form


```ts
// /api/ready
export default async function readyFunction(req: NextApiRequest, res: NextApiResponse) {
    const output: ReadyStatus = {
        ready: true,
    };

    res.status(200).json(output);
}
```

---

## Rewrites, redirects, custom headers CSP

Rewrites

```js
// Prices pages rules
const rewrites = [{
    source: '/prix-immobilier-new/:regionSlug([a-z-]+)/',
    destination: '/prix-immobilier-new/region',
}];
```

---

## Rewrites, redirects, custom headers CSP

Redirections

```js
const redirect = [{
    source: '/about',
    destination: '/',
    permanent: true,
}]
```

---

## Rewrites, redirects, custom headers CSP

Headers (pour déclarer les CSP)

```js
const headers = [{
    source: '/(.*)',
    headers: [
        { key: 'Content-Security-Policy-Report-Only', value: require('./csp') },
    ]
}]
```

---

## Head

---

## Image optim @lucien

---

## Polyfill injecté automatique @lucien

---

## Sentry @lucien

---

# Coté tooling

- 0 config par design, mais configurable, surcharge complète de l'objet webpack
- Linter eslint avec les rules Core Webvitals et A11Y par défaut
- Alias sur les chemins d'import. Ex : `@/images/cat.gif`
- Abstraction de `fetch()` pour une utilisation universelle

---

# Limitations

- SSR : code react sans window,
- Build time config par defaut => react env
- Server code removing

---

# Code

Une boite derriere
Dev très actif (react 18 en cours d’implem)
Commu hyperactive
Docs quali et interactive

---

# Features pour futur

- I18n...
- Migration tooling en Rust avec SWC
- Migration CRA automatisée (expérimentale)

---

# Merci


