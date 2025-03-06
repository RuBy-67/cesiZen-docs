# 🎯 Documentation des Routes du Tracker d'Émotions

## 🌐 Base URL
```http
/api/tracker
```

## 📑 Routes Disponibles

### 📝 1. Enregistrer une Émotion
```http
POST /
```

#### 📝 Description
Enregistre une nouvelle émotion pour l'utilisateur connecté.

#### 🔒 Headers Requis
```http
Authorization: Bearer <token>    // Token JWT valide
```

#### ⚡ Corps de la Requête
```json
{
  "emotionId": "number",        // ID de l'émotion ressentie
  "intensite": "number",        // Niveau d'intensité (1-5)
  "commentaire": "string",      // Commentaire optionnel
  "date": "string"             // Date au format YYYY-MM-DD HH:mm:ss
}
```

#### ✅ Réponse Réussie (201)
```json
{
  "message": "Émotion enregistrée avec succès",
  "tracker": {
    "id": "number",            // ID de l'enregistrement
    "userId": "number",        // ID de l'utilisateur
    "emotionId": "number",     // ID de l'émotion
    "intensite": "number",     // Niveau d'intensité
    "commentaire": "string",   // Commentaire
    "date": "string"          // Date d'enregistrement
  }
}
```

#### ❌ Erreurs Possibles
| Code | Description |
|------|-------------|
| 400  | Données invalides |
| 401  | Non authentifié |
| 404  | Émotion non trouvée |
| 500  | Erreur serveur |

### 📅 2. Historique des Émotions
```http
GET /historique
```

#### 📝 Description
Récupère l'historique des émotions enregistrées par l'utilisateur.

#### 🔒 Headers Requis
```http
Authorization: Bearer <token>    // Token JWT valide
```

#### 📊 Paramètres Query
| Nom | Type | Description | Requis |
|-----|------|-------------|--------|
| debut | string | Date de début (YYYY-MM-DD) | ✅ |
| fin | string | Date de fin (YYYY-MM-DD) | ✅ |

#### ✅ Réponse Réussie (200)
```json
{
  "historique": [
    {
      "id": "number",            // ID de l'enregistrement
      "emotion": {
        "id": "number",          // ID de l'émotion
        "name": "string",        // Nom de l'émotion
        "baseId": "number"       // ID de la base d'émotion
      },
      "intensite": "number",     // Niveau d'intensité
      "commentaire": "string",   // Commentaire
      "date": "string"          // Date d'enregistrement
    }
  ]
}
```

#### ❌ Erreurs Possibles
| Code | Description |
|------|-------------|
| 400  | Dates invalides |
| 401  | Non authentifié |
| 500  | Erreur serveur |

### 🗑️ 3. Supprimer un Enregistrement
```http
DELETE /:id
```

#### 📝 Description
Supprime un enregistrement d'émotion spécifique.

#### 🔒 Headers Requis
```http
Authorization: Bearer <token>    // Token JWT valide
```

#### 📊 Paramètres URL
| Nom | Type | Description | Requis |
|-----|------|-------------|--------|
| id | number | ID de l'enregistrement | ✅ |

#### ✅ Réponse Réussie (200)
```json
{
  "message": "Enregistrement supprimé avec succès"
}
```

#### ❌ Erreurs Possibles
| Code | Description |
|------|-------------|
| 401  | Non authentifié |
| 403  | Non autorisé |
| 404  | Enregistrement non trouvé |
| 500  | Erreur serveur |

## 🔒 Sécurité

### 🛡️ Contrôles d'Accès
- Authentification JWT requise
- Vérification de propriété des enregistrements
- Validation des données entrantes

### 💡 Bonnes Pratiques
- Validez les dates et l'intensité
- Limitez la taille des commentaires
- Utilisez des timestamps UTC

### ⚠️ Limitations
- Maximum 10 enregistrements par heure
- Commentaires limités à 500 caractères
- Historique limité à 30 jours par requête 