# Modules Fonctionnels

Le backend est découpé en modules NestJS autonomes. Voici le détail de chaque moteur.

## 🔑 [Identity & Access Management (IAM)](./iam.md)
Gère l'authentification, les sessions et les permissions. Sécurité critique.

## 📥 [GitHub Ingestion](./ingestion.md)
Le "Flow Magique". Traitement des webhooks, analyse des repos et création de versions.

## 🏬 [Store API](./store.md)
Le service qui nourrit le frontend public. Optimisé pour la lecture et le cache.

---

## Guide d'implémentation d'un module
Pour créer un nouveau module, utilise le CLI NestJS et respecte cette organisation :
1. \`entity\` : Le modèle de données (Prisma).
2. \`dto\` : Validation des inputs.
3. \`service\` : Logique métier pure.
4. \`controller\` : Endpoints API.
