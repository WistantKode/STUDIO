# Architecture : Le Monolithe Modulaire

Le backend de Wistant Studio est conçu comme un **Monolithe Modulaire**. Ce choix a été fait pour maximiser la vitesse de développement tout en permettant une transition future vers des microservices si nécessaire.

## 🧠 Le Concept
Au lieu de séparer physiquement les services sur différents serveurs, nous les séparons **logiquement** au sein de la même application NestJS.

### Avantages
- **Communication In-Process** : Pas de latence réseau entre les services.
- **Partage de Types** : Les interfaces et DTOs sont immédiatement disponibles.
- **Maintenance Simplifiée** : Un seul déploiement, une seule base de données Prisma.

## 🛠️ Règles d'Isolation
Pour que le monolithe reste propre, chaque module doit suivre ces règles :
1. **Bounded Context** : Un module ne doit jamais modifier directement les données d'un autre module. Il doit passer par un service injecté ou des évènements internes.
2. **DTOs Stricts** : Chaque entrée/sortie doit être mappée via des DTOs (Data Transfer Objects).
3. **Services Isolés** : La logique métier réside dans les services, les contrôleurs ne sont que des "portiers".

## 🔄 Flux de Données Type
1. Request → **Controller** (Validation)
2. Controller → **Service** (Logique métier)
3. Service → **Prisma** (Persistence)
4. Data → **Mapper** (Transformation pour l'utilisateur)
5. Response → Client
