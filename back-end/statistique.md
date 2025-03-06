# 📊 Documentation des Routes des Statistiques

## 🌐 Base URL
```http
/api/statistiques
```

## 📑 Routes Disponibles

### 📈 1. Statistiques Personnelles
```http
GET /:id
```

#### 📝 Description
Récupère les statistiques détaillées d'un utilisateur pour une période spécifique.

#### 🔒 Headers Requis
```http
Authorization: Bearer <token>    // Token JWT valide
```

#### 📊 Paramètres
| Type | Nom | Description | Requis |
|------|-----|-------------|--------|
| URL | id | ID de l'utilisateur | ✅ |
| Query | periode | Type de période (semaine, mois, trimestre) | ✅ |

#### ✅ Réponse Réussie (200)
```json
{
  "statistiques": {
    "periode": "string",              // Période analysée
    "total_emotions": "number",       // Nombre total d'émotions enregistrées
    "emotions_par_categorie": [
      {
        "categorie": "string",        // Nom de la catégorie
        "count": "number"             // Nombre d'émotions dans cette catégorie
      }
    ],
    "evolution_temporelle": [
      {
        "date": "string",            // Date au format YYYY-MM-DD
        "count": "number"            // Nombre d'émotions ce jour
      }
    ]
  }
}
```

#### ❌ Erreurs Possibles
| Code | Description |
|------|-------------|
| 400  | Période invalide |
| 401  | Non authentifié |
| 403  | Accès non autorisé |
| 500  | Erreur serveur |

### 📊 2. Statistiques Globales
```http
GET /global
```

#### 📝 Description
Récupère les statistiques globales de tous les utilisateurs (réservé aux administrateurs).

#### 🔒 Headers Requis
```http
Authorization: Bearer <token>    // Token JWT valide d'administrateur
```

#### 📊 Paramètres Query
| Nom | Type | Description | Requis |
|-----|------|-------------|--------|
| periode | string | Type de période (semaine, mois, trimestre) | ✅ |

#### ✅ Réponse Réussie (200)
```json
{
  "statistiques": {
    "periode": "string",                    // Période analysée
    "total_utilisateurs_actifs": "number",  // Nombre d'utilisateurs actifs
    "total_emotions": "number",             // Total des émotions enregistrées
    "emotions_par_categorie": [
      {
        "categorie": "string",              // Nom de la catégorie
        "count": "number"                   // Nombre d'émotions
      }
    ],
    "evolution_temporelle": [
      {
        "date": "string",                   // Date au format YYYY-MM-DD
        "count": "number"                   // Nombre d'émotions
      }
    ]
  }
}
```

#### ❌ Erreurs Possibles
| Code | Description |
|------|-------------|
| 400  | Période invalide |
| 401  | Non authentifié |
| 403  | Non autorisé (non admin) |
| 500  | Erreur serveur |

## 🔒 Sécurité

### 🛡️ Contrôles d'Accès
- Authentification JWT requise
- Vérification des droits d'accès aux données
- Protection contre les injections SQL

### 💡 Bonnes Pratiques
- Utilisez des périodes valides
- Mettez en cache les résultats fréquemment demandés
- Limitez la taille des réponses

### ⚠️ Limitations
- Maximum 1000 points de données par requête
- Cache de 5 minutes pour les statistiques globales
- Maximum 100 requêtes par heure par utilisateur 