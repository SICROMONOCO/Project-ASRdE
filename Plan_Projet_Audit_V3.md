---
Title: [ASRdE (Audit de Sécurité Réseau D'une Entre ) Project Plan]
date: 2026-03-11
---

|                 |                                                   |
| --------------- | ------------------------------------------------- |
| **Titre** | Plan de travail Audit de Sécurité Réseau D'une Enterprise |
| **Auteurs** | MOHAMED AIT BELLA, BILAL SIKI                     |
| **Encadrant** | Pr. Rachid Dakir                                  |
| **Institution** | FACULTÉ POLYDISCIPLINAIRE DE OUARZAZATE           |
| **Matière** | CYBERSÉCURITÉ S4                                  |
| **Date** | 2026                                              |

## 1. Objectif & Problématique

> [!goal] But
Tester la résistance du réseau face aux cyberattaques (Intrusions, Vol de données).

> [!question] Problématique
Comment sécuriser les actifs critiques (Serveurs, Données) sans impacter le travail des employés ?

---

## 2. Périmètre (Le Scope)

| Élément           | Description                                                                                                     |
| ----------------- | --------------------------------------------------------------------------------------------------------------- |
| **Cibles** | Serveur Active Directory (Gestion des accès), Serveur de fichiers, et les équipements réseaux (Firewall/Switch) |
| **Environnement** | Lab virtuel isolé (VMware/VirtualBox) pour simuler une entreprise                                               |

---

## 3. Méthodologie & Outils (Le Cœur Technique)

### Notre Démarche de Pentest (En 4 étapes clés)

| Phase                 | Objectif                               | Outil             |
| --------------------- | -------------------------------------- | ----------------- |
| 1. **Reconnaissance** | Identifier les cibles                  | `Nmap`            |
| 2. **Mapping** | Scanner les vulnérabilités             | `Nessus`          |
| 3. **Exploitation** | Simuler l'attaque                      | `Metasploit`      |
| 4. **Audit Interne** | Tester la robustesse des mots de passe | `John the Ripper` |

---

## 4. Solutions Préconisées (Hardening)

> [!tip] Après notre audit, nous proposons 3 axes de protection :
> 
> - **Réseau** : Segmentation par VLANs (Isoler les départements)
> - **Système** : Mise en place d'une politique de mots de passe forte (GPO) et du MFA
> - **Maintenance** : Gestion rigoureuse des mises à jour (Patch Management)

---

## 5. Conclusion & Livrables
	
> [!success] Résultat
Un rapport technique pour l'IT et une synthèse stratégique pour la direction.

> [!abstract] Bilan
Ce projet m'a permis de maîtriser les outils de Kali Linux et de comprendre l'importance de la défense en profondeur.

---

## 6. Répartition des Tâches (Directives du Professeur)

> [!note] Distribution des rôles pour la V3
> Conformément aux instructions, la distribution du travail pour la prochaine étape sera structurée de la manière suivante :

### Mohamed Ait Bella
- **Recherche Documentaire :** Compétences de l'Auditeur IT et Normes d'Audit d'Entreprise.

### Bilal Siki
- **Présentation (2ème partie) :** Création d'une présentation globale englobant tout ce qui sera fait dans le Lab.
- **Processus & Commandes :** Explication détaillée des méthodologies et des commandes utilisées.
- **Pratique :** Animation de scénarios en direct (Live scenarios).
- **Documentation :** Présentation de la structure formelle du document d'audit basé sur le Lab.

---

> [!quote] Remerciements
Nous vous remercions pour votre temps et votre considération.

**Cordialement,**

*MOHAMED AIT BELLA & BILAL SIKI*