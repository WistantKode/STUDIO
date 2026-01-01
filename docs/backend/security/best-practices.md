# Sécurité : Les Règles d'Or

La sécurité n'est pas une option, c'est l'un des piliers du projet "Machine de Guerre".

## 🛡️ Stratégies d'Infrastructures
1. **Secrets Isolation** : Utilisation de variables d'environnement (Vault ou secrets GitHub). Jamais de secrets dans le code.
2. **Rate Limiting** : Protection contre les attaques Brute Force via \`@nestjs/throttler\`.
3. **CORS Monitoring** : Seuls les domaines \`*.wistant.dev\` sont autorisés à communiquer avec l'API.

## 💻 Sécurité au Niveau du Code
- **Validation Pipe** : Tout input utilisateur est passé au crible par Zod ou Class-Validator.
- **Sanitization** : Nettoyage des chaînes de caractères pour éviter les injections XSS/SQL.
- **Dependency Scan** : Audit automatique des dépendances à chaque build via \`npm audit\` ou Snyk.

## 📝 Check-list de Publication
- [ ] Mots de passe hashés.
- [ ] HTTPS forcé.
- [ ] Headers de sécurité (Helmet) activés.
- [ ] Audit logs pour les actions sensibles.
