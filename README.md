# Projet Jenkins CI/CD avec Application Web

## Description du projet
Ce projet illustre la mise en place d’un **pipeline CI/CD** avec **Jenkins**, pour construire, tester, publier et déployer automatiquement une **application web front-end** réalisée en **HTML/CSS**. L’objectif est d’automatiser le cycle de vie de l’application depuis le push sur GitHub jusqu’au déploiement sur un serveur distant (AWS).

---

## Structure du projet
- `Jenkinsfile` : Pipeline Jenkins déclaratif pour CI/CD.
- `dockerfile` : Définition de l’image Docker pour le déploiement.
- `index.html` et fichiers HTML/CSS associés : Interface front-end de l’application.
- `css/` : Contient les fichiers CSS pour le style.
- `imgs/` : Images utilisées dans l’application.
- `README.md` : Documentation du projet.

---

## Pipeline Jenkins
Le pipeline comprend plusieurs étapes :

1. **Checkout** : Récupération du code depuis le dépôt GitHub (`main` branch).
2. **Build Docker Image** : Construction d’une image Docker à partir du `dockerfile`.
3. **Test** : Vérification basique des fichiers HTML, CSS et JS.
4. **Push to Docker Hub** :  
   - Connexion à Docker Hub avec les credentials Jenkins.  
   - Tag unique de l’image (`BUILD_NUMBER`) et tag `latest`.  
   - Push de l’image sur Docker Hub.
5. **Deploy to AWS (Staging)** :  
   - Connexion au serveur distant AWS via SSH.  
   - Arrêt et suppression du container existant.  
   - Déploiement du nouveau container Docker avec l’image `latest`.

---

## Application Web
L’application front-end est une **interface simple en HTML/CSS**, contenant :  
- Pages pour gérer les étudiants, enseignants et employés.  
- Formulaires d’ajout, modification et consultation des données.  
- Mise en page responsive avec CSS.  

Le site est accessible sur le serveur AWS à l’adresse :  



---

## Technologies utilisées
- **CI/CD** : Jenkins  
- **Versioning** : Git / GitHub  
- **Conteneurisation** : Docker  
- **Front-end** : HTML / CSS  
- **Cloud** : Serveur AWS EC2  

---

## Comment exécuter le projet localement
1. Cloner le dépôt :  
```bash
git clone https://github.com/Abdallah-Abdelnour/jenkins-projet.git
cd jenkins-projet

2. Construire l’image Docker :
docker build -t monsite:local .

3. Lancer le container :
docker run -d -p 8080:80 --name monsite-test monsite:local

