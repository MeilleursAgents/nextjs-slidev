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

- Framework React, pas juste un builder
- Serveur Node pour la production
- Page driven

</v-clicks>

---

# Qu'est-ce que ca nous apporte ?

<v-clicks>

- **SSG**
- **Routing**
- **API**
- **Rewrites redirect, custom headers CSP**
- **Head**
- **Image optim @lucien**
- **Polyfill injecté automatique @lucien**
- **Sentry @lucien**

</v-clicks>

---

## SSG

---

## Routing

---

## API

---

## Rewrites redirect, custom headers CSP

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
- Absctraction de `fetch()` pour une utilisation universelle
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

- I18n ….
- Migration tooling en Rust avec SWC
- Migration CRA automatisée (expérimentale)

---

# Merci


