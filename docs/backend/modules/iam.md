# Module : Identity & Access Management (IAM)

L'IAM de Wistant Studio est conçu pour être impénétrable tout en offrant une expérience fluide pour l'administrateur (Studio).

## 🔒 Technologies
- **NestJS Identity** / Passport.
- **JWT (JSON Web Tokens)** pour l'authentification sans état (stateless).
- **Argon2** pour le hashage des mots de passe.

## 🚀 Fonctionnalités
1. **Auth Double Facteur (2FA)** : Requis pour accéder au \`studio.wistant.dev\`.
2. **Refresh Tokens** : Rotation des tokens pour minimiser les risques en cas de vol.
3. **RBAC (Role-Based Access Control)** :
    - \`ADMIN\` : Contrôle total (publication, modification).
    - \`VIEWER\` : Consultation des analytics uniquement.

## 🤝 Bonnes Pratiques Dev
- Ne jamais logger un mot de passe ou un token.
- Toujours utiliser un décorateur \`@CurrentUser\` pour récupérer l'identité.
- Valider systématiquement l'expiration des tokens.
