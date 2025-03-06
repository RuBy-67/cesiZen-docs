# 🔐 Documentation des Routes d'Authentification

## 🌐 Base URL
```http
/api/auth
```

## 📑 Routes Disponibles

### 🔑 1. Connexion
```http
POST /login
```

#### 📝 Description
Authentifie un utilisateur et génère des tokens d'accès et de rafraîchissement.

#### ⚡ Requête
```json
{
  "email": "string",     // Adresse email de l'utilisateur
  "password": "string"   // Mot de passe
}
```

#### ✅ Réponse Réussie (200)
```json
{
  "message": "Connexion réussie",
  "accessToken": "string",    // Token JWT pour l'authentification
  "refreshToken": "string"    // Token pour rafraîchir l'accès
}
```

#### ❌ Erreurs Possibles
| Code | Description |
|------|-------------|
| 401  | Utilisateur non trouvé ou mot de passe incorrect |
| 500  | Erreur serveur |

### 🔄 2. Rafraîchissement du Token
```http
POST /refresh
```

#### 📝 Description
Rafraîchit le token d'accès en utilisant un token de rafraîchissement valide.

#### ⚡ Requête
```json
{
  "token": "string"    // Token de rafraîchissement
}
```

#### ✅ Réponse Réussie (200)
```json
{
  "accessToken": "string"    // Nouveau token JWT
}
```

#### ❌ Erreurs Possibles
| Code | Description |
|------|-------------|
| 401  | Token requis |
| 403  | Token invalide ou expiré |
| 500  | Erreur serveur |

## 🔒 Sécurité

### 🛡️ Mesures de Protection
- Tokens JWT pour l'authentification
- Expiration du token d'accès : 1 heure
- Expiration du token de rafraîchissement : 7 jours
- Hachage des mots de passe avec bcrypt

### 💡 Bonnes Pratiques
- Stockez les tokens de manière sécurisée
- Rafraîchissez le token avant son expiration
- Ne transmettez jamais les tokens en clair
- Utilisez HTTPS en production

### ⚠️ Notes Importantes
- Les tokens sont sensibles à la casse
- Les tokens expirés ne peuvent pas être réutilisés
- Maximum 3 tentatives de connexion par minute 