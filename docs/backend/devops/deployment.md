# DevOps : Déploiement & Maintenance

"You build it, you run it." Voici comment le backend est opéré.

## 🐳 Dockerisation
Chaque service possède un \`Dockerfile\` multi-stage optimisé pour la production (basé sur \`node:alpine\`).

## ⚙️ CI/CD (GitHub Actions)
Le pipeline se déclenche à chaque push sur \`main\` :
1. **Lint & Test** : Vérification de la qualité du code.
2. **Build** : Création de l'image Docker.
3. **Deploy** : Mise à jour automatique de l'instance sur Fly.io ou Vercel.

## 📊 Monitoring
- **Logs unifiés** : Utilisation de Pino pour des logs structurés (JSON).
- **Error Tracking** : Sentry pour capturer les exceptions en temps réel.
- **Uptime Monitoring** : Vérification automatique de la disponibilité de l'API toutes les 5 minutes.
