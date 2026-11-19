# 🛡️ NetGuard – Network Intrusion Detection System (NIDS)

**NetGuard** est une plateforme de surveillance et de détection d'intrusions réseau (NIDS) développée avec **C# et ASP.NET Core 10**. Son objectif est d'analyser le trafic réseau à partir de captures réalisées avec Wireshark, d'identifier des comportements potentiellement suspects et de centraliser les événements de sécurité dans une interface de supervision.

Le projet s'inscrit dans le domaine de la cybersécurité défensive (Blue Team) et vise à proposer un outil permettant de faciliter l'analyse du trafic réseau, la détection d'anomalies et la gestion des alertes de sécurité.

---

## 🎯 Objectifs du projet

Les principaux objectifs de NetGuard sont :

- Capturer le trafic réseau à l'aide de Wireshark.
- Importer et analyser des fichiers de capture PCAP et PCAPNG.
- Extraire les informations pertinentes des paquets réseau.
- Identifier les communications et comportements suspects.
- Détecter certaines activités potentiellement malveillantes.
- Générer des alertes de sécurité automatiquement.
- Centraliser les événements réseau dans une base de données.
- Fournir un tableau de bord pour superviser l'activité réseau.
- Conserver un historique des événements et des incidents.

---

## 🏗️ Architecture du projet

NetGuard repose sur une architecture modulaire séparant la collecte des données, leur analyse, leur stockage et leur visualisation.

```text
                 NETWORK TRAFFIC
                        |
                        v
               WIRESHARK / NPCAP
                        |
                        v
                PCAP / PCAPNG FILES
                        |
                        v
              NETGUARD COLLECTOR
                    (C#)
                        |
                        v
               PACKET PROCESSING
                SharpPcap
                PacketDotNet
                        |
                        v
               DETECTION ENGINE
                        |
              +---------+---------+
              |                   |
              v                   v
         NETWORK EVENTS       SECURITY ALERTS
              |                   |
              +---------+---------+
                        |
                        v
                ASP.NET CORE API
                        |
                        v
                 ENTITY FRAMEWORK
                        |
                        v
                  SQL SERVER
                        |
                        v
                REACT DASHBOARD
```

### Description des composants

| Composant | Responsabilité |
|---|---|
| Wireshark | Capture du trafic réseau |
| Npcap | Accès aux interfaces réseau sous Windows |
| NetGuard Collector | Importation et collecte des paquets |
| SharpPcap | Accès aux captures réseau en C# |
| PacketDotNet | Décodage et analyse des protocoles |
| Detection Engine | Identification des comportements suspects |
| ASP.NET Core Web API | Gestion des fonctionnalités et des API |
| Entity Framework Core | Communication avec SQL Server |
| SQL Server | Stockage des données |
| React | Interface de supervision |

---

## 🛠️ Technologies utilisées

### Backend

- **C# 14** : langage principal du projet.
- **.NET 10** : plateforme de développement.
- **ASP.NET Core Web API** : développement des API REST.
- **Entity Framework Core 10** : mapping objet-relationnel et gestion des migrations.
- **LINQ** : interrogation et analyse des données.
- **BackgroundService** : exécution des tâches de collecte en arrière-plan.

### Analyse réseau

- **Wireshark** : capture et inspection du trafic réseau.
- **Npcap** : capture des paquets sous Windows.
- **SharpPcap** : bibliothèque de capture et de lecture réseau en C#.
- **PacketDotNet** : décodage des protocoles réseau.
- **PCAP / PCAPNG** : formats de fichiers de capture.

### Base de données

- **Microsoft SQL Server 2025 Express**
- **SQL Server Management Studio (SSMS)**

### Frontend

- **React** : interface utilisateur.
- **Chart.js** : visualisation des statistiques et des événements.

### Outils de développement

- Visual Studio 2026
- Swagger / OpenAPI
- Postman
- Git et GitHub

---

## 🔍 Fonctionnalités prévues

### 1. Network Traffic Analysis

Analyse des captures réseau pour extraire :

- Adresse IP source.
- Adresse IP destination.
- Port source et destination.
- Protocole réseau.
- Horodatage.
- Taille des paquets.
- Informations sur les communications.

### 2. Intrusion Detection Engine

Mise en place d'un moteur de détection basé sur des règles permettant notamment d'identifier :

- Les tentatives répétées de connexion.
- Les comportements compatibles avec un scan de ports.
- Les volumes de trafic inhabituels.
- Les communications avec des adresses IP signalées comme suspectes.
- Les connexions répétées vers des ports inhabituels.
- Certaines anomalies dans les communications réseau.

Les détections seront fondées sur des indicateurs observables et ne constitueront pas, à elles seules, une preuve d'intrusion.

### 3. Security Alerts Management

Gestion des alertes générées :

- Niveau de criticité : Critical, High, Medium, Low.
- Description de l'événement.
- Adresse IP concernée.
- Date et heure de détection.
- Type de détection.
- Statut de l'alerte.
- Historique des alertes.

### 4. Network Monitoring Dashboard

Le tableau de bord permettra de visualiser :

- Nombre total de paquets analysés.
- Nombre d'événements réseau.
- Nombre d'alertes générées.
- Répartition des protocoles.
- Adresses IP les plus actives.
- Évolution du trafic réseau.
- Dernières activités suspectes.

### 5. Incident Management

Gestion des incidents de sécurité :

- Création d'incidents à partir des alertes.
- Classification par criticité.
- Affectation aux analystes.
- Suivi du traitement.
- Historique des interventions.

### 6. Authentication and Authorization

Sécurisation de la plateforme :

- Authentification JWT.
- Gestion des utilisateurs.
- Gestion des rôles.
- Autorisations par fonctionnalité.
- Journalisation des actions.

---

## 🗄️ Modèle de données

La base de données NetGuard sera organisée autour des principales entités suivantes :

| Entité | Description |
|---|---|
| User | Comptes des utilisateurs |
| NetworkDevice | Équipements réseau surveillés |
| NetworkEvent | Événements réseau analysés |
| DetectionRule | Règles de détection |
| Alert | Alertes de sécurité |
| Incident | Incidents identifiés |
| AuditLog | Historique des actions |

### Relations principales

- Un NetworkDevice peut être associé à plusieurs NetworkEvents.
- Un NetworkEvent peut générer plusieurs Alertes.
- Une DetectionRule peut déclencher plusieurs Alertes.
- Un User peut être responsable de plusieurs Incidents.
- Un User peut effectuer plusieurs actions enregistrées dans AuditLog.

---

## 📁 Structure du projet

```text
NetGuard/
│
├── NetGuard.sln
│
├── NetGuard.API/
│   ├── Controllers/
│   ├── Middleware/
│   ├── Extensions/
│   ├── Program.cs
│   └── appsettings.json
│
├── NetGuard.Core/
│   ├── Entities/
│   ├── DTOs/
│   ├── Enums/
│   ├── Interfaces/
│   └── Services/
│
├── NetGuard.Infrastructure/
│   ├── Data/
│   ├── Configurations/
│   ├── Repositories/
│   └── Services/
│
├── NetGuard.Collector/
│   ├── Collectors/
│   ├── PacketProcessing/
│   ├── Models/
│   └── Program.cs
│
└── README.md
```

---

## ⚙️ Installation et configuration

### Prérequis

Avant de commencer, les outils suivants doivent être installés :

- Visual Studio 2026.
- .NET SDK 10.
- SQL Server 2025 Express.
- SQL Server Management Studio.
- Wireshark.
- Npcap.
- Git.

### Vérifier l'installation de .NET

```powershell
dotnet --version
dotnet --list-sdks
dotnet --list-runtimes
```

### Cloner le projet

```bash
git clone https://github.com/USERNAME/NetGuard.git

cd NetGuard
```

### Restaurer les dépendances

```bash
dotnet restore
```

### Compiler la solution

```bash
dotnet build
```

### Configuration de SQL Server

La chaîne de connexion sera définie dans le fichier `appsettings.json`.

Exemple :

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=localhost\\SQLEXPRESS;Database=NetGuardDB;Trusted_Connection=True;TrustServerCertificate=True;"
  }
}
```

**Remarque :** adapter le nom du serveur à l'instance SQL Server réellement installée.

### Entity Framework Core

Après configuration du DbContext et installation des packages nécessaires :

```powershell
Add-Migration InitialCreate
Update-Database
```

Ces commandes permettent de générer et d'appliquer la première migration de la base de données.

---

## 📊 Exemple de fonctionnement

1. L'utilisateur effectue une capture réseau avec Wireshark.
2. La capture est enregistrée au format PCAP ou PCAPNG.
3. NetGuard importe le fichier.
4. Le collecteur C# extrait les informations des paquets.
5. Le moteur de détection analyse les événements.
6. Les comportements suspects déclenchent des alertes.
7. Les événements et alertes sont enregistrés dans SQL Server.
8. Le dashboard présente les résultats à l'utilisateur.

---

## 🔐 Sécurité et environnement de test

NetGuard est conçu pour être utilisé dans un environnement autorisé.

Les captures réseau peuvent contenir des informations sensibles. Leur collecte, leur stockage et leur analyse doivent respecter les règles de confidentialité et les autorisations applicables.

Les tests de détection seront réalisés sur des captures contrôlées et des environnements de laboratoire.

---

## 🚀 Roadmap

- [ ] Création de la solution .NET.
- [ ] Mise en place de l'architecture backend.
- [ ] Modélisation des entités.
- [ ] Configuration SQL Server.
- [ ] Première migration Entity Framework Core.
- [ ] Développement des API REST.
- [ ] Authentification JWT.
- [ ] Intégration de SharpPcap.
- [ ] Intégration de PacketDotNet.
- [ ] Importation des fichiers PCAP / PCAPNG.
- [ ] Développement du moteur de détection.
- [ ] Gestion des alertes.
- [ ] Gestion des incidents.
- [ ] Développement du dashboard React.
- [ ] Tests et validation du système.

---

## 🎓 Domaine du projet

**Cybersécurité – Blue Team – Network Security – Intrusion Detection – Network Traffic Analysis**

NetGuard est un projet visant à mettre en pratique les concepts de surveillance réseau, d'analyse de trafic, de détection d'anomalies et de développement d'applications sécurisées avec l'écosystème .NET.

---

**Project:** NetGuard  
**Type:** Network Intrusion Detection System (NIDS)  
**Backend:** ASP.NET Core 10  
**Language:** C# 14  
**Database:** Microsoft SQL Server 2025  
**Status:** In Development
