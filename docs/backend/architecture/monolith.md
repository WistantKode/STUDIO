# 🏛️ Architecture : Pourquoi le Monolithe Modulaire ?

Si tu veux construire une "Machine de Guerre", tu dois comprendre la différence entre un moteur de Formule 1 et un moteur de tracteur. Le **Monolithe Modulaire** est notre moteur de F1 : compact, mais extrêmement organisé.

## 🏘️ L'Analogie : Le Manoir vs La Ville
Imagine que tu construis plusieurs maisons pour différentes familles (Microservices). Si le facteur veut passer d'une maison à l'autre, il doit sortir dans la rue, prendre sa voiture, et attendre au feu rouge (Latence réseau). S'il manque de sel dans une maison, il doit appeler les autres (Appels API complexes).

**Le Monolithe Modulaire**, c'est un **Manoir massif**. 
- La Cuisine (Module Ingestion), la Chambre (Module IAM) et le Salon (Module Store) sont sous le même toit.
- Pour passer du sel (Data) d'une pièce à l'autre, il suffit de passer la porte (Appel de fonction interne). 
- C'est **instantané**, **sécurisé** et tout le monde partage le même système de plomberie (Prisma / Database).

## 🚀 Pourquoi NestJS ? (Le Chef d'Orchestre)
NestJS n'est pas juste un framework, c'est un **cadre de pensée**. Il nous impose la **Dependency Injection (DI)** (Injection de Dépendances).

### C'est quoi la DI ? (Analogie du Robot)
Imagine que tu as un Robot (un Service). Pour qu'il fonctionne, il a besoin d'une Batterie.
- **Sans DI** : Le Robot fabrique lui-même sa batterie. S'il y a un défaut dans la batterie, tu dois démonter le Robot.
- **Avec DI** : Tu donnes la batterie au Robot quand tu l'allumes. Si tu veux tester le Robot, tu peux lui donner une batterie factice.
- **Conséquence** : Ton code est **testable**, **découplable** et **propre**.

## 🧩 Structure d'un Module (La Cellule de base)
Dans NestJS, tout est un `Module`. Un module est comme une boîte noire qui contient :
1. **Controller** : Le portier. Il reçoit les requêtes HTTP, vérifie les papiers (Validation), et dit "Entrez".
2. **Service** : Le cerveau. C'est ici que réside la logique. "Si le repo GitHub a plus de 100 stars, alors mets-le en avant".
3. **Repository (Prisma)** : La mémoire. C'est le lien avec la base de données.

## ⚖️ Le Choix de la Simplicité (La Vérité Technique)
On aurait pu faire 5 APIs différentes. Pourquoi on ne l'a pas fait ?
- **Coût Cognitif** : Plus tu as de services, plus tu perds de temps à configurer Docker, les déploiements, et les secrets.
- **Cohérence des données** : Dans un monolithe, si une transaction échoue, tout s'arrête proprement. Dans des microservices, tu peux te retrouver avec un projet créé sur l'API mais pas d'entrée dans le Store (Incohérence).

**Conclusion** : On commence en Monolithe pour la puissance et la vitesse. Si un jour le Store reçoit 1 million de clics par seconde, on pourra découper le module `Store` pour en faire un service indépendant sans effort, car notre code est déjà structuré par modules.
