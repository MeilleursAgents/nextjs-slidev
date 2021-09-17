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
- Page driven structure

</v-clicks>

---

# Pourquoi chez nous ?

<v-clicks>

- React
- SSR
- On aime l'experience de dev
- Acteur majeur sur le marché du React SSR 
- Des optims des perfs faciles (Pour respected les Core Web Vitals)

</v-clicks>

---

# Qu'est-ce que ca nous apporte ?

<v-clicks>

- **Routing**
- **Géneration statique (et incrémentale)**
- **API**
- **Rewrites redirect, custom headers CSP**
- **Head**
- **Image optim @lucien**
- **Polyfill injecté automatique @lucien**
- **Sentry @lucien**

</v-clicks>

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

![Remote Image](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F0ddb1934-cbbb-4ea4-8a76-b7501fc78a7e%2FScreenshot_2020-05-20_at_19.03.36.png?table=block&id=33cd2f32-4b2f-4bb6-9f13-a0e3e4e0c5f8&spaceId=a1bf93e4-d3ed-4bef-b7e7-a1181abf225b&width=1540&userId=82bf6ebc-5bea-43d6-97ac-9d8846177cc4&cache=v2)


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

### Image locale
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

[https://drive.google.com/drive/u/0/folders/1SLX9T3M7O1B7290gNRX8WyMvHrtJfu_z](Live demo)

---

## Polyfill injecté automatique

[https://drive.google.com/drive/u/0/folders/1SLX9T3M7O1B7290gNRX8WyMvHrtJfu_z](Live demo)

```tsx
    <Script
        src="https://polyfill.io/v3/polyfill.min.js?features=IntersectionObserverEntry%2CIntersectionObserver"
        strategy="beforeInteractive"
    />
```

### 
---

## Sentry @lucien

![Local Image](/img.png)
- Config simple (Server/Client)
- Combine @sentry/webpack @sentry/node @sentry/browser
- Optimisations + upload des source-maps
---

# Coté tooling

- 0 config par design, mais configurable, surcharge complète de l'objet webpack
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

- Une boite derriere avec une équipe à plein de dessus : Vercel
- Dev très actif (react 18 en cours d’implem)
- Commu hyperactive (voir les exemples)
- Docs de qualité et interactives

---

# Features pour futur

- I18n...
- Migration tooling en Rust avec SWC
- Migration CRA automatisée (expérimentale)

---

# Merci


