# 🧪 Cahier de Tests - Cersizen

## 📋 Table des Matières
1. [Tests Fonctionnels](#-tests-fonctionnels)
2. [Tests de Performance](#-tests-de-performance)
3. [Tests de Sécurité](#-tests-de-sécurité)
4. [Tests d'Interface](#-tests-dinterface)
5. [Tests de Compatibilité](#-tests-de-compatibilité)

## 🔍 Tests Fonctionnels

### 🔐 1. Authentication

#### 1.1 Inscription
| ID | Description | Étapes | Résultat Attendu | Statut |
|----|-------------|--------|------------------|---------|
| AUTH-01 | Inscription réussie | 1. Accéder à la page d'inscription<br>2. Remplir email valide<br>3. Remplir mot de passe valide<br>4. Confirmer mot de passe<br>5. Soumettre | - Compte créé<br>- Redirection dashboard<br>- Message succès | ⬜ |
| AUTH-02 | Email invalide | 1. Saisir email invalide<br>2. Soumettre | Message d'erreur format | ⬜ |
| AUTH-03 | Mot de passe faible | 1. Saisir mot de passe < 8 caractères | Message d'erreur sécurité | ⬜ |
| AUTH-04 | Email existant | 1. Utiliser email déjà enregistré | Message email déjà utilisé | ⬜ |

#### 1.2 Connexion
| ID | Description | Étapes | Résultat Attendu | Statut |
|----|-------------|--------|------------------|---------|
| AUTH-05 | Connexion réussie | 1. Saisir email valide<br>2. Saisir mot de passe correct<br>3. Soumettre | - Connexion réussie<br>- Redirection dashboard | ⬜ |
| AUTH-06 | Identifiants invalides | 1. Saisir mauvais email/mot de passe | Message d'erreur | ⬜ |
| AUTH-07 | Déconnexion | 1. Cliquer sur déconnexion | - Session terminée<br>- Redirection accueil | ⬜ |


#### 1.3 Gestion de profil

| ID       | Description                  | Étapes                                                                 | Résultat Attendu                                                                 | Statut |
|----------|------------------------------|-----------------------------------------------------------------------|----------------------------------------------------------------------------------|--------|
| PROF-01  | Mise à jour du profil        | 1. Accéder à la page de profil<br>2. Modifier les informations<br>3. Soumettre | - Informations mises à jour<br>- Message de confirmation                        | ⬜      |
| PROF-02  | Changement de mot de passe   | 1. Accéder à la section mot de passe<br>2. Saisir ancien mot de passe<br>3. Saisir nouveau mot de passe<br>4. Confirmer nouveau mot de passe<br>5. Soumettre | - Mot de passe mis à jour<br>- Message de confirmation                          | ⬜      |
| PROF-03  | Validation des informations  | 1. Accéder à la page de profil<br>2. Vérifier les informations affichées | - Informations correctes<br>- Correspondance avec les données saisies           | ⬜      |
| PROF-04  | Ajout d'une photo de profil  | 1. Accéder à la page de profil<br>2. Cliquer sur "Ajouter une photo"<br>3. Sélectionner une image<br>4. Soumettre | - Photo de profil mise à jour<br>- Affichage de la nouvelle photo               | ⬜      |
| PROF-05  | Suppression de la photo de profil | 1. Accéder à la page de profil<br>2. Cliquer sur "Supprimer la photo"<br>3. Confirmer la suppression | - Photo de profil supprimée<br>- Affichage de la photo par défaut               | ⬜      |




### 📝 2. Tracker d'Émotions

#### 2.1 Enregistrement d'Émotion
| ID | Description | Étapes | Résultat Attendu | Statut |
|----|-------------|--------|------------------|---------|
| TRACK-01 | Ajout émotion basique | 1. Sélectionner émotion<br>2. Définir intensité<br>3. Enregistrer | Émotion sauvegardée | ⬜ |
| TRACK-02 | Ajout avec commentaire | 1. Sélectionner émotion<br>2. Ajouter commentaire<br>3. Enregistrer | Émotion + commentaire sauvegardés | ⬜ |
| TRACK-03 | Validation intensité | 1. Saisir intensité > 5 | Message d'erreur | ⬜ |

#### 2.2 Historique
| ID | Description | Étapes | Résultat Attendu | Statut |
|----|-------------|--------|------------------|---------|
| TRACK-04 | Affichage historique | 1. Accéder à l'historique | Liste émotions triée par date | ⬜ |
| TRACK-05 | Filtrage par période | 1. Sélectionner période<br>2. Appliquer filtre | Émotions de la période | ⬜ |
| TRACK-06 | Suppression émotion | 1. Sélectionner émotion<br>2. Supprimer | Émotion retirée de l'historique | ⬜ |

### 📊 3. Dashboard

#### 3.1 Statistiques
| ID | Description | Étapes | Résultat Attendu | Statut |
|----|-------------|--------|------------------|---------|
| DASH-01 | Chargement stats | 1. Accéder au dashboard | Affichage graphiques et stats | ⬜ |
| DASH-02 | Filtres temporels | 1. Changer période<br>2. Appliquer | Stats mises à jour | ⬜ |
| DASH-03 | Export données | 1. Cliquer export<br>2. Choisir format | Fichier téléchargé | ⬜ |

### 🧘‍♂️ 4. Exercices de Respiration

#### 4.1 Sessions
| ID | Description | Étapes | Résultat Attendu | Statut |
|----|-------------|--------|------------------|---------|
| BREATH-01 | Démarrer exercice | 1. Sélectionner exercice<br>2. Lancer | Animation + minuteur démarrent | ⬜ |
| BREATH-02 | Pause exercice | 1. Exercice en cours<br>2. Cliquer pause | Session en pause | ⬜ |
| BREATH-03 | Terminer session | 1. Compléter exercice | Stats session enregistrées | ⬜ |

## 🚀 Tests de Performance

### 1. Temps de Chargement
| ID | Description | Critère de Succès | Statut |
|----|-------------|-------------------|---------|
| PERF-01 | Chargement initial | < 3 secondes | ⬜ |
| PERF-02 | Navigation pages | < 1 seconde | ⬜ |
| PERF-03 | Chargement graphiques | < 2 secondes | ⬜ |

### 2. Réactivité
| ID | Description | Critère de Succès | Statut |
|----|-------------|-------------------|---------|
| PERF-04 | Input utilisateur | < 100ms | ⬜ |
| PERF-05 | Animations | 60 FPS | ⬜ |
| PERF-06 | Scroll historique | Fluide sans lag | ⬜ |

## 🔒 Tests de Sécurité

### 1. Protection des Données
| ID | Description | Critère de Succès | Statut |
|----|-------------|-------------------|---------|
| SEC-01 | Token JWT | Expiration correcte | ⬜ |
| SEC-02 | Données sensibles | Chiffrement en transit | ⬜ |
| SEC-03 | Injection SQL | Requêtes sécurisées | ⬜ |

### 2. Authentification
| ID | Description | Critère de Succès | Statut |
|----|-------------|-------------------|---------|
| SEC-04 | Brute Force | Blocage après 5 tentatives | ⬜ |
| SEC-05 | Session timeout | Déconnexion après 30min | ⬜ |
| SEC-06 | CSRF | Tokens validés | ⬜ |

## 💻 Tests d'Interface

### 1. Responsive Design
| ID | Description | Critère de Succès | Statut |
|----|-------------|-------------------|---------|
| UI-01 | Mobile (320px) | Layout adapté | ⬜ |
| UI-02 | Tablet (768px) | Layout adapté | ⬜ |
| UI-03 | Desktop (1024px+) | Layout adapté | ⬜ |

### 2. Accessibilité
| ID | Description | Critère de Succès | Statut |
|----|-------------|-------------------|---------|
| UI-04 | Navigation clavier | Tous éléments accessibles | ⬜ |
| UI-05 | Lecteur d'écran | Contenu bien décrit | ⬜ |
| UI-06 | Contraste | WCAG AA minimum | ⬜ |

## 🌐 Tests de Compatibilité

### 1. Navigateurs
| ID | Description | Critère de Succès | Statut |
|----|-------------|-------------------|---------|
| COMP-01 | Chrome | Fonctionnel | ⬜ |
| COMP-02 | Firefox | Fonctionnel | ⬜ |
| COMP-03 | Safari | Fonctionnel | ⬜ |
| COMP-04 | Edge | Fonctionnel | ⬜ |

### 2. Systèmes
| ID | Description | Critère de Succès | Statut |
|----|-------------|-------------------|---------|
| COMP-05 | iOS | PWA fonctionnelle | ⬜ |
| COMP-06 | Android | PWA fonctionnelle | ⬜ |
| COMP-07 | Windows | Application responsive | ⬜ |
| COMP-08 | MacOS | Application responsive | ⬜ |

## 📝 Instructions d'Exécution

### 🔄 Cycle de Test
1. Exécuter les tests dans l'ordre spécifié
2. Marquer chaque test : ✅ (Succès), ❌ (Échec), ⏳ (En cours)
3. Documenter les bugs dans le système de suivi
4. Retester après corrections

### 🐛 Rapport de Bug
Format à utiliser :
```
ID Test : XXX-XX
Environnement : [OS/Navigateur/Version]
Description : [Description détaillée]
Étapes de reproduction : [Liste étapes]
Résultat actuel : [Description]
Résultat attendu : [Description]
Capture d'écran : [Si applicable]
```

### 📊 Métriques de Qualité
- Taux de succès des tests
- Temps moyen de correction
- Nombre de bugs critiques
- Performance moyenne
- Score d'accessibilité 
