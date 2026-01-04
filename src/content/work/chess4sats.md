---
title: Chess4sats
publishDate: 2025-11-02 00:00:00
img: /assets/chess4sats_512.png
img_alt: Logo Chess4sats
description: |
  Application web fullstack de jeu d’échecs en ligne intégrant une authentification sécurisée,
  une gestion complète des parties et une architecture pensée pour l’intégration de paiements
  via le Lightning Network de Bitcoin.
tags:
  - Dev
  - Fullstack
  - Backend
  - Frontend
  - API
  - Security
  - Bitcoin
  - Lightning
---

> Description du projet.

Chess4Sats est une application web fullstack permettant à des joueurs de s’affronter aux échecs en ligne dans un environnement sécurisé et moderne.  
Le projet a été conçu comme une plateforme orientée « match », avec une forte attention portée à la logique métier, à la gestion des états de jeu et à la fiabilité des échanges entre le front-end et le back-end.

L’architecture repose sur une API backend centralisant les règles du jeu, la persistance des données et la sécurité, couplée à une interface front-end réactive offrant une expérience utilisateur fluide sur desktop comme sur mobile.

À terme, Chess4Sats a vocation à intégrer des parties payantes grâce au réseau Lightning de Bitcoin, permettant des transactions rapides et à très faible coût.

---

## Fonctionnalités principales

### Authentification et sécurité
- Inscription et connexion via un système **JWT** (token stocké côté client)
- Protection des routes avec redirections automatiques si l’utilisateur n’est pas authentifié
- Gestion de session côté front :
  - affichage de la date d’expiration du token
  - déconnexion propre (suppression du token + redirection)
- Architecture pensée pour évoluer vers des mécanismes avancés :
  - refresh token
  - rate-limit
  - sécurisation renforcée des endpoints

### Gestion des parties
- Création d’une partie via une page dédiée (*CreateGamePage*)
- Attribution des joueurs et initialisation des paramètres de jeu :
  - cadence
  - règles / état initial
- Page de jeu dédiée (*PlayGamePage*) avec échiquier interactif
- Reprise d’une partie en cours :
  - rechargement fiable de l’état depuis la base
  - position **FEN**
  - historique des coups

### Déroulement du match et logique d’échecs
- Échiquier interactif avec déplacements en **drag & drop**
- Validation des coups via la logique métier :
  - **chess.js** côté front
  - contrôles côté backend (cohérence / persistance)
- Enregistrement des coups et mise à jour continue de l’état de la partie
- Gestion des états :
  - *en cours*
  - *terminée*
  - résultat final

### Fin de partie
- Détection automatique de la fin de partie :
  - échec et mat
  - abandon
  - victoire au temps
- Enregistrement du **winner_id** côté backend dès qu’un résultat est déterminé
- Affichage explicite côté front :
  - message de victoire
  - arrêt des interactions
  - arrêt du chronomètre

### Gestion du temps (cadence)
- Cadence standard de **10 minutes par joueur**
- Décrémentation du chronomètre uniquement pendant le tour du joueur actif
- Arrêt immédiat du chrono à la fin de la partie :
  - mat
  - abandon
  - temps écoulé
- Mise à jour dynamique de l’affichage :
  - compte à rebours en temps réel
  - synchronisation avec l’état de la partie

### Historique et navigation
- Liste des parties avec filtrage par état :
  - *en cours*
  - *terminée*
- Accès à l’historique des parties terminées
- Affichage des **noms des joueurs** à la place des identifiants techniques (IDs)

---

## Architecture et choix techniques
- Architecture **front-end / back-end découplée**
- Backend :
  - API REST sécurisée (auth, gestion des parties, persistance)
  - logique métier centralisée (états, règles, winner, temps)
- Frontend :
  - consommation de l’API (création, reprise, mise à jour de partie)
  - UI responsive (desktop / mobile)
  - échiquier interactif et feedback utilisateur

---

## Roadmap — Paiements Lightning (objectif du projet)
- Intégration prévue avec **LNBits** pour proposer des parties payantes
- Logique cible :
  - création d’un match payant
  - génération d’une facture Lightning
  - validation du paiement avant démarrage de la partie
- Vision long terme :
  - matchmaking compétitif
  - parties **pay-to-play**
  - règlement instantané en satoshis via le Lightning Network

---

## Stack utilisée
Git | Python | FastAPI | JWT | API REST | MySQL | React | TypeScript | Vite | Tailwind CSS |
chess.js | react-chessboard | Bitcoin | Lightning Network (LNBits – prévu)
