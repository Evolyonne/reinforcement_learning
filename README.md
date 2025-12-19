# Projet de Reinforcement Learning — BipedalWalker

## 1. Présentation générale du projet

Ce projet a pour objectif de mettre en pratique les notions de **Reinforcement Learning (RL)**
vues en cours à travers une étude expérimentale et comparative sur l’environnement
**BipedalWalker-v3** de Gymnasium, dédié au contrôle continu d’un robot bipède.

L’accent est mis sur :
- la compréhension de l’environnement,
- l’implémentation et l’entraînement de plusieurs algorithmes de RL,
- la comparaison rigoureuse de leurs performances,
- l’analyse critique des résultats obtenus.

---

## 2. Description de l’environnement

### Environnement utilisé
- **Nom** : BipedalWalker-v3  
- **Bibliothèque** : Gymnasium  
- **Type** : contrôle continu basé sur la physique (Box2D)

L’environnement simule un robot bipède devant apprendre à marcher de manière autonome
sans tomber, sur un terrain généré procéduralement.


---

### États (observations)
Les observations sont continues et décrivent :
- la posture du robot,
- les angles et vitesses des articulations,
- les contacts des pieds avec le sol,
- certaines informations liées au terrain.

---

### Actions
Les actions sont continues et correspondent aux **commandes des moteurs des jambes** :
- 4 actions réelles dans l’intervalle \([-1, 1]\),
- chaque action contrôle un couple moteur.

---

### Récompenses
La fonction de récompense combine :
- une récompense positive liée à la progression vers l’avant,
- des pénalités en cas de mouvements inefficaces,
- une forte pénalité en cas de chute.

Dans certaines extensions du projet, une mécanique de **collecte de récompenses**
(“coins”) est ajoutée via un wrapper Gymnasium afin de transformer la tâche en un
jeu d’optimisation séquentielle.

---

### Conditions de terminaison
Un épisode se termine lorsque :
- le robot chute,
- le nombre maximal de pas est atteint,
- ou que le parcours est complété.

---

## 3. Algorithmes implémentés

Les algorithmes suivants ont été implémentés et évalués dans le cadre de ce projet :

- **PPO (Proximal Policy Optimization)** — algorithme on-policy servant de référence
- **A2C (Advantage Actor-Critic)** — approche actor-critic synchrone
- **SAC (Soft Actor-Critic)** — algorithme off-policy basé sur l’entropie maximale
- **TD3 (Twin Delayed Deep Deterministic Policy Gradient)** — algorithme off-policy
  conçu pour améliorer la stabilité de l’apprentissage en contrôle continu

Chaque algorithme est implémenté dans un **notebook séparé**, avec une structure identique
afin de faciliter la comparaison.

---

## 4. Résultats et comparaisons

Chaque algorithme est évalué à l’aide des métriques suivantes :

- **Score moyen par épisode** (évaluation sur épisodes indépendants)
- **Score final** (moyenne des derniers épisodes d’entraînement)
- **Vitesse d’apprentissage** (nombre d’épisodes nécessaires pour atteindre un seuil de performance)
- **Stabilité** (écart-type des récompenses sur les derniers épisodes)
- **Temps d’entraînement**

Un tableau comparatif est utilisé pour synthétiser les résultats et mettre en évidence
les différences de comportement entre les algorithmes.

Des **courbes d’apprentissage** (récompense par épisode et moyenne glissante) sont
également présentées pour visualiser la convergence.

---

## 5. Analyse critique

Les expériences montrent que :
- PPO fournit une base solide mais peut être instable sans réglage précis,
- le **PPO amélioré** offre une meilleure stabilité et de meilleures performances
  au prix d’un temps d’entraînement plus élevé,
- **SAC** présente une exploration plus efficace et une bonne stabilité grâce à
  son approche off-policy, mais nécessite plus de mémoire (replay buffer).

Les tests sur **BipedalWalkerHardcore-v3** mettent en évidence les limites de
généralisation des politiques entraînées sur la version standard, en particulier
face aux trous et obstacles complexes.

Ces résultats illustrent l’importance du choix de l’environnement d’entraînement
et du réglage des hyperparamètres en Reinforcement Learning.

---

## 6. Utilisation des outils d’IA

L’utilisation d’outils d’IA (notamment **ChatGPT**) a été effectuée comme **outil
d’assistance** pour :
- clarifier certains concepts théoriques,
- structurer le code et la documentation,
- améliorer la lisibilité et l’organisation des notebooks.

Tous les choix algorithmiques, les implémentations et les analyses ont été compris,
adaptés et validés par les étudiants, conformément aux consignes du projet.

---

## 7. Instructions d’exécution et de reproduction

### Prérequis
- Python ≥ 3.9
- gymnasium
- stable-baselines3
- numpy, pandas, matplotlib
- pygame (pour la visualisation)

### Installation
```bash
pip install gymnasium stable-baselines3 pygame numpy pandas matplotlib
