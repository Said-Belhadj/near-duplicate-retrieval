# Near Duplicate Retrieval for Historical Images

## Présenté par: Saïd BELHADJ

## Table des matières
1. [Introduction](#introduction)
2. [Les données](#les-données)
3. [Architecture proposée](#architecture-proposée)
4. [Résultats](#résultats)
5. [Licence](#licence)

## Introduction
Le projet "Near Duplicate Retrieval for Historical Images" vise à offrir aux historiens un outil permettant de retracer l'origine et l'utilisation des images dans les archives historiques, afin de découvrir et de corriger les usages incorrects ou falsifiés des images dans le contexte de conflits.

## Les données
Le dataset initial comprend 274 images de scènes de combat et de conflits, incluant des images de cadavres et d'autres aspects graphiques des batailles. Les images sont réparties en 71 classes. Pour pallier le nombre limité d'images, une stratégie d'augmentation de données ciblée a été mise en place pour simuler les altérations typiques des documents anciens numérisés :

### Types d'augmentation réalisés :
- **Ajout de Bruit** : Simuler les imperfections du scan.
- **Ajustements de Luminosité** : Reproduire les variations dues à l'usure.
- **Transformations Affines** : Imiter les distorsions physiques comme le pliage.
- **Flip Horizontal & Vertical** : Assurer la reconnaissance d'images sous différentes orientations.

Après l'augmentation des données, le dataset comprend désormais 2 192 images :
- **Entraînement** : 1 520 images
- **Validation** : 408 images
- **Test** : 264 images

### Distribution des données 


## Architecture proposée
Le modèle développé pour ce projet repose sur plusieurs variantes de ResNet, notamment ResNet 152, ResNet 34 et ResNet 18. Le modèle a été entraîné sur 60 epochs avec deux fonctions de coût différentes pour une tâche de classification : la cross-entropy et la triplet margin.

La **Triplet Margin Loss** est utilisée pour entraîner un modèle à distinguer précisément entre des exemples positifs et négatifs dans un espace d'apprentissage métrique.

De plus, la PCA (Principal Component Analysis) a été utilisée pour réduire la dimensionnalité des embeddings générés par le ResNet, augmentant ainsi la vitesse de traitement et concentrant le modèle sur les caractéristiques les plus pertinentes. Cette approche a été préférée pour pallier le problème des scores entassés entre 0.99 et 0.98, permettant une meilleure discrimination entre les images.

## Résultats
Les performances du modèle ont été évaluées sur deux tâches principales : la classification et la récupération d'images quasi-dupliquées.

### Tâche de Classification
- **Cross Entropy Loss** : Précision de 47%, Rappel de 46%
- **Triplet Margin Loss** : Précision de 46%, Rappel de 44%

### Near Duplicate Retrieval
- **Cross Entropy Loss** :
  - Mean nDCG : 95.12%
  - Mean Top-5 Accuracy : 82%
- **Triplet Margin Loss** :
  - Mean nDCG : 97%
  - Mean Top-5 Accuracy : 82%

## Conclusion
Ce projet montre l'efficacité des techniques de CBIR (Content-Based Image Retrieval) pour la recherche d'images historiques en utilisant des modèles de deep learning comme ResNet combinés à des techniques d'augmentation de données et de réduction de dimensionnalité.

## Licence
Ce projet est sous licence [Nom de la licence].

---

Pour plus d'informations, veuillez consulter le rapport complet dans le document PDF joint.
