# Démonstration SOC : détection d'une tentative de connexion SSH échouée

## 1. Objectif

Pour ce test, je voulais vérifier que Wazuh était capable de détecter une tentative de connexion SSH échouée et de générer une alerte exploitable pour un analyste SOC.

## 2. Environnement utilisé

Le test a été réalisé dans mon laboratoire de cybersécurité avec les éléments suivants :

- **Système :** Ubuntu
- **SIEM :** Wazuh
- **Service surveillé :** OpenSSH
- **Utilisateur testé :** `utilisateur_test_inexistant`
- **Adresse source observée :** `127.0.0.1`

L'objectif était de générer un événement contrôlé, puis de vérifier comment il était enregistré et détecté.

## 3. Déroulement du test

J'ai lancé une tentative de connexion SSH en utilisant volontairement un nom d'utilisateur qui n'existe pas sur le système.

La connexion a échoué, comme prévu. J'ai ensuite consulté les journaux SSH d'Ubuntu, puis les alertes remontées par Wazuh pour vérifier que l'événement avait bien été détecté.

## 4. Résultats obtenus

L'analyse des alertes a permis d'identifier deux règles pertinentes :

- **Règle 5710 — Niveau 5 :** tentative de connexion avec un utilisateur inexistant.
- **Règle 5503 — Niveau 5 :** échec d'authentification détecté par PAM.

Ces deux alertes correspondent au type d'événement généré pendant le test. Le niveau 5 indique la classification attribuée par Wazuh ; il ne suffit pas, à lui seul, à confirmer une attaque.

## 5. Capture 1 — Vue générale de Wazuh

La première capture présente le tableau de bord général. Sur la période sélectionnée, il affiche 468 événements au total et 6 échecs d'authentification.

Cette vue permet d'avoir un aperçu de l'activité surveillée. Ces chiffres correspondent aux données affichées dans le tableau de bord et ne représentent pas nécessairement des attaques.

![Vue générale du tableau de bord Wazuh](../screenshots/test1wazuh.png)

## 6. Capture 2 — Résultats du test

La deuxième capture montre une vue filtrée affichant 2 événements au total et 2 échecs d'authentification.

J'ai ensuite examiné les alertes correspondantes, notamment les règles 5710 et 5503, afin de comprendre pourquoi elles avaient été déclenchées.

![Vue filtrée du test SSH](../screenshots/test2Wazuh.png)

## 7. Analyse et interprétation

Ce test m'a permis de suivre plusieurs étapes importantes d'une investigation SOC :

1. Générer un événement de sécurité dans un environnement contrôlé.
2. Vérifier sa présence dans les journaux système.
3. Examiner les alertes produites par Wazuh.
4. Comprendre les règles déclenchées et les informations qu'elles fournissent.
5. Identifier les limites du test et les vérifications à réaliser pour approfondir l'analyse.

Un point important concerne l'adresse `127.0.0.1`, qui correspond à la boucle locale. Le test valide donc la détection d'un événement local, mais ne démontre pas encore la détection d'une tentative provenant d'une machine distante.

## 8. Améliorations envisagées

Pour approfondir ce laboratoire, je souhaite notamment :

- Réaliser plusieurs tentatives de connexion échouées dans un environnement contrôlé.
- Étudier la détection de tentatives répétées et les règles associées.
- Examiner les faux positifs et les possibilités d'amélioration des alertes.
- Tester la collecte d'événements provenant d'une autre machine de laboratoire.
- Rédiger un compte rendu d'investigation avec les observations, les éléments de preuve et les recommandations.

## 9. Conclusion

Ce premier test m'a permis de vérifier le fonctionnement de la détection d'échecs de connexion SSH avec Wazuh. J'ai pu examiner les journaux système, retrouver les alertes correspondantes et commencer à interpréter les résultats dans une démarche d'analyse SOC.

La prochaine étape sera d'approfondir les tests afin de mieux comprendre la détection de comportements répétés et la manière dont un analyste SOC qualifie un événement suspect.