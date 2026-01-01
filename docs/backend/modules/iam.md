# 🔑 Module : IAM (Les Clés du Royaume)

Le module IAM (Identity & Access Management) est le cœur de la confiance dans Wistant Studio. C'est ici que l'on définit qui tu es et ce que tu peux toucher.

## 🔐 L'Authentification Double Facteur (2FA)
Pour ton Studio (Dashboard), le mot de passe ne suffit pas. On veut une preuve que c'est bien toi.

### Le Processus technique :
1. **L'Enregistrement** : Le serveur génère une clé secrète et te montre un QR Code.
2. **La Validation** : Ton application (Google Authenticator) utilise cette clé pour générer un code de 6 chiffres qui change toutes les 30 secondes (TOTP - Time-based One-Time Password).
3. **Le Pourquoi** : Même si quelqu'un vole ton mot de passe, il ne peut pas entrer sans ton téléphone. Pour un projet qui expose tes compétences, c'est ta protection ultime contre le sabotage.

## 🔄 Refresh Tokens : La sécurité sans la frustration
On ne veut pas que tu doives te reconnecter toutes les 15 minutes.
- **Access Token** : Très courte durée (15 min). Il sert à faire les requêtes.
- **Refresh Token** : Longue durée (7 jours). Il reste caché dans un cookie sécurisé (`HttpOnly`).
- **Le Flux** : Quand l'Access Token expire, le frontend envoie discrètement le Refresh Token pour en obtenir un nouveau. Si le frontend est piraté, le pirate n'a qu'un token de 15 minutes. Le Refresh Token, lui, est protégé dans le navigateur et inaccessible en JavaScript.

## 👮‍♂️ RBAC (Role-Based Access Control)
On utilise des **Décorateurs** NestJS : `@Roles(Role.Admin)`.
- Si tu oublies de mettre le décorateur, la route est protégée par défaut (Sécurité par défaut).

## 💡 Conseil de Mentor
Utilise toujours des **UUID** (identifiants uniques complexes) au lieu d'IDs simples (1, 2, 3) pour tes utilisateurs dans les URLs. Ça évite que quelqu'un puisse deviner l'ID d'un autre utilisateur en changeant simplement le chiffre dans l'URL.
