# Première approche "à la main" du problème

## Introduction

Nous voulons concentrer nos recherches autour de la prédiction de passe. Ainsi nous allons chercher des modèles permettant cette prédiction pour ensuite les intégrer à l'interface visuelle. Notre idée générale est la suivante : donner une valeur en terme de possibilité de passe à chaque zone du terrain en prenant en compte plusieurs paramètres pouvant encourager ou au contraire empêcher une passe. 
Nous allons procéder par étape en intégrant petit à petit de nouvelles contraintes.

## 1er modèle

Dans une première approche on se place en 2D. On cherche à découper le terrain en zones où le ballon pourrait être envoyé par le joueur qui le possède tout en étant conservé par l'équipe qui attaque (sans être intercepté par un adversaire ou bien sorti hors des limites du terrain). On appellera ces zones : zone de passe et zone perdue. On fait les hypothèses suivantes 
pour déterminer chaque zone :
- les joueurs peuvent se déplacer depuis leur position à une vitesse Vj constante pour tous les joueurs.
- la vitesse du ballon est constante : pas de décélération => le ballon ne s'arrête pas
- la vitesse Vb du ballon est plus grande que celle des joueurs 

Afin de déterminer chaque zone on effectue de la manière suivante :
- on découpe le terrain en associant au ballon et aux joueurs les points pour lesquels ils sont les plus proches (qu'ils sont les plus rapides à rejoindre par rapport aux autres). Ce découpage revient à déterminer les espaces de Voronoï associés aux joueurs et au ballon en donnant un point double au ballon. Ainsi les zones où les défenseurs arrivent plus vite que les attaquants sont des zones perdues. De même les zones où le ballon arrive plus vite que les joueurs est une zone perdue car cela signifie qu'il ira hors des limites du terrain (cf schéma 1).

<table border="0">
  <tr>
    <td>
      <img src="schema1.png" style="width: 70px;">
    </td>
  </tr>
</table>

- il reste des zones non perdues qui devraient l'être (cf zone rayée schéma 2). Ainsi il faut prendre en compte le fait que si la balle passe par une zone de défenseur pour atteindre une autre zone libre elle sera alors perdue car interceptée par le défenseur
(cf schéma 3)

<table border="0">
  <tr>
    <td>
      <img src="Images/schema2.png" style="width: 70px;">
    </td>
  </tr>
</table>

<table border="0">
  <tr>
    <td>
      <img src="Images/schema3.png" style="width: 70px;">
    </td>
  </tr>
</table>

## Prise en compte de la vitesse des joueurs

La vitesse des joueurs va influencer le découpage des zones puisqu'un joueur peut se trouver plus loin d'une zone qu'un autre joueur et arriver plus vite que ce dernier. Ce problème est illustré sur le schéma suivant :

<table border="0">
  <tr>
    <td>
      <img src="Images/schema4.png" style="width: 70px;">
    </td>
  </tr>
</table>