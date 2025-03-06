# 👥 Documentation des Routes Utilisateurs

## 🌐 Base URL
```http
/api/users
```

## 📑 Routes Disponibles

### 👤 1. Profil Utilisateur
```http
GET /profile
```

#### 📝 Description
Récupère les informations du profil de l'utilisateur connecté.

#### 🔒 Headers Requis
```http
Authorization: Bearer <token>    // Token JWT valide
```

#### ✅ Réponse Réussie (200)
```json
{
  "user": {
    "id": "number",            // ID unique de l'utilisateur
    "email": "string",         // Adresse email
    "username": "string",      // Nom d'utilisateur
    "ville": {
      "id": "number",         // ID de la ville
      "nom": "string"         // Nom de la ville
    },
    "dateInscription": "string" // Date d'inscription
  }
}
```

#### ❌ Erreurs Possibles
| Code | Description |
|------|-------------|
| 401  | Non authentifié |
| 404  | Utilisateur non trouvé |
| 500  | Erreur serveur |

### ✏️ 2. Modifier le Profil
```http
PUT /profile
```

#### 📝 Description
Modifie les informations du profil de l'utilisateur connecté.

#### 🔒 Headers Requis
```http
Authorization: Bearer <token>    // Token JWT valide
```

#### ⚡ Corps de la Requête
```json
{
  "username": "string",     // Nouveau nom d'utilisateur (optionnel)
  "email": "string",       // Nouvelle adresse email (optionnel)
  "villeId": "number",     // Nouvel ID de ville (optionnel)
  "password": "string"     // Nouveau mot de passe (optionnel)
}
```

#### ✅ Réponse Réussie (200)
```json
{
  "message": "Profil mis à jour avec succès",
  "user": {
    "id": "number",            // ID de l'utilisateur
    "email": "string",         // Email mis à jour
    "username": "string",      // Nom d'utilisateur mis à jour
    "ville": {
      "id": "number",         // ID de la ville
      "nom": "string"         // Nom de la ville
    }
  }
}
```

#### ❌ Erreurs Possibles
| Code | Description |
|------|-------------|
| 400  | Données invalides |
| 401  | Non authentifié |
| 404  | Utilisateur ou ville non trouvé |
| 409  | Email déjà utilisé |
| 500  | Erreur serveur |

### 🗑️ 3. Supprimer le Compte
```http
DELETE /profile
```

#### 📝 Description
Supprime définitivement le compte de l'utilisateur connecté.

#### 🔒 Headers Requis
```http
Authorization: Bearer <token>    // Token JWT valide
```

#### ⚡ Corps de la Requête
```json
{
  "password": "string"      // Mot de passe pour confirmation
}
```

#### ✅ Réponse Réussie (200)
```json
{
  "message": "Compte supprimé avec succès"
}
```

#### ❌ Erreurs Possibles
| Code | Description |
|------|-------------|
| 400  | Mot de passe incorrect |
| 401  | Non authentifié |
| 500  | Erreur serveur |

## 🔒 Sécurité

### 🛡️ Contrôles d'Accès
- Authentification JWT requise
- Validation des données sensibles
- Protection contre les injections SQL

### 💡 Bonnes Pratiques
- Validez les formats d'email
- Hachez les mots de passe
- Limitez les tentatives de modification

### ⚠️ Limitations
- Maximum 5 changements de mot de passe par jour
- Username limité à 30 caractères
- Email limité à 100 caractères 