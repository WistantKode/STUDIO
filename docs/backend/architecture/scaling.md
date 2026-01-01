# 🚀 Scaling : Survivre à 30 000 utilisateurs simultanés

Faire un site pour 10 personnes est facile. Faire un système qui encaisse **30 000 utilisateurs connectés en même temps** est un défi de haute ingénierie. Voici comment Wistant Studio est armé pour la guerre.

## 🏗️ Stratégie 1 : Horizontal Scaling (Le Clone)
Contrairement à une application classique, notre backend est **Stateless** (Souverain/Sans état).
- **Le Concept** : Le serveur ne stocke rien sur son propre disque dur qui soit vital (pas de sessions locales).
- **L'Action** : Si 30k users arrivent, on lance **10 ou 20 instances** (clones) de notre API derrière un **Load Balancer**.
- **Analogie** : C'est comme ouvrir 20 caisses au supermarché quand il y a trop de monde. Comme les caissiers n'ont pas besoin de se souvenir de toi (grâce au JWT), n'importe quel caissier peut s'occuper de ta commande.

## ⚡ Stratégie 2 : Le Bouclier Redis (Caching)
La base de données (PostgreSQL) est souvent le point faible. Si 30k users demandent la liste des apps en même temps, la DB explose.
- **La Solution** : On utilise **Redis**. 
- **Le Flux** : 
    1. L'API regarde dans Redis : "Est-ce que j'ai la liste des apps ?"
    2. Si oui (HIT), elle répond en **microsecondes** sans toucher à PostgreSQL.
    3. Si non (MISS), elle demande à PostgreSQL, stocke le résultat dans Redis pour les suivants, et répond.
- **Résultat** : PostgreSQL reste frais et disponible pour les écritures importantes (Studio), pendant que Redis gère la foule du Store.

## 📥 Stratégie 3 : Décompression de Charge (Asynchronisme)
Si 30k users essaient de générer un ZIP en même temps :
- On ne le fait pas sur le serveur principal.
- On envoie la tâche à des **Workers séparés** via BullMQ.
- On peut avoir 1 instance API pour répondre aux clics, et 5 instances Workers qui ne font que de la compression de fichiers.

## 🗄️ Stratégie 4 : Optimisation Database
Pour 30k users, PostgreSQL doit être tuné :
- **Connection Pooling** : On utilise **Prisma Accelerate** ou **PgBouncer**. Sans ça, PostgreSQL sature en essayant de gérer 30 000 connexions simultanées. Le pooler permet de réutiliser quelques centaines de connexions pour des milliers de requêtes.
- **Indexation Chirurgicale** : Chaque recherche (par nom, par tag) doit être indexée. Sans index, PostgreSQL doit lire toute la table pour chaque utilisateur. Avec index, c'est instantané.

## 🛡️ Stratégie 5 : Graceful Degradation
Si malgré tout le système sature :
- On active le **Circuit Breaker**.
- On coupe les fonctionnalités secondaires (ex: analytics en temps réel) pour préserver les fonctionnalités vitales (Browsing & Download).

---

## 🏁 Conclusion
Avec cette architecture (Stateless API + Load Balancing + Redis Cache + Connection Pooling), Wistant Studio ne craint pas les pics de trafic. C'est la différence entre un site web et une **infrastructure**.
