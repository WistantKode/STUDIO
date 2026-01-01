# 📥 Le Flow Magique : Automatisation GitHub

C'est ici que l'on prouve que tu es un ingénieur **DevOps/Product**. Le but : qu'un développeur (toi) publie une release sur GitHub et que, 5 secondes plus tard, elle apparaisse magnifiquement sur ton Store.

## 🔄 Étape par étape : Pourquoi et Comment

### 1. Le Webhook (L'Oreille)
GitHub envoie une notification (JSON) à notre API dès qu'un évènement se produit (Push, Release).
- **Le Pourquoi** : On ne veut pas "poller" (demander toutes les 5 min) à GitHub s'il y a du nouveau. C'est inefficace. On préfère que GitHub nous appelle.
- **La Sécurité** : On utilise une `Secret Key`. Si le payload n'est pas signé avec cette clé, on ignore la requête (Protection contre les faux appels).

### 2. La File d'Attente (Le Buffer)
On n'analyse pas le projet immédiatement. On le met dans une **Queue (BullMQ + Redis)**.
- **Le Pourquoi** : L'analyse d'un projet peut prendre du temps (récupérer des images, parser du texte). Si on le faisait dans la requête HTTP, elle prendrait 10 secondes et GitHub croirait que notre serveur a crashé.
- **Analogie** : C'est comme un restaurant. Le serveur prend la commande (API) et la donne en cuisine (Queue). Il revient immédiatement vers toi, et les cuisiniers travaillent en arrière-plan.

### 3. Le Parser (L'Intelligence)
Le worker récupère le `README.md`. 
- **Comment** : Via l'API GitHub (`Octokit`). On cherche des mots-clés ou des badges.
- **L'Objectif** : Générer automatiquement une description "Draft". On ne publie rien sans ton accord (validation manuelle dans le Studio).

### 4. Le ZIP Engine (Le Produit)
Le backend génère un lien de téléchargement.
- **Le Pourquoi** : Les recruteurs aiment voir le code sans aller sur GitHub. On prépare un ZIP propre (sans les `.git`, les `node_modules` et les secrets).

## 💡 Concept Clé : Idempotence
C'est un mot barbare qui veut dire : "Si je reçois 2 fois le même webhook, je ne crée pas 2 fois le même projet". 
Notre backend vérifie toujours l'ID du projet avant de créer quoi que ce soit. C'est la base de la robustesse.
