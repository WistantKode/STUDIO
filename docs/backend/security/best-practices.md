# 🛡️ Sécurité : Défense en Profondeur

Dans un projet pro, la sécurité n'est pas une porte fermée à clé, c'est un **château avec plusieurs remparts**. Si un rempart tombe, les autres doivent tenir. C'est le principe de la **Défense en Profondeur**.

## 🧱 Rempart 1 : La Validation (Zod / Class-Validator)
On ne fait **jamais** confiance à ce qui vient du client.
- **Le Pourquoi** : Un hackeur peut modifier une requête HTTP pour envoyer du texte là où on attend un nombre, ou injecter du code SQL.
- **La Solution** : On utilise des `Pipes de Validation`. Si la donnée ne correspond pas exactement au moule (DTO), elle est rejetée avant même d'arriver au service.

## 🧱 Rempart 2 : L'Authentification (JWT)
On utilise des **JWT (JSON Web Tokens)**. 

### Analogie : Le Ticket de Concert
- Quand tu te connectes, le serveur te donne un Ticket (JWT).
- Ce ticket est signé par le serveur (tu ne peux pas le modifier sans briser la signature).
- À chaque fois que tu veux accéder à une ressource privée, tu montres ton ticket.
- **L'Avantage** : Le serveur n'a pas besoin de chercher dans sa base de données à chaque fois pour savoir qui tu es. Il vérifie juste la signature du ticket. C'est extrêmement rapide.

## 🧱 Rempart 3 : L'Autorisation (RBAC)
Une fois qu'on sait qui tu es (Authentification), on vérifie ce que tu as le droit de faire (Autorisation).
- On utilise des `Guards` NestJS.
- Un utilisateur peut être authentifié mais ne pas avoir le droit de supprimer un projet (Rôle `VIEWER` vs `ADMIN`).

## 🧱 Rempart 4 : La Protection Brute-Force (Throttler)
On limite le nombre d'appels à l'API.
- **Le Pourquoi** : Pour éviter qu'un script tente 10 000 mots de passe par seconde.
- **L'Action** : On installe un `Throttler`. Après 5 tentatives infructueuses, on bloque l'IP pendant 15 minutes.

## 🧱 Rempart 5 : Les Headers (Helmet)
On ajoute des en-têtes HTTP de sécurité.
- Ils empêchent par exemple que ton site soit affiché dans une `<iframe>` sur un autre site (protection contre le Clickjacking) ou que le navigateur essaie de deviner le type de fichier (Sniffing).

---

## 🛡️ Règle d'or : Least Privilege
Donne toujours le **minimum de droits** nécessaires. Si ton API n'a besoin que de lire la DB, ne lui donne pas les droits de suppression sur toute la base. C'est la base de la survie en milieu hostile (Internet).
