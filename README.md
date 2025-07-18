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
git clone https://github.com/mmouhib/pi.git
cd pi
rm -rf .git
git init
git remote add origin https://github.com/votre-username/votre-repo.git
git add .
git commit -m "Initial commit"
git branch -M main
git push -u origin main


## 2️⃣ Lancer le projet

docker compose up jenkins sonarqube nexus grafana prometheus -d

## 3️⃣ Nexus Configuration

Récupérer le mot de passe initial :

docker exec -it nexus bash
cat /nexus-data/admin.password
Accéder à http://localhost:8081 et remplacer le mot de passe initial par admin.

## 4️⃣ Jenkins Configuration
Accéder à http://localhost:8080

Ajouter ces Credentials :

Docker Hub : ID = nexus-docker-credentials

SonarQube : ID = sonar-credentials

Configurer :

JDK 8

Maven (version recommandée : 3.9.x)

## 5️⃣ Docker Compose Backend App
Dans docker-compose.yml, remplacez toutes les occurrences de mmouhib par votre nom d'utilisateur Docker Hub.

## 6️⃣ SonarQube Configuration
Accéder à http://localhost:9000

Changer le mot de passe admin → mot de passe sécurisé

Créer un token via My Account → Security

Ajouter ce token dans le pom.xml sous sonar.login

##  7️⃣ Créer un Pipeline Jenkins
Jenkins → Nouveau Item → Pipeline

Source : votre GitHub

Utiliser le Jenkinsfile de votre repo

Lancer un build (Build Now)

## 8️⃣ Grafana Dashboards
Après avoir lancé le pipeline :

Accéder à Grafana : http://localhost:3000

Login : admin / admin@123

Importer les dashboards suivants dans Grafana :

yaml
Copy
Edit
9964
4701
11378
16459
1860
8321
17642



💡 Il est prêt à être collé dans ton README.md. Si tu veux je peux aussi générer le badge final avec ton Docker Hub ou GitHub username.
