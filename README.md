# API de Gestion des Tâches pour des Superheros !!

## Introduction
Cette API permet aux utilisateurs de 
gérer leurs tâches, 
en s'authentifiant via JWT.
L'API est sécurisée et permet d'ajouter, de récupérer et de filtrer les tâches.
L'API permet aussi de créer des tags, de les attacher à une tâche, et de récupérer tous les tags d'un utilisateur.
Toutes ces fonctionnalités ont été testés, le fichier Postman joint à ce dossier montre le bon fonctionnement de l'API.


## Organisation du Projet
Le projet suit une structure MVC (Model-View-Controller) que j'ai choisis pour avoir une meilleure modularité et maintenabilité.

📁 **`src/`**  
├── 📁 `controllers/` → Gère la logique métier et les réponses aux requêtes  
├── 📁 `services/` → Contient les interactions avec la base de données (Prisma)  
├── 📁 `routes/` → Définit les routes Express  
├── 📁 `middlewares/` → Gère l'authentification et la validation  
└── 📄 `server.js` → Point d'entrée du serveur Express


## Installation & Exécution
### Prérequis
- **Node.js** (v18 ou plus)
- **Docker** (Optionnel)
- **Postman** (pour tester l'API)

### Étapes d'installation
1**Installer les dépendances**
   ```sh
   npm install
   ```
2**Configurer l'environnement**
    - Renomme le fichier `.env.example` en `.env` et ajuste les valeurs
   ```env
   DATABASE_URL="postgresql://postgres:password@localhost:5432/Tasks"
   ```

## 🔥 Exécution de l'API
### 📌 **Avec Node.js** (Sans Docker)
1. **Appliquer les migrations Prisma**
   ```sh
   npx prisma migrate dev --name init
   ```
2. **Démarrer l'API**
   ```sh
   node server.js
   ```
3. **Tester sur Postman** avec `http://localhost:3000`

### 🐳 **Avec Docker (PostgreSQL + API)**
1. **Lancer PostgreSQL et l’API en conteneurs**
   ```sh
   docker build -t api-taches . 
   docker run -p 3000:3000 --env-file .env --name api-taches api-taches    
   ```
2. **Il faut changer l'URL dans le fichier env aussi pour que ça fonctionne**


## Routes de l'API
### Authentification
- `POST /auth/register` → Inscription d'un utilisateur
- `POST /auth/login` → Connexion et récupération d'un JWT

### Tâches (Nécessite JWT)
- `GET /tasks` → Récupérer les tâches de l'utilisateur
- `POST /tasks` → Créer une tâche
- `GET /tasks?priority=1` → Trier les tâches par priorité

### Tags
- `POST /tags` → Ajouter un tag
- `GET /tags` → Récupérer tous les tags
- `POST /assign/Tasks/assign/Taskid/Tagid` → assigner un tag à une tâche

---

## Sécurité & JWT
L'API utilise **JSON Web Tokens (JWT)** pour sécuriser l'accès aux routes.
1. **Connexion (`/auth/login`)** → Retourne un token
2. **Ajout du token dans les requêtes**
   ```sh
   Authorization: Bearer {TON_TOKEN_JWT}
   ```

---

##  Choix de Conception
### 1️⃣ **Prisma pour la base de données**
Utilisation de **Prisma ORM** pour gérer PostgreSQL efficacement, avec des migrations et des requêtes optimisées.

### 2️⃣ **Architecture MVC**
- **Séparation des responsabilités** → Facilité de maintenance et évolutivité.
- **`services/`** pour la logique métier et l’accès aux données.
- **`controllers/`** pour la gestion des réponses API.

### 3️⃣ **Docker pour l’environnement**
L’API et la base de données **PostgreSQL** sont conteneurisées avec un **Docker**, ce qui facilite le déploiement et la gestion des services.

### Swagger pour la documentation
L’API est documentée avec **OpenAPI 3.0**, accessible via Swagger Editor.


## Auteurs
👨‍💻 **Développeur_étudiant** : BAIRI Fadi  
📧 **Contact** : fadibairi3@gmail.com

**Merci d’utiliser cette API !**

