# 🚀 Guide d'Installation du Backend

## 📋 Prérequis
- Node.js (v22 ou supérieur)
- PostgreSQL (v13 ou supérieur)
- npm ou yarn

## 📁 Fichiers Requis

### 1. `.env`
Créez un fichier `.env` à la racine du dossier `backend` avec les variables suivantes :

```env
# Configuration du serveur
PORT=5000
NODE_ENV=development

# Configuration de la base de données
DB_HOST=localhost
DB_PORT=5432
DB_NAME=cesizen
DB_USER=votre_utilisateur
DB_PASSWORD=votre_mot_de_passe

# Clés JWT
JWT_SECRET=votre_clé_secrète_jwt
REFRESH_SECRET=votre_clé_secrète_refresh

# Configuration des emails (optionnel)
SMTP_HOST=smtp.example.com
SMTP_PORT=587
SMTP_USER=votre_email
SMTP_PASS=votre_mot_de_passe
```

### 2. `database.sql`
Le fichier de structure de la base de données est disponible dans `/backend/database/database.sql`

## 🛠️ Installation

1. **Cloner le repository**
```bash
git clone https://github.com/votre-repo/cesizen.git
cd cesizen/backend
```

2. **Installer les dépendances**
```bash
npm install
# ou
yarn install
```

3. **Configurer la base de données**
```bash
# Créer la base de données
psql -U postgres
CREATE DATABASE cesizen;
\q

# Importer la structure
psql -U postgres -d cesizen -f database/database.sql
```

4. **Démarrer le serveur**
```bash
# Mode développement
npm run dev
# ou
yarn dev

# Mode production
npm start
# ou
yarn start
```

## 🔍 Vérification de l'Installation

1. Le serveur devrait démarrer sur `http://localhost:5000`
2. Testez l'API avec la route de statut :
```bash
curl http://localhost:5000/status
```

## 🚨 Résolution des Problèmes Courants

### Erreur de connexion à la base de données
- Vérifiez que PostgreSQL est en cours d'exécution
- Vérifiez les informations de connexion dans le fichier `.env`
- Assurez-vous que l'utilisateur a les droits nécessaires

### Erreur de port déjà utilisé
```bash
# Trouvez le processus utilisant le port
lsof -i :5000
# Arrêtez le processus
kill -9 PID
```

## 📚 Documentation Supplémentaire
- [Documentation de l'API](./README.md)
- [Guide de Contribution](../CONTRIBUTING.md)
- [Politique de Sécurité](../SECURITY.md) 