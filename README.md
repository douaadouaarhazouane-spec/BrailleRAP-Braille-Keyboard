# BrailleRAP-Braille-Keyboard
Autonomous Braille Keyboard for BrailleRAP using STM32
# Clavier braille autonome pour BrailleRAP

## Présentation

BrailleRAP est une machine permettant d'imprimer du texte en braille à l'aide de moteurs pas à pas et d'un électroaimant.

À l'origine, l'utilisation de la machine nécessite un ordinateur pour envoyer le texte à imprimer. L'objectif de ce projet est de développer un clavier braille autonome permettant d'écrire directement sur la BrailleRAP, sans passer par un ordinateur.

Ce projet a été réalisé dans le cadre d'un stage de Master 1 EEEA – Systèmes Embarqués à l'ISTIC – Université de Rennes.

## Problème rencontré

L'utilisation de la BrailleRAP dépendait principalement d'un ordinateur. Cela pouvait limiter l'autonomie de l'utilisateur, notamment pour des personnes malvoyantes ou des jeunes enfants.

Le besoin principal était donc de proposer une interface simple, directe et plus accessible.

## Solution proposée

La solution développée repose sur un clavier braille composé de six boutons principaux correspondant aux six points d'une cellule braille.

Une carte STM32 lit les boutons, identifie la combinaison saisie, puis envoie des commandes G-code à la carte MKS Gen L via une liaison UART. La carte MKS pilote ensuite les moteurs et l'électroaimant pour imprimer les caractères braille.

## Architecture du système


Utilisateur
   ↓
Clavier braille
   ↓
STM32
   ↓ UART
MKS Gen L
   ↓
Moteurs + électroaimant
   ↓
Feuille braille
## Fonctionnement général

Le fonctionnement du système est simple et entièrement autonome. L'utilisateur appuie sur une combinaison de boutons correspondant à une lettre en braille. La carte STM32 lit l'état des boutons, reconnaît le caractère associé puis génère les commandes G-code nécessaires.

Ces commandes sont envoyées par une liaison UART à la carte MKS Gen L, qui exécute les déplacements des moteurs et active l'électroaimant afin de former les points braille sur la feuille.


Lecture des boutons
        ↓
Identification de la lettre
        ↓
Génération des commandes G-code
        ↓
Communication UART
        ↓
Carte MKS Gen L
        ↓
Déplacement des moteurs
        ↓
Activation de l'électroaimant
        ↓
Impression du caractère braille



## Fonctionnement général

Le fonctionnement du clavier est entièrement autonome. L'utilisateur appuie sur une combinaison de boutons correspondant aux points d'une cellule braille. La carte STM32 lit cette combinaison, identifie le caractère associé puis génère les commandes nécessaires à son impression.

Ces commandes sont transmises via une liaison UART à la carte MKS Gen L, qui exécute les déplacements des moteurs et commande l'électroaimant afin de créer les points braille sur la feuille.


Utilisateur
      │
      ▼
Appui sur les boutons
      │
      ▼
Lecture par la STM32
      │
      ▼
Identification du caractère
      │
      ▼
Génération des commandes G-code
      │
      ▼
Communication UART
      │
      ▼
Carte MKS Gen L
      │
      ▼
Moteurs + Électroaimant
      │
      ▼
Impression du caractère en braille

# Fonctionnalités

Le système développé permet actuellement :

* Impression des lettres de l'alphabet (A à Z)
* Gestion des espaces entre les mots
* Retour automatique à la ligne
* Éjection automatique de la feuille
* Impression de plusieurs signes de ponctuation
* Communication directe avec la BrailleRAP sans utiliser un ordinateur



# Matériel utilisé

Le prototype est constitué des éléments suivants :

| Composant         | Rôle                                    |
| ----------------- | --------------------------------------- |
| STM32             | Gestion du clavier et de la logique     |
| MKS Gen L V2.1    | Pilotage de la machine                  |
| Firmware Marlin   | Interprétation des commandes G-code     |
| Boutons poussoirs | Saisie des points braille               |
| Électroaimant     | Formation des points braille            |
| Moteurs pas à pas | Déplacement selon les axes X et Y       |
| Connecteurs Wago  | Distribution des connexions électriques |



# Architecture matérielle

Le système est composé de deux parties principales :

* Le clavier braille piloté par la STM32.
* La machine BrailleRAP pilotée par la carte MKS Gen L.

La STM32 interprète les combinaisons braille puis envoie les commandes à la MKS, qui contrôle les moteurs et l'électroaimant afin de réaliser l'impression.


# La machine BrailleRAP et clavier 

![clv](Images/clv.jpg)


