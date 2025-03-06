# 🏙️ Documentation des Routes des Villes

## 🌐 Base URL
```http
/api/villes
```

## 📑 Routes Disponibles

### 🔍 1. Liste des Villes
```http
GET /
```

#### 📝 Description
Récupère la liste complète des villes disponibles dans l'application.

#### 🔒 Headers Requis
```http
Authorization: Bearer <token>    // Token JWT valide
```

#### 📊 Paramètres Query
| Nom | Type | Description | Requis |
|-----|------|-------------|--------|
| search | string | Terme de recherche | ❌ |
| limit | number | Nombre maximum de résultats | ❌ |

#### ✅ Réponse Réussie (200)
```json
{
  "villes": [
    {
      "id": "number",         // ID unique de la ville
      "nom": "string",        // Nom de la ville
      "codePostal": "string", // Code postal
      "pays": "string"        // Pays de la ville
    }
  ],
  "total": "number"          // Nombre total de villes
}
```

#### ❌ Erreurs Possibles
| Code | Description |
|------|-------------|
| 401  | Non authentifié |
| 500  | Erreur serveur |

### 🎯 2. Détails d'une Ville
```http
GET /:id
```

#### 📝 Description
Récupère les informations détaillées d'une ville spécifique.

#### 🔒 Headers Requis
```http
Authorization: Bearer <token>    // Token JWT valide
```

#### 📊 Paramètres URL
| Nom | Type | Description | Requis |
|-----|------|-------------|--------|
| id | number | ID de la ville | ✅ |

#### ✅ Réponse Réussie (200)
```json
{
  "ville": {
    "id": "number",         // ID unique de la ville
    "nom": "string",        // Nom de la ville
    "codePostal": "string", // Code postal
    "pays": "string",       // Pays de la ville
    "latitude": "number",   // Latitude géographique
    "longitude": "number",  // Longitude géographique
    "population": "number"  // Population de la ville
  }
}
```

#### ❌ Erreurs Possibles
| Code | Description |
|------|-------------|
| 401  | Non authentifié |
| 404  | Ville non trouvée |
| 500  | Erreur serveur |

### 🔎 3. Recherche de Villes
```http
GET /search
```

#### 📝 Description
Recherche des villes par nom ou code postal.

#### 🔒 Headers Requis
```http
Authorization: Bearer <token>    // Token JWT valide
```

#### 📊 Paramètres Query
| Nom | Type | Description | Requis |
|-----|------|-------------|--------|
| q | string | Terme de recherche | ✅ |
| pays | string | Filtrer par pays | ❌ |
| limit | number | Nombre maximum de résultats | ❌ |

#### ✅ Réponse Réussie (200)
```json
{
  "resultats": [
    {
      "id": "number",         // ID de la ville
      "nom": "string",        // Nom de la ville
      "codePostal": "string", // Code postal
      "pays": "string"        // Pays de la ville
    }
  ],
  "total": "number"          // Nombre total de résultats
}
```

#### ❌ Erreurs Possibles
| Code | Description |
|------|-------------|
| 400  | Terme de recherche manquant |
| 401  | Non authentifié |
| 500  | Erreur serveur |

## 🔒 Sécurité

### 🛡️ Contrôles d'Accès
- Authentification JWT requise
- Validation des paramètres de recherche
- Protection contre les injections SQL

### 💡 Bonnes Pratiques
- Utilisez des index pour les recherches
- Mettez en cache les résultats fréquents
- Limitez la taille des réponses

### ⚠️ Limitations
- Maximum 100 résultats par requête
- Rate limit de 60 requêtes par minute
- Cache de 24 heures pour les données statiques 