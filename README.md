# Laboratoire SOC — Supervision de sécurité avec Wazuh

![Statut du projet](https://img.shields.io/badge/statut-en%20cours-orange)
![Domaine](https://img.shields.io/badge/domaine-SOC%20%7C%20Blue%20Team-blue)
![Plateforme](https://img.shields.io/badge/plateforme-Linux-lightgrey)

## 1. Présentation du projet

Ce projet consiste à construire un laboratoire personnel de cybersécurité afin de comprendre le fonctionnement d'un centre opérationnel de sécurité (SOC), à l'aide de Wazuh, une plateforme open source de supervision de la sécurité.

L'objectif est d'apprendre à collecter des journaux système, surveiller les événements de sécurité, détecter des activités suspectes, analyser des alertes et documenter des incidents dans un environnement contrôlé.

Ce laboratoire permettra de développer des compétences pratiques en cybersécurité défensive, notamment en analyse de journaux, détection d'événements, investigation et réponse à incident.

**État du projet :** en cours de réalisation. Les configurations, les tests et les résultats seront documentés au fur et à mesure de l'avancement.

## 2. Objectifs

- Installer et comprendre l'architecture de Wazuh.
- Connecter un poste Linux à la plateforme de supervision.
- Collecter et analyser des journaux de sécurité.
- Étudier les échecs d'authentification répétés.
- Tester et valider des mécanismes de détection.
- Identifier les faux positifs et les limites des règles.
- Analyser des alertes et reconstituer une chronologie d'événements.
- Rédiger un rapport d'incident structuré.
- Documenter les choix techniques et rendre les manipulations reproductibles.

## 3. Technologies et langages

| Technologie ou langage | Utilisation |
|---|---|
| Wazuh | Supervision de la sécurité, analyse des journaux et alertes |
| Linux / Ubuntu | Système d'exploitation du laboratoire |
| Bash | Commandes Linux et automatisation de tâches |
| YAML | Fichiers de configuration lorsque nécessaire |
| Markdown | Documentation et rapports |
| JSON | Événements de test structurés |
| Python | Automatisation et analyse complémentaire, si nécessaire |
| Git / GitHub | Gestion des versions et publication du projet |

Les technologies supplémentaires seront ajoutées uniquement lorsqu'elles apporteront une réelle valeur au projet.

## 4. Architecture prévue

Le laboratoire reposera initialement sur un serveur Wazuh et un poste Linux surveillé.

```text
+----------------------------+
| Poste Linux surveillé      |
|                            |
| Journaux système           |
| Journaux d'authentification|
+-------------+--------------+
              |
              | Collecte des journaux
              v
+----------------------------+
| Agent Wazuh                |
|                            |
| Surveillance des journaux  |
+-------------+--------------+
              |
              | Communication sécurisée
              v
+----------------------------+
| Serveur Wazuh              |
|                            |
| Analyse et alertes         |
+-------------+--------------+
              |
              v
+----------------------------+
| Tableau de bord Wazuh      |
|                            |
| Recherche et investigation |
+----------------------------+
```

Il s'agit de l'architecture logique prévue. La configuration réelle, les flux réseau et les paramètres de communication seront documentés après l'installation.

## 5. Environnement du laboratoire

L'environnement initial comprendra :

- Un ordinateur sous Windows ou Linux.
- Une machine virtuelle Linux pour réaliser les tests.
- Un serveur Wazuh et son tableau de bord.
- Un agent Wazuh installé sur le poste surveillé.
- Un environnement de test isolé lorsque cela est nécessaire.

Les ressources matérielles requises, les versions compatibles et les paramètres d'installation seront vérifiés à partir de la documentation officielle de Wazuh avant le déploiement.

## 6. Plan de réalisation

### Phase 1 — Préparation et installation

- [ ] Étudier l'architecture générale de Wazuh.
- [ ] Vérifier les ressources disponibles sur l'ordinateur.
- [ ] Préparer la machine virtuelle Linux.
- [ ] Installer Wazuh en suivant la documentation officielle.
- [ ] Vérifier l'accès au tableau de bord.
- [ ] Documenter les commandes et les étapes d'installation.

### Phase 2 — Surveillance d'un poste Linux

- [ ] Installer et enregistrer l'agent Wazuh.
- [ ] Vérifier la communication entre l'agent et le serveur.
- [ ] Identifier les journaux d'authentification collectés.
- [ ] Consulter les événements dans le tableau de bord.
- [ ] Documenter le cheminement des journaux.

### Phase 3 — Détection des échecs d'authentification

- [ ] Observer le fonctionnement normal des authentifications.
- [ ] Générer des échecs de connexion contrôlés dans le laboratoire.
- [ ] Identifier les événements correspondants dans les journaux.
- [ ] Vérifier si une règle de détection génère une alerte.
- [ ] Relever l'identifiant de la règle, la gravité et les informations utiles.
- [ ] Évaluer la pertinence de l'alerte.

### Phase 4 — Validation des détections

- [ ] Définir des scénarios de test et les résultats attendus.
- [ ] Comparer les activités normales et suspectes.
- [ ] Vérifier si les alertes attendues sont générées.
- [ ] Analyser les alertes manquantes ou inattendues.
- [ ] Documenter les faux positifs et les limites de détection.
- [ ] Proposer des améliorations lorsque les tests les justifient.

### Phase 5 — Investigation d'un incident

- [ ] Choisir un scénario de sécurité réalisé en laboratoire.
- [ ] Reconstituer la chronologie des événements.
- [ ] Identifier les comptes et les systèmes concernés.
- [ ] Distinguer les faits confirmés des hypothèses.
- [ ] Évaluer les conséquences potentielles.
- [ ] Proposer des mesures de confinement et de correction.
- [ ] Rédiger un rapport d'incident.

### Phase 6 — Documentation et amélioration

- [ ] Finaliser la documentation de l'architecture.
- [ ] Ajouter des captures d'écran expurgées des données sensibles.
- [ ] Documenter les procédures permettant de reproduire les tests.
- [ ] Expliquer les choix techniques.
- [ ] Présenter les limites connues.
- [ ] Définir les prochaines améliorations.

## 7. Scénario de détection : échecs d'authentification répétés

### Objectif

Étudier des tentatives répétées de connexion échouées sur un poste Linux surveillé.

### Scénario

Un compte utilisateur reçoit plusieurs échecs d'authentification sur une courte période.

Cette activité peut être liée à une erreur de saisie, à un service mal configuré ou à une tentative suspecte d'accès au système.

Des échecs répétés ne suffisent pas, à eux seuls, à prouver qu'une attaque a eu lieu.

### Méthode d'investigation

1. Identifier les événements d'authentification pertinents.
2. Examiner les horodatages, les comptes concernés, les sources disponibles et les résultats des tentatives.
3. Rechercher les alertes Wazuh associées.
4. Étudier les règles de détection et leurs conditions de déclenchement.
5. Vérifier si l'activité peut être expliquée par un comportement légitime.
6. Documenter les preuves et les incertitudes restantes.
7. Proposer des actions adaptées à la situation observée.

### Résultats attendus

L'investigation devra permettre de produire :

- Des exemples de journaux pertinents.
- Les informations relatives aux alertes et aux règles concernées.
- Une chronologie des événements.
- Une évaluation argumentée des éléments observés.
- Une analyse des limites de détection.
- Un plan d'action proposé.

Les résultats réels seront ajoutés après l'exécution et la validation du scénario.

## 8. Modèle de rapport d'incident

Chaque investigation devra comporter les sections suivantes :

1. **Résumé de l'incident :** que s'est-il passé ?
2. **Périmètre :** quels systèmes et comptes sont concernés ?
3. **Chronologie :** quels événements se sont produits et à quel moment ?
4. **Éléments de preuve :** quels journaux et alertes soutiennent l'analyse ?
5. **Évaluation :** quels faits sont confirmés, suspectés ou inconnus ?
6. **Impact potentiel :** quelles ressources pourraient être affectées ?
7. **Réponse :** quelles mesures de confinement et de correction sont recommandées ?
8. **Retour d'expérience :** que pourrait-on améliorer ?
9. **Amélioration de la détection :** comment rendre la surveillance plus efficace ?

## 9. Organisation du dépôt

```text
soc-home-lab-wazuh/
├── README.md
├── .gitignore
├── docs/
│   ├── architecture.md
│   ├── installation.md
│   ├── detection.md
│   └── incident-report.md
├── config/
│   └── agent/
├── tests/
│   └── sample-events.json
├── scripts/
│   └── README.md
└── screenshots/
    └── README.md
```

Les fichiers seront ajoutés progressivement, au fur et à mesure de la réalisation des différentes phases. Les configurations publiées seront expurgées de toute information sensible.

## 10. Sécurité et cadre des tests

Toutes les manipulations seront réalisées dans un environnement personnel ou sur des systèmes pour lesquels une autorisation explicite a été obtenue.

- Aucun accès non autorisé à des systèmes tiers.
- Aucun test contre des infrastructures publiques sans autorisation.
- Aucun mot de passe réel, jeton secret ou donnée personnelle dans le dépôt.
- Aucune capture d'écran contenant des informations sensibles.
- Utilisation d'événements synthétiques lorsque les journaux réels ne sont pas nécessaires.
- Documentation du périmètre et des autorisations des tests.

## 11. Compétences visées

Ce projet doit permettre de développer progressivement les compétences suivantes :

- Administration de systèmes Linux.
- Compréhension et analyse des événements de sécurité.
- Utilisation des concepts SIEM.
- Surveillance des authentifications.
- Investigation et qualification des alertes.
- Validation des mécanismes de détection.
- Analyse des faux positifs.
- Documentation technique.
- Rédaction de rapports d'incident.
- Communication et justification des décisions techniques.

## 12. Limites du projet

Ce laboratoire personnel ne constitue pas un SOC de production.

Les résultats dépendent des systèmes surveillés, des sources de journaux activées, de la configuration, des règles de détection et des scénarios testés.

La réussite d'un test ne prouve pas que toutes les attaques seront détectées. La couverture de détection et les faux positifs devront être évalués dans un périmètre défini.

## 13. Améliorations futures

Les évolutions possibles comprennent :

- La surveillance d'un poste Windows.
- La création et la validation de règles Wazuh personnalisées.
- L'ajout de règles Sigma et l'étude de leur compatibilité.
- La correspondance des détections avec MITRE ATT&CK.
- L'automatisation de tests reproductibles avec Python.
- L'ajout de nouveaux scénarios d'incident.
- La comparaison des résultats selon les sources de journaux.

Ces évolutions seront priorisées selon leur intérêt pédagogique et le temps disponible.

## 14. Références

- [Documentation officielle de Wazuh](https://documentation.wazuh.com/current/)
- [Guide de démarrage Wazuh](https://documentation.wazuh.com/current/getting-started/)
- [Spécification Sigma](https://github.com/SigmaHQ/sigma-specification)
- [MITRE ATT&CK](https://attack.mitre.org/)

---

**Auteur :** Devnew14

**Type de projet :** laboratoire personnel de cybersécurité défensive (Blue Team)

**Statut :** en cours de réalisation
