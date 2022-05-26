# Olist_Client_Segmentation
Créer une segmentation des clients que l'équipe marketing du site e-commerce brésilien Olist pourra exploiter dans le cadre de leurs campagnes de communication

Lien des consignes académiques OpenClassRooms: https://openclassrooms.com/fr/paths/148/projects/630/assignment

## Présentation

Olist souhaite que vous fournissiez à ses équipes d'e-commerce une segmentation des clients qu’elles pourront utiliser au quotidien pour leurs campagnes de communication.

Votre objectif est de comprendre les différents types d’utilisateurs grâce à leur comportement et à leurs données personnelles.

Vous devrez fournir à l’équipe marketing une description actionable de votre segmentation et de sa logique sous-jacente pour une utilisation optimale, ainsi qu’une proposition de contrat de maintenance basée sur une analyse de la stabilité des segments au cours du temps.

## Base de données

Pour cette mission, Olist vous fournit une base de données anonymisée comportant des informations sur l’historique de commandes, les produits achetés, les commentaires de satisfaction, et la localisation des clients depuis janvier 2017.
Lien: https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce

## Traitement et nettoyage de la donnée

- 9 fichiers csv à disposition: utilisation correcte des merges afin de créer un dataframe unique avec toutes les données exploitables
- Suppression des colonnes non pertinentes
- Gestion des nans
- Résultat du nettoyage: DataFrame avec une ligne par produit commandé (une commande de plusieurs produits = plusieurs lignes)

## DataViz

Le site web est relativement nouveau.
Conséquence: 97% des clients n'ont effectué qu'une seule commande
![image](https://user-images.githubusercontent.com/76253068/170501237-3f647bf0-cbcc-4084-b74d-04775523d9f2.png)

### Distribution du nombre de produit par commande

![image](https://user-images.githubusercontent.com/76253068/170501636-1777b89d-e1b5-47b8-bb42-819696554d4a.png)

### Distribution du montant total par commande

![image](https://user-images.githubusercontent.com/76253068/170501871-7a3c06b6-264c-4c02-8eae-b8af2e8d84f3.png)

### Distribution du nombre de commande par mois

![image](https://user-images.githubusercontent.com/76253068/170501997-1633176c-a0fb-4a7b-961b-6f5ad338a9eb.png)

## Modélisation

### Implémentation du modèle RFM

### Passage d'un dataframe produits commandés à un dataframe commandes
![image](https://user-images.githubusercontent.com/76253068/170502523-c845d42e-b7e3-4344-883f-c485179a9151.png)

### Passage d'un dataframe commande à un dataframe RFM par clients uniques
![image](https://user-images.githubusercontent.com/76253068/170502354-edbcf183-d6fb-40cc-8111-8308fc6efa5e.png)

### Transformation logarithmique

Normalisation efficace des variables frequency et monetary

![image](https://user-images.githubusercontent.com/76253068/170503768-c2792370-8d1b-4d85-902f-0eeedd7fad11.png)

## Feature engineering

### Détermination du nombre de clusters
![image](https://user-images.githubusercontent.com/76253068/170504054-2fb5509e-d948-4e41-966d-8fdf0e0655f4.png)

![image](https://user-images.githubusercontent.com/76253068/170504137-e493673d-2179-4be6-9a67-f856b6633109.png)

![image](https://user-images.githubusercontent.com/76253068/170505477-333a357b-f7e9-4e9d-97e6-b45011e741ac.png)

On observe que tous les clients ayant effectué plus d'une commande sont dans une catégorie (fidèles)

Parmi ceux ayant commandé une seule fois, ceux ayant dépensé beaucoup sont dans une deuxième catégorie (dépensiers).

Ceux ayant commandé il y a longtemps et peu dépensé dans une troisième catégorie (économes).

Ceux ayant commandé récemment et peu dépensé dans une quatrième catégorie (nouveaux clients)

### Détermination du nombre de clusters en rajoutant la variable reviews

![image](https://user-images.githubusercontent.com/76253068/170505792-39bdd382-d6f9-4bf1-a669-983492993372.png)

Grâce à l'ajout de la nouvelle variable review, un nouveau cluster, celui des clients insatisfaits, peut être ajouté à la liste.
(voir cluster 0 dans le graphique ci-dessous)

![image](https://user-images.githubusercontent.com/76253068/170506507-ef2207f9-d1c9-4660-84ff-dff045be7168.png)

### Essais d'autres algorithmes que K-Means

Les essais n'ont pas été fructueux, le K-Means sera donc retenu

## Modèle retenu

![image](https://user-images.githubusercontent.com/76253068/170506964-f37bc24b-6370-4bba-80af-123ea79a6d22.png)

### Interprétation des clusters

![image](https://user-images.githubusercontent.com/76253068/170507060-a4a011ce-7d4b-42f9-b62c-c8103a8d9eac.png)

## Mis à jour du modèle

### Simulation d'un modèle entraîné en janvier 2018
### Evolution de l'ARI score au fil des mois:
![image](https://user-images.githubusercontent.com/76253068/170507504-d7fd6c15-120a-44c3-80ed-8fd8c0584cb2.png)

Le score passe en dessous du seuil symbolique de 0.8 au bout de 3 mois, fréquence à laquelle le modèle devra être réentraîné.

## Synthèse 

![image](https://user-images.githubusercontent.com/76253068/170507972-7aa2259d-7216-43e6-8282-89fdac67c4d2.png)
