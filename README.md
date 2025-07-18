# 🚀 Project Setup Guide

📌 **Important** : Ne change pas le nom du dossier racine (`pi`).

---

## ✅ Default Credentials

| Tool | Username | Password |
|------|----------|----------|
| Grafana | `admin` | `admin@123` |
| Nexus | `admin` | *see step below* |

---

## ⚙️ Requirements

- Linux (WSL ou machine locale)
- Docker & Docker Compose installés

---

## 1️⃣ Clone et Préparation du Projet

```bash
git clone https://github.com/chyrazz/pi.git
cd pi
rm -rf .git
git init
git remote add origin https://github.com/votre-username/votre-repo.git
git add .
git commit -m "Initial commit"
git branch -M main
git push -u origin main

```

## **2️⃣ Lancer les Conteneurs**

```bash
docker compose up -d jenkins sonarqube nexus grafana prometheus

```

## **3️⃣ Configuration de Nexus**

- Récupérer le mot de passe initial :

```bash
docker exec -it nexus bash
cat /nexus-data/admin.password

Aller sur http://localhost:8081

Se connecter avec :

Login : admin

Mot de passe : (celui récupéré ci-dessus)

Modifier le mot de passe admin en admin pour simplifier l’accès (optionnel)

```
## **4️⃣ Configuration de Jenkins**

- Accéder à [http://localhost:8080](http://localhost:8080)
- Ajouter ces Credentials :  
  - Docker Hub : ID = `nexus-docker-credentials`  
  - SonarQube : ID = `sonar-credentials`
- Configurer :  
  - JDK 8  
  - Maven (version recommandée : 3.9.x)


## **5️⃣ Personnaliser Docker Compose pour Backend App**

- Ouvrir `docker-compose.yml`  
- Remplacer toutes les occurrences de `chanzouti2001` par votre nom d'utilisateur Docker Hub


## **6️⃣ Configuration de SonarQube**

- Accéder à [http://localhost:9000](http://localhost:9000)
- Changer le mot de passe `admin` par un mot de passe sécurisé
- Créer un token d’accès :  
  - Aller dans **My Account** → **Security** → **Generate Tokens**
- Ajouter ce token dans le `pom.xml` sous la propriété `sonar.login`


## **7️⃣ Créer un Pipeline Jenkins**

- Dans Jenkins, créer un **Nouveau Item** → **Pipeline**  
- Configurer la source GitHub avec votre repo  
- Utiliser le `Jenkinsfile` présent dans le repo  
- Lancer un build (**Build Now**)



## **8️⃣ Dashboards Grafana**

- Après le premier build, accéder à Grafana : [http://localhost:3000](http://localhost:3000)  
- Connexion :  
  - Login : `admin`  
  - Mot de passe : `admin@123`  
- Importer les dashboards Grafana via leurs IDs (Menu Import > Dashboard IDs) :  

| Dashboard ID | Description (exemple)                |
|--------------|------------------------------------|
| 9964         | Kubernetes cluster monitoring       |
| 4701         | Jenkins build statistics            |
| 11378        | Docker container metrics            |
| 16459        | Prometheus server overview          |
| 1860         | Node Exporter server metrics        |
| 8321         | SonarQube quality gates             |
| 17642        | System CPU and Memory monitoring    |


