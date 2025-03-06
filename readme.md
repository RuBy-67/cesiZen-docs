# Cesizen - Application de Suivi des Émotions

Cette application permet aux utilisateurs de suivre et d'enregistrer leurs émotions quotidiennes. Elle est construite avec une architecture moderne utilisant Node.js pour le backend et Ionic/Angular pour le frontend.

## 🚀 Prérequis

- Node.js (v23 ou supérieur)
- npm (v9 ou supérieur)
- Ionic CLI
- Angular CLI


- [Docs serveur Backend](./back-end/README.md) 
- [Docs serveur Front-end](./front-end/readme.md)
## 📦 Installation

### Installation globale des outils

```bash
# Installation d'Ionic CLI
npm install -g @ionic/cli

# Installation d'Angular CLI
npm install -g @angular/cli
```

### Backend (Node.js)

```bash
# Naviguer vers le dossier backend
cd backend

# Installer les dépendances
npm install

# Créer le fichier .env avec les variables d'environnement nécessaires
cp .env.example .env
```

### Frontend (Ionic/Angular)

```bash
# Naviguer vers le dossier frontend
cd frontend

# Installer les dépendances
npm install
```

## 🔧 Configuration

### Backend (.env)

Créez un fichier `.env` dans le dossier `backend` avec les variables suivantes :

```env
PORT=5000
DB_HOST=localhost
DB_USER=votre_utilisateur
DB_PASSWORD=votre_mot_de_passe
DB_NAME=votre_base_de_donnees
JWT_SECRET=votre_secret_jwt
```

## 🚀 Lancement de l'application

### Démarrer le Backend

```bash
# Dans le dossier backend
npm run dev
```
Le serveur backend démarrera sur http://localhost:5000

### Démarrer le Frontend

```bash
# Dans le dossier frontend
ionic serve
```
L'application frontend sera accessible sur http://localhost:8100

## 📱 Fonctionnalités principales

- 🔐 Authentification des utilisateurs
- 📝 Enregistrement des émotions
- 🎯 Sélection d'émotions de base et spécifiques
- 💭 Ajout de commentaires aux émotions
- 📊 Historique des émotions enregistrées

## 🎨 Palette de couleurs

```scss
background: "#EFE8D6" // Fond principal
primary: "#7A9A8B"   // Couleur principale
secondary: "#A9C39C" // Couleur secondaire
accent: "#C0D0E0"    // Accent
highlight: "#F2BC7E" // Surbrillance
soft: "#D8D0A1"      // Couleur douce
```

## 🛠️ Technologies utilisées

### Backend
- Node.js
- Express
- MySQL
- JWT pour l'authentification

### Frontend
- Ionic Framework
- Angular
- TailwindCSS
- TypeScript

## 📝 Notes de développement

- Le backend utilise une architecture RESTful
- L'authentification est gérée via JWT (JSON Web Tokens)
- Le frontend utilise une approche modulaire avec des composants réutilisables
- Les styles sont gérés avec une combinaison de TailwindCSS et de styles Ionic personnalisés

## 🤝 Contribution

1. Fork le projet
2. Créez votre branche (`git checkout -b feature/AmazingFeature`)
3. Committez vos changements (`git commit -m 'Add some AmazingFeature'`)
4. Push vers la branche (`git push origin feature/AmazingFeature`)
5. Ouvrez une Pull Request

## 📄 Licence

Ce projet est sous licence MIT. Voir le fichier `LICENSE` pour plus de détails.
