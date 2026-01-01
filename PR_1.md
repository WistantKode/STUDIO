# Pull Request 1: Infrastructure Foundations and Backend Documentation

## Description
Cette Pull Request regroupe l'ensemble des travaux initiaux concernant l'infrastructure du monorepo et la mise en place d'une documentation technique exhaustive du backend. L'objectif est de sécuriser les fondations du projet avant d'entamer les développements fonctionnels.

## Changements Majeurs

### Infrastructure et Workspace
- Mise en place de Turborepo avec pnpm workspaces.
- Séparation des domaines applicatifs en trois entités distinctes : `landing`, `store` et `studio`.
- Initialisation de NestJS 11 et Prisma 7 pour le backend.
- Configuration partagée de Tailwind CSS et installation des bibliothèques d'animation (GSAP, Framer Motion, Lenis).

### Documentation Technique (Backend)
- Rédaction d'un manifeste architectural détaillant le choix du Monolithe Modulaire.
- Explication approfondie du "Flow Magique" d'ingestion des dépôts GitHub (Webhooks, Queues BullMQ).
- Documentation des stratégies de haute disponibilité pour supporter une charge de 30 000 utilisateurs simultanés.
- Guide complet sur la stratégie de "Défense en Profondeur" et la gestion des accès (IAM, JWT, 2FA).

## Choix Techniques et Justifications

### Architecture Scalable
Le backend est conçu de manière "stateless" pour permettre un scaling horizontal transparent. L'utilisation d'une couche de cache Redis limite la charge sur PostgreSQL lors des pics de trafic sur le Store.

### Sécurité par Défaut
L'authentification repose sur des JWT avec rotation de Refresh Tokens via cookies sécurisés. Chaque point d'entrée API est protégé par des schémas de validation stricts (DTO).

## État du Projet
La Phase 1 ("Infrastructure Shell") est terminée. Le projet dispose désormais d'une roadmap claire (PROGRAM.md) et d'un historique de versions (RELEASES.md) cohérent.
