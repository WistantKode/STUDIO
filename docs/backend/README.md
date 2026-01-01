# Backend Documentation — Wistant Studio

Bienvenue dans la documentation technique du cœur du système Wistant Studio. Ce guide détaille l'architecture, les modules, la sécurité et les processus DevOps qui font fonctionner la plateforme.

## 🧭 Navigation

1. [**Architecture**](./architecture/monolith.md) — Comprendre le Monolithe Modulaire.
2. [**Modules**](./modules/README.md) — Détail technique des cœurs fonctionnels (IAM, Ingestion, Store).
3. [**Sécurité**](./security/best-practices.md) — Règles d'or et implémentations critiques.
4. [**DevOps**](./devops/deployment.md) — Pipelines, Docker et Monitoring.

## 🎯 Philosophie Technique
- **Minimalisme & Précision** : Pas de code inutile. Chaque ligne de NestJS doit avoir un but.
- **Product Engineer Mindset** : Le backend n'est pas juste une API, c'est le moteur d'une expérience utilisateur.
- **Fail Fast** : Validation stricte des données (Zod/Class-Validator) à l'entrée du système.

---

## 🏗️ Structure des Dossiers Backend
\`\`\`text
apps/api/src/
├── shared/          # Centralisation (Prisma, Logger, Exceptions)
├── modules/
│   ├── iam/         # Auth, 2FA, JWT
│   ├── ingestion/   # GitHub Webhooks, Parsing metadata
│   ├── store/       # API publique pour le frontend Store
│   └── studio/      # API privée pour le dashboard admin
└── main.ts          # Point d'entrée NestJS
\`\`\`
