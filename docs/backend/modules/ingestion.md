# Module : GitHub Ingestion

C'est le module d'automatisation qui transforme un dépôt GitHub en produit publiable sur le Store.

## 🔄 Le Workflow (Flow Magique)
1. **Webhook Receive** : Réception du signal de GitHub (Release ou Push).
2. **Payload Parsing** : Extraction du nom du repo, des tags et de l'auteur.
3. **Queue Ingestion** : Ajout d'une tâche dans BullMQ pour éviter de bloquer l'API.
4. **Analysis Worker** :
    - Récupération du \`README.md\` via l'API GitHub.
    - Détection de la stack technique.
    - Création d'un enregistrement \`Draft\` dans la base de données.

## 🛠️ Intégration API GitHub
Pour interagir avec GitHub, nous utilisons le SDK officiel **Octokit**.
- **Rate Limit** : Toujours utiliser un token d'accès personnel (PAT) ou une GitHub App pour éviter le bridage.
- **Error Handling** : Si GitHub est down, le worker doit "retry" automatiquement (Exponential Backoff).
