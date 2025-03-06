# 😊 Documentation des Routes des Émotions

## 🌐 Base URL
```http
/api/emotions
```

## 📑 Routes Disponibles

### 📋 1. Liste des Émotions
```http
GET /
```

#### 📝 Description
Récupère la liste complète des émotions disponibles dans l'application.

#### 🔒 Headers Requis
```http
Authorization: Bearer <token>    // Token JWT valide
```

#### ✅ Réponse Réussie (200)
```json
[
  {
    "id": "number",         // Identifiant unique de l'émotion
    "name": "string",       // Nom de l'émotion
    "baseId": "number"      // Identifiant de la catégorie d'émotion
  }
]
```

#### ❌ Erreurs Possibles
| Code | Description |
|------|-------------|
| 401  | Non authentifié |
| 500  | Erreur serveur |

### 🎯 2. Émotions par Base
```http
GET /base/:id
```

#### 📝 Description
Récupère toutes les émotions associées à une catégorie spécifique.

#### 🔒 Headers Requis
```http
Authorization: Bearer <token>    // Token JWT valide
```

#### 📊 Paramètres URL
| Paramètre | Type | Description |
|-----------|------|-------------|
| id | number | ID de la base d'émotion |

#### ✅ Réponse Réussie (200)
```json
[
  {
    "id": "number",         // Identifiant unique de l'émotion
    "name": "string",       // Nom de l'émotion
    "baseId": "number"      // Identifiant de la catégorie d'émotion
  }
]
```

#### ❌ Erreurs Possibles
| Code | Description |
|------|-------------|
| 401  | Non authentifié |
| 404  | Base d'émotion non trouvée |
| 500  | Erreur serveur |

### ➕ 3. Ajouter une Émotion
```http
POST /
```

#### 📝 Description
Ajoute une nouvelle émotion dans le système (réservé aux administrateurs).

#### 🔒 Headers Requis
```http
Authorization: Bearer <token>    // Token JWT valide d'administrateur
```

#### ⚡ Corps de la Requête
```json
{
  "emotionName": "string",      // Nom de la nouvelle émotion
  "emotionBaseId": "number"     // ID de la catégorie d'émotion
}
```

#### ✅ Réponse Réussie (201)
```json
{
  "message": "Émotion ajoutée avec succès",
  "emotion": {
    "id": "number",         // Identifiant unique de l'émotion créée
    "name": "string",       // Nom de l'émotion
    "baseId": "number"      // Identifiant de la catégorie
  }
}
```

#### ❌ Erreurs Possibles
| Code | Description |
|------|-------------|
| 401  | Non authentifié |
| 403  | Non autorisé (non admin) |
| 400  | Données invalides |
| 500  | Erreur serveur |

## 🔒 Sécurité

### 🛡️ Contrôles d'Accès
- Authentification JWT requise pour toutes les routes
- Droits administrateur requis pour l'ajout d'émotions
- Validation des données entrantes

### 💡 Bonnes Pratiques
- Vérifiez toujours la validité du token
- Utilisez les IDs appropriés pour les bases d'émotions
- Validez les noms d'émotions avant l'envoi

### ⚠️ Limitations
- Maximum 50 émotions par base
- Noms d'émotions limités à 50 caractères
- Requêtes limitées à 100 par minute par utilisateur 