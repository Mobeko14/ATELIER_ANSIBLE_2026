------------------------------------------------------------------------------------------------------
ATELIER ANSIBLE
------------------------------------------------------------------------------------------------------
L’idée en 30 secondes : Dans cet atelier, vous allez apprendre à **automatiser le déploiement d’un serveur web avec Ansible**, directement depuis GitHub **Codespaces**, sans infrastructure complexe. L’objectif est de comprendre comment **décrire un état cible** (installer, configurer, déployer) et laisser l’outil l’appliquer automatiquement, de manière reproductible et idempotente. On passe ainsi d’une logique manuelle à une logique DevOps industrialisée.
  
**Architecture cible :** Ci-dessous, voici l'architecture cible souhaitée.   
  
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/8064eb95-da73-4bdd-9ef2-a7cebbbd71c8" />
  
-------------------------------------------------------------------------------------------------------
Séquence 1 : Codespace de Github
-------------------------------------------------------------------------------------------------------
Objectif : Création d'un Codespace Github  
Difficulté : Très facile (~5 minutes)
-------------------------------------------------------------------------------------------------------
**Faites un Fork de ce projet**. Si besoin, voici une vidéo d'accompagnement pour vous aider à "Forker" un Repository Github : [Forker ce projet](https://youtu.be/p33-7XQ29zQ) 
  
Ensuite depuis l'onglet **[CODE]** de votre nouveau Repository, **ouvrez un Codespace Github**.
  
---------------------------------------------------
Séquence 2 : Création du votre environnement de travail
---------------------------------------------------
Objectif : Créer votre environnement de travail  
Difficulté : Simple (~10 minutes)
---------------------------------------------------
Vous allez dans cette séquence mettre en place votre environnement et les logiciels Ansible. Depuis le terminal de votre Codespace copier/coller les codes ci-dessous étape par étape :  

**Installation de Ansible et Nginx**  
```
sudo apt update
sudo apt install -y ansible curl
```
**Vérifier l’environnement**  
```
ansible --version
curl --version
```
**Tester la cible locale**  
```
ansible -i inventory.ini local -m ping
```
**Exécuter le playbook**  
```
ansible-playbook -i inventory.ini playbook.yml
```
**Vérifier le résultat**  
```
curl http://localhost
```  
---------------------------------------------------  
**Réccupération de l'URL de votre serveur Nginx**. Votre serveur Nginx (et sa page Web) est déployé dans Codespace. Pour obtenir votre URL cliquez sur l'onglet **[PORTS]** dans votre Codespace (à coté de Terminal), ouvrez le port 80 et rendez public votre port (Visibilité du port). Ouvrez l'URL dans votre navigateur et c'est terminé.  
  
---------------------------------------------------
Séquence 3 : Exercices  
Difficulté : Facile (~30 minutes)
---------------------------------------------------
### Exercice 1 : Customisation de la page d'accueil 
Customisez la page d'accueil de votre site Web en ajoutant la ligne suivante dans votre fichier index.html  
```
<h1>Déploiement réalisé par [Votre Nom]</h1>
```

### Exercice 2 : Paramétrer dynamiquement votre serveur avec Ansible 
Voici le contenu (contenu imposé) de votre nouveau fichier index.html    
```
<!DOCTYPE html>
<html>
<head>
  <title>{{ page_title }}</title>
</head>
<body>
  <h1>{{ page_title }}</h1>
  <p>Déployé par : {{ author }}</p>
  <p>Utilisateur système : {{ app_user }}</p>
</body>
</html>
```
Modifier votre playbook afin de :  
* Créer un title contenant le texte suivant : "Serveur déployé avec Ansible"
* L'auteur sera : "Votre nom"
* L'utilisateur sera un **utilisateur Linux** : "Votre prénom"
  
---------------------------------------------------
Séquence 4 : Questions  
Difficulté : Moyenne (~45 minutes)
---------------------------------------------------
**Complétez et documentez ce fichier README.md** pour répondre aux questions des exercices.  
Faites preuve de pédagogie et soyez clair dans vos explications et procedures de travail.  

**Question 1 :**  
Pourquoi Ansible est-il qualifié d’outil "déclaratif" ?    
  
*..Répondez à cet exercice ici..*

**Question 2 :**  
Pourquoi l’utilisation de variables est-elle essentielle dans un playbook ?  
  
*..Répondez à cet exercice ici..*

**Question 3 :**  
En quoi Ansible facilite-t-il la gestion de plusieurs serveurs ?  
  
*..Répondez à cet exercice ici..*

**Question 4 :**  
Quels sont les avantages et les limites d’Ansible dans un contexte DevOps ?   
  
*..Répondez à cet exercice ici..*
  
**Question 5 :**  
Quelle est la différence entre les modules copy et template dans Ansible ?   
  
*..Répondez à cet exercice ici..*

---------------------------------------------------
Séquence 5 : Atelier  
Difficulté : Moyenne (~1 heure)
---------------------------------------------------
### Structurer votre déploiement Ansible afin de pouvoir choisir entre un rôle DEV ou un rôle PROD  
Modifier votre fichier playbook.yml afin de pouvoir choisir entre un rôle DEV ou un rôle PROD.  

**Resultats attendus**  
* Déploiement en DEV  
```
ansible-playbook -i inventory.ini playbook.yml --limit dev
```
```
app_name: "Application DEV"
env: "dev"
author: "Etudiant DEV"
```
* Déploiement en PROD
```
ansible-playbook -i inventory.ini playbook.yml --limit prod
```
```
app_name: "Application PROD"
env: "prod"
author: "Equipe Ops""
```
---------------------------------------------------
### Zoom sur votre environnement Codepace 
Codepace est un outil proposer par GitHub soumit à quota (4$/mois). Si vous dépasser votre quota mensuel vous ne serez plus en mesure de pouvoir utiliser Codespace. C'est pourquoi à **la fin de votre atelier, pensez à suprimer votre Codespace après avoir mis à jour votre GitHub**.  

### Vous pouvez voir l'état de vos Codespace ici : https://github.com/codespaces  
  
---------------------------------------------------
Evaluation
---------------------------------------------------
Cet atelier ANSIBLE, **noté sur 20 points**, est évalué sur la base du barème suivant :  
- Mise en oeuvre (2 points)
- Exercice N°1 - Customisation de la page d'accueil (2 points)
- Exercice N°2 - Paramétrer dynamiquement votre serveur avec Ansible (2 points)
- Questions + Qualité du Readme (lisibilité, erreur, ...) (5 points)
- Atelier - Rôles DEV et PROD (6 points)
- Processus travail (quantité de commits, cohérence globale, interventions externes, ...) (3 points) 


## Question 1 : Pourquoi Ansible est-il qualifié d’outil "déclaratif" ?

Ansible est qualifié d’outil déclaratif car on ne décrit pas les étapes techniques une par une, mais **l’état final souhaité du système**.

Par exemple, au lieu d’écrire toutes les commandes pour installer et démarrer un serveur web, on déclare simplement que :

* le paquet nginx doit être installé
* le service doit être démarré

Ansible se charge ensuite de déterminer les actions nécessaires pour atteindre cet état.

De plus, Ansible est **idempotent**, ce qui signifie que si l’état souhaité est déjà atteint, aucune modification ne sera appliquée. Cela garantit des déploiements fiables et reproductibles.


## Question 2 : Pourquoi l’utilisation de variables est-elle essentielle dans un playbook ?

Les variables permettent de rendre les playbooks **flexibles, réutilisables et dynamiques**.

Elles évitent de coder des valeurs en dur (hardcoding) et permettent de :

* personnaliser les déploiements (ex : nom, utilisateur, port)
* adapter le même playbook à différents environnements (dev, test, production)
* centraliser les configurations

Par exemple, au lieu d’écrire directement un titre HTML, on utilise :
{{ page_title }}

Ainsi, le contenu peut être modifié sans changer la structure du playbook, ce qui facilite la maintenance et l’évolution.


## Question 3 : En quoi Ansible facilite-t-il la gestion de plusieurs serveurs ?

Ansible permet de gérer plusieurs serveurs simultanément grâce à son fichier d’inventaire.

Dans cet inventaire, on peut :

* définir plusieurs machines
* les organiser en groupes (web, database, etc.)

Un seul playbook peut ensuite être exécuté sur :

* un serveur
* un groupe de serveurs
* ou toute l’infrastructure

Ansible utilise SSH pour se connecter aux machines, sans agent à installer, ce qui simplifie fortement le déploiement.

Cela permet d’assurer :

* une configuration uniforme
* un gain de temps important
* une réduction des erreurs humaines


## Question 4 : Quels sont les avantages et les limites d’Ansible dans un contexte DevOps ?

### Avantages :

* Simplicité d’utilisation (syntaxe YAML lisible)
* Pas d’agent à installer (fonctionne via SSH)
* Idempotence (exécutions sûres et répétables)
* Automatisation rapide des tâches
* Intégration facile dans des pipelines DevOps

### Limites :

* Moins performant pour de très grandes infrastructures
* Exécution séquentielle (peut être plus lent que d’autres outils)
* Gestion d’état moins avancée que certains outils comme Terraform
* Débogage parfois complexe sur des playbooks volumineux

Ansible reste cependant un excellent outil pour la configuration et l’automatisation dans un environnement DevOps.


## Question 5 : Quelle est la différence entre les modules copy et template dans Ansible ?

Le module **copy** permet de copier un fichier tel quel depuis la machine de contrôle vers la machine cible.

Exemple :

* copier un fichier HTML statique
* aucun traitement du contenu

Le module **template**, quant à lui, utilise le moteur Jinja2 pour générer un fichier dynamique.

Il permet d’intégrer des variables dans le fichier grâce à la syntaxe :
{{ variable }}

Ainsi :

* copy → contenu fixe
* template → contenu dynamique et personnalisable

Le module template est donc essentiel pour créer des configurations adaptables selon le contexte (utilisateur, environnement, etc.).


