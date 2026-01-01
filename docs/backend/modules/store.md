# Module : Store Public API

Ce module alimente le site \`store.wistant.dev\`. Il doit être extrêmement performant.

## ⚡ Performance
- **Caching Layer** : Les listes d'applications sont mises en cache dans Redis.
- **Prisma Optimization** : Utilisation de sélections (\`select\`) précises pour ne pas charger d'objets inutiles.
- **Pagination** : Toujours paginer les listes pour éviter les payloads massifs.

## 📝 Endpoints Principaux
- \`GET /apps\` : Liste filtrable des produits.
- \`GET /apps/:slug\` : Détail complet d'une application (Screenshots, Changelog).
- \`GET /apps/:slug/download\` : Lien de téléchargement sécurisé du code source (ZIP).
