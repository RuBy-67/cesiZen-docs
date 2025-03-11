# 📚 Documentation de l'API Cesizen

## 🌟 Introduction

Bienvenue dans la documentation de l'API Cesizen. Cette API permet de gérer le suivi émotionnel des utilisateurs et fournit diverses fonctionnalités pour améliorer leur bien-être.

## 🔑 Authentification

L'API utilise l'authentification JWT (JSON Web Token). La plupart des routes nécessitent un token d'accès valide qui doit être inclus dans l'en-tête de la requête :

```http
Authorization: Bearer <votre_token>
```

## 📑 Sommaire des Routes

### 🔐 [Authentification](./auth.md)
- `POST /api/auth/login` - Connexion utilisateur
- `POST /api/auth/refresh` - Rafraîchissement du token

### 😊 [Émotions](./emotion.md)
- `GET /api/emotions` - Liste des émotions
- `GET /api/emotions/base/:id` - Émotions par base
- `POST /api/emotions` - Ajout d'émotion (Admin)

### 🎯 [Bases d'Émotions](./emotionBase.md)
- `GET /api/emotion-bases` - Liste des bases
- `POST /api/emotion-bases` - Ajout de base (Admin)

### 📊 [Statistiques](./statistique.md)
- `GET /api/statistiques/:id` - Statistiques personnelles
- `GET /api/statistiques/global` - Statistiques globales (Admin)

### 📝 [Trackers](./tracker.md)
- `POST /api/trackers` - Ajout d'un tracker
- `GET /api/trackers/history` - Historique des trackers

### 👥 [Utilisateurs](./users.md)
- `GET /api/users` - Liste des utilisateurs (Admin)
- `GET /api/users/:id` - Détails d'un utilisateur

### 🏙️ [Villes](./villes.md)
- `GET /api/villes` - Liste des villes
- `GET /api/villes/search` - Recherche de villes
- `GET /api/villes/:id` - Détails d'une ville

### 📨 [Chat](.\chat.md)
- `POST /api/message` - Envoyer un message
- `GET /api/history` - Récupérer l'Historique
- `DELETE /api/history ` - Supprimmer l'historique

## 🛠️ Installation

Pour installer et configurer le backend, consultez notre [Guide d'Installation](./installation.md).

## 🔒 Sécurité

- Toutes les routes protégées nécessitent un token JWT valide
- Les mots de passe sont hachés avec bcrypt
- Les tokens expirent après une période définie
- Protection CORS activée
- Validation des données entrantes

## 📝 Conventions de Nommage

- Les URLs utilisent le format kebab-case
- Les paramètres JSON utilisent le format camelCase
- Les réponses JSON suivent un format cohérent

## 🚀 Versions

- Version actuelle : 1.0.0
- Node.js : ≥ 14.x
- PostgreSQL : ≥ 13.x

## 👥 Support

Pour toute question ou problème :
- 📧 Email : support@cesizen.com
- 💬 Discord : [Serveur Cesizen](https://discord.gg/cesizen)
- 🐛 Issues : [GitHub Issues](https://github.com/cesizen/issues) 
