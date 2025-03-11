# 💬 Documentation des Routes de Chat - CesiZen

## 🌐 Base URL
```http
/api/chat
```

## 📑 Routes Disponibles

### 📨 1. Envoyer un Message
```http
POST /message
```

#### 📝 Description
Envoie un message à l'assistant CesiZen et obtient une réponse personnalisée.

#### 🔒 Headers Requis
```http
Authorization: Bearer <token>    // Token JWT valide
```

#### ⚡ Corps de la Requête
```json
{
  "message": "string"    // Message de l'utilisateur
}
```

#### ✅ Réponse Réussie (200)
```json
{
  "success": true,
  "message": "string"    // Réponse de l'assistant
}
```

#### ❌ Erreurs Possibles
| Code | Description |
|------|-------------|
| 400  | Message manquant |
| 401  | Non authentifié |
| 500  | Erreur serveur |

### 📋 2. Récupérer l'Historique
```http
GET /history
```

#### 📝 Description
Récupère l'historique complet des conversations de l'utilisateur.

#### 🔒 Headers Requis
```http
Authorization: Bearer <token>    // Token JWT valide
```

#### ✅ Réponse Réussie (200)
```json
[
  {
    "content": "string",      // Contenu du message
    "is_user": "boolean",     // true si message utilisateur, false si assistant
    "timestamp": "date"       // Date et heure du message
  }
]
```

#### ❌ Erreurs Possibles
| Code | Description |
|------|-------------|
| 401  | Non authentifié |
| 500  | Erreur serveur |

### 🗑️ 3. Supprimer l'Historique
```http
DELETE /history
```

#### 📝 Description
Supprime tout l'historique des conversations de l'utilisateur.

#### 🔒 Headers Requis
```http
Authorization: Bearer <token>    // Token JWT valide
```

#### ✅ Réponse Réussie (200)
```json
{
  "message": "Historique supprimé avec succès"
}
```

#### ❌ Erreurs Possibles
| Code | Description |
|------|-------------|
| 401  | Non authentifié |
| 500  | Erreur serveur |

## 🤖 Configuration de l'Assistant

### ⚙️ Paramètres Techniques
| Paramètre | Valeur |
|-----------|--------|
| Modèle | mistral-tiny |
| Température | 0.7 |
| Top P | 0.9 |
| Tokens maximum | 350 |

### 🎯 Comportement de l'Assistant
- 🗣️ Répond en français (sauf si question en anglais)
- 💝 Ton bienveillant et rassurant
- 📝 Réponses concises (3-4 phrases maximum)
- 🎓 Solutions adaptées aux étudiants
- 🧘‍♂️ Exercices courts et simples
- ⚕️ Pas de conseils médicaux

## 🔒 Sécurité

### 🛡️ Contrôles d'Accès
- Authentification JWT requise pour toutes les routes
- Messages sauvegardés de manière sécurisée
- Historique isolé par utilisateur

### 💡 Bonnes Pratiques
- Vérifiez toujours la validité du token
- Limitez la taille des messages à 1000 caractères
- Gérez les timeouts de réponse (30 secondes max)

### ⚠️ Limitations
- Maximum 50 messages par minute
- Taille maximale de l'historique : 100 messages
- Temps de réponse maximum : 30 secondes 
