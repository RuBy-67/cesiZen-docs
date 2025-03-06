# 🎯 Documentation des Routes des Bases d'Émotions

## 🌐 Base URL
```http
/api/emotion-bases
```

## 📑 Routes Disponibles

### 📋 1. Liste des Bases d'Émotions
```http
GET /
```

#### 📝 Description
Récupère la liste complète des catégories d'émotions disponibles dans l'application.

#### 🔒 Headers Requis
```http
Authorization: Bearer <token>    // Token JWT valide
```

#### ✅ Réponse Réussie (200)
```json
[
  {
    "emotion_base_id": "number",      // Identifiant unique de la base
    "emotion_base_name": "string"     // Nom de la catégorie d'émotion
  }
]
```

#### ❌ Erreurs Possibles
| Code | Description |
|------|-------------|
| 401  | Non authentifié |
| 500  | Erreur serveur |

### ➕ 2. Ajouter une Base d'Émotion
```http
POST /
```

#### 📝 Description
Crée une nouvelle catégorie d'émotion dans le système (réservé aux administrateurs).

#### 🔒 Headers Requis
```http
Authorization: Bearer <token>    // Token JWT valide d'administrateur
```

#### ⚡ Corps de la Requête
```json
{
  "emotionBaseName": "string"    // Nom de la nouvelle catégorie d'émotion
}
```

#### ✅ Réponse Réussie (201)
```json
{
  "message": "Catégorie d'émotion ajoutée avec succès",
  "emotionBase": {
    "emotion_base_id": "number",      // Identifiant unique généré
    "emotion_base_name": "string"     // Nom de la catégorie créée
  }
}
```

#### ❌ Erreurs Possibles
| Code | Description |
|------|-------------|
| 401  | Non authentifié |
| 403  | Non autorisé (non admin) |
| 400  | Nom invalide ou déjà existant |
| 500  | Erreur serveur |

## 🔒 Sécurité

### 🛡️ Contrôles d'Accès
- Authentification JWT requise pour toutes les routes
- Droits administrateur requis pour l'ajout de bases
- Validation des données entrantes

### 💡 Bonnes Pratiques
- Vérifiez l'unicité des noms de bases
- Utilisez des noms descriptifs et clairs
- Limitez le nombre de bases pour maintenir la clarté

### ⚠️ Limitations
- Maximum 20 bases d'émotions
- Noms limités à 30 caractères
- Caractères spéciaux non autorisés dans les noms 