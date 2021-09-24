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

Pourquoi et comment ?

---

# Qu'est-ce que NextJS ?

<v-clicks>

- Framework React
- SSR friendly, serveur Node pour la production
- Orienté DX et performance

</v-clicks>

---

# Pourquoi chez nous ?

<v-clicks>

- React
- SSR
- On aime l'experience de dev
- Acteur majeur sur le marché du React SSR 
- Des optims des perfs faciles (Pour respecter les Core Web Vitals)

</v-clicks>

---

# Qu'est-ce que ca nous apporte ?

- **Routing**
- **Géneration statique (et incrémentale)**
- **API**
- **Rewrites redirect, custom headers CSP**
- **Head**
- **Image optim @lucien**
- **Dynamic Loading @lucien**
- **Polyfill injecté automatique @lucien**
- **Sentry @lucien**

---

## Routing

### Folder driven

Un fichier = une route

src/pages

 ↳ index.tsx                   /

 ↳ about.tsx                   /about

 ↳ characters/index.tsx        /characters

 ↳ characters/[id].tsx         /characters/123

 ↳ [...slug].tsx               /whatever-blabla

### Pages d'erreur

Templates de 4XX, 5XX personnalisables au même titre que les autres pages 

---

## Géneration statique (et incrémentale)

Différentes facon de faire

![Local Image](/build.png)


---

## Géneration statique (et incrémentale)

Sur une page avec du contenu dynamique, exporter une méthode.

```tsx {6-11}
const Blog = ({ posts }) => 
    <ul>
        {posts.map((post) => <li>{post.title}</li>)}
    </ul>

export async function getStaticProps(context) {
    const posts = fetch('/posts')
    return {
        props: { posts },
        revalidate: false, // Optionnel
    }
}
```

Généré au build

Coté client, quand le HTML devient SPA, on ne recharge plus la page, seule la data est fetch

Le endpoint interne `/_next/data` est appelé pour exécuter cette méthode et répond du JSON.


---

## API

NextJS fournit une route particulière pour écrire des routes

- Faire une API Rest
- Un proxy 👀
- De la validation XHR pour un form


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

Surcharge du head/metas/title au niveau page (Bonus : Utilisation de NextSEO pour simplifier)

```tsx
<NextSeo
    description={translate(
        'Comparez et choisissez votre agence immobilière selon ses ventes récentes, ses avis clients et sa proximité avec votre bien',
    )}
    openGraph={{
        title: translate('Comparateur d’agences immobilières'),
        description: translate(
            'Comparez et choisissez votre agence immobilière selon ses ventes récentes, ses avis clients et sa proximité avec votre bien',
        ),
        url: 'https://www.meilleursagents.com/professionnel-immobilier/',
    }}
    title={translate('Comparateur d’agences immobilières')}
/>
```

---

## Image optim

```tsx
    <Image src={profilePic} alt="Picture of the author" />
```

### Image distante
```tsx
    <Image 
        src={"https://thumbor.meilleursagents.com/oNKMEA-KsOPNUUe5BxHq2gThxrQ=/120x80/filters:watermark(realtor.png,center,center,0)/f9f9f9"} 
        alt="Une image thumbor"
        width={120}
        height={80}
        placeholder="blur"
        blurDataUrl="https://blur.com/image.jpeg"
        // layout="fill"
        // objectFit="cover"
        // objectPosition="center"
        // quality="90"
        // priority={false}
    />
```

<a href="https://drive.google.com/file/d/167la-8yyXYuf_SXtRwABsC3pVSMETi7Y/view">Live demo</a>

---

## Dynamic Loading

Chargement de composants en fonction du scroll

<a href="https://drive.google.com/file/d/1Mf_1POjml_oX2EId1qj-SV-4R5iCE7r3/view">Live demo</a>

---

## Polyfill injecté automatique

```tsx
<Script
    src="https://polyfill.io/v3/polyfill.min.js?features=IntersectionObserverEntry%2CIntersectionObserver"
    strategy="beforeInteractive"
/>
```

<a href="https://drive.google.com/file/d/1MDNcZIrXmajolrIwspOFWi_GJ8WaOsZ4/view">Live demo</a>

### 
---

## Sentry

![Local Image](/img.png)
- Config simple (Server/Client)
- Combine @sentry/webpack @sentry/node @sentry/browser
- Optimisations + upload des source-maps
---

# Coté tooling

- 0 config de nature, mais configurable, surcharge complète de l'objet webpack
- Linter eslint avec les rules Core Webvitals et A11Y par défaut
- Alias sur les chemins d'import. Ex : `@/images/cat.gif`
- Abstraction de `fetch()` pour une utilisation universelle

---

# Retour d'expérience

- SSR : code react sans window
  - Des réflexes à prendre, notamment pour le responsive
- Build time config par defaut => 
    - Contournement avec `react-env`
- Suppression du code serveur à prendre en compte
  - Car notre app est full-stack
- Prégénération des pages en grand nombre

---

# Ecosystème

- Une boite derrière avec une équipe à plein temps de dessus : Vercel
- Dévelopement très actif (react 18 en cours d’implementation)
- Communauté hyperactive (voir les exemples)
- Docs de qualité et interactives

---

# Features pour futur

- I18n...
- Migration tooling en Rust avec SWC
- Migration CRA automatisée (expérimentale)

---

# Merci

Join us

![Local Image](/join-us.gif)

---

P.S. : 

Fait avec Sli.dev, MarkDown based, en VueJS

Plus simple que Spectacle (L'alternative React) mais moins mature en features
