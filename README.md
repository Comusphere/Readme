# Comusphere UI

> Interface web du réseau social communautaire **Comusphere** — connectez-vous, créez et animez vos communautés.

![Next.js](https://img.shields.io/badge/Next.js-13-black?logo=next.js)
![TypeScript](https://img.shields.io/badge/TypeScript-5-blue?logo=typescript)
![Tailwind CSS](https://img.shields.io/badge/TailwindCSS-3-38bdf8?logo=tailwind-css)
![Redux](https://img.shields.io/badge/Redux-Toolkit-764abc?logo=redux)
![Vercel](https://img.shields.io/badge/Deployed%20on-Vercel-black?logo=vercel)

---

## Présentation

**Comusphere** est un réseau social communautaire de nouvelle génération qui permet à chacun de créer ou rejoindre des communautés centrées sur des centres d'intérêt précis. Contrairement aux plateformes généralistes, Comusphere offre des espaces structurés, personnalisables et modérables, avec une messagerie en temps réel intégrée nativement.

Ce dépôt contient le **frontend** de la plateforme, développé avec Next.js 13, TypeScript, Tailwind CSS et Redux.

---

## Fonctionnalités

- **Authentification** — Inscription, connexion sécurisée via JWT stocké en cookie `httpOnly`
- **Communautés** — Création, gestion des membres, rôles (fondateur / modérateur / membre)
- **Publications** — Texte, images, liens ; likes, dislikes, commentaires et réponses
- **Chat en temps réel** — Messagerie publique (par communauté) et privée (entre membres) via WebSocket
- **Notifications** — Alertes pour nouvelles interactions, messages, demandes d'adhésion
- **Recherche** — Recherche de communautés, membres et publications
- **Profil communautaire** — Pseudonyme et avatar distincts par communauté
- **Responsive** — Interface mobile-first via Tailwind CSS

---

## Stack technique

| Couche | Technologie |
|---|---|
| Framework | Next.js 13 (App Router) |
| Langage | TypeScript |
| Style | Tailwind CSS |
| État global | Redux Toolkit |
| Communication API | Fetch / REST (`https://api.comusphere.com`) |
| Chat temps réel | WebSocket (`https://dev.comusphere.com`) |
| Déploiement | Vercel (CDN mondial + SSR) |

---

## Charte graphique

| Rôle | Couleur |
|---|---|
| Fond dark / Titre light | `#251F2F` |
| Fond light / Titre dark | `#F2EDFB` |
| Call to action (boutons) | `#F8E559` |
| Conteneurs / accents | `#701A75` |
| Texte secondaire | `#CACACA` |

**Typographies :** `Secular One` (titres) · `Segoe UI` (corps de texte)

---

## Prérequis

- Node.js ≥ 18
- npm ou yarn
- Backend Comusphere en cours d'exécution (voir [`comusphere-api`](https://github.com/Comusphere/comusphere-api))

---

## Installation

```bash
# Cloner le dépôt
git clone https://github.com/Comusphere/comusphere-ui.git
cd comusphere-ui

# Installer les dépendances
npm install
```

---

## Configuration

Créez un fichier `.env.local` à la racine du projet :

```env
NEXT_PUBLIC_API_URL=http://localhost:8080
NEXT_PUBLIC_CHAT_URL=http://localhost:4000
```

Pour la production, ces variables pointent vers :
- `https://api.comusphere.com` (backend Spring Boot)
- `https://dev.comusphere.com` (microservice chat Node.js)

---

## Lancer le projet

```bash
# Développement
npm run dev

# Build de production
npm run build
npm start
```

L'application sera disponible sur `http://localhost:3000`.

---

## Structure du projet

```
comusphere-ui/
├── app/                    # App Router Next.js 13
│   ├── (auth)/             # Pages inscription / connexion
│   ├── community/[id]/     # Pages d'une communauté
│   ├── messages/           # Messagerie privée
│   └── ...
├── components/             # Composants React réutilisables
│   ├── PostCard/
│   ├── CommentDrawer/
│   ├── Sidebar/
│   └── ...
├── store/                  # Configuration Redux
│   ├── slices/             # auth, community, posts...
│   └── index.ts
├── lib/                    # Utilitaires, appels API, WebSocket
├── public/                 # Assets statiques
└── tailwind.config.ts
```

---

## Architecture globale

```
┌─────────────────────────────────────────┐
│            comusphere-ui (Next.js)       │
│         Vercel — SSR + CDN mondial       │
└───────────────┬─────────────────────────┘
                │ REST API          │ WebSocket
                ▼                   ▼
   ┌────────────────────┐  ┌──────────────────────┐
   │  comusphere-api    │  │  comusphere-chat      │
   │  Spring Boot 3     │  │  Node.js + WebSocket  │
   │  Java 21           │  │  MongoDB Atlas        │
   └────────┬───────────┘  └──────────────────────┘
            │
            ▼
   ┌────────────────────┐
   │   MySQL (Azure)    │
   │  Users, Posts,     │
   │  Communities...    │
   └────────────────────┘
```

---

## Authentification

Le frontend utilise un token **JWT** transmis à chaque requête via l'en-tête `Authorization: Bearer ...`. Le token est stocké dans un cookie sécurisé `httpOnly` pour prévenir les attaques XSS. La session utilisateur est gérée côté client par Redux.

---

## Déploiement

Le frontend est déployé automatiquement sur **Vercel** à chaque push sur la branche principale :

- CI/CD intégré depuis GitHub
- Variables d'environnement configurées sur Vercel
- SSR activé pour le référencement (SEO)
- Domaine : [`https://comusphere.com`](https://comusphere.com)

---

## Roadmap (V2 et au-delà)

- [ ] Infinite scroll sur le fil d'actualités
- [ ] Notifications push (web + mobile)
- [ ] Mode sombre / clair automatique
- [ ] Authentification 2FA (TOTP + QR Code)
- [ ] Suggestions de messages avec IA (Mistral)
- [ ] PWA — Progressive Web App
- [ ] Accessibilité ARIA complète
- [ ] Système de badges communautaires

---

## Projets liés

| Dépôt | Description |
|---|---|
| [`comusphere-api`](https://github.com/Comusphere/comusphere-api) | Backend Java 21 / Spring Boot 3 |
| [`comusphere-chat`](https://github.com/Comusphere/comusphere-chat) | Microservice chat Node.js / WebSocket |

---

## Auteur

**Thevaraj Theivathan** — Projet de fin d'études  
Master Développement & Innovation · Option Lead FullStack · ENSITECH · 2024-2025

---

## Licence

Ce projet est réalisé dans un cadre académique. Tous droits réservés © 2024-2025 Thevaraj Theivathan.