# Bras_Robot_4DDL

Simulation et contrôle le bras robotique avec MATLAB, Simulink et Simscape Multibody

![Bras4ddl](https://user-images.githubusercontent.com/46745468/146089247-a5815b74-6f4e-446c-b6c0-c4044bb0ba2c.png)


Le schéma bloc du control sur Simulink :

![BlockControl_SIMULINK](https://user-images.githubusercontent.com/46745468/146233262-87a942a0-33e8-4952-93f3-e39e35206da0.PNG)


Il existe deux méthodes pour contrôler les robots en termes de positionnement et d'orientation, et c'est l'utilisation de la « forward » cinématique ou « inverse » cinématique.

La « forward » cinématique est utilisée lorsque nous devons trouver la position et l'orientation de l'effecteur terminal à partir des angles articulaires donnés.

D'autre part, la « inverse » cinématique est utilisée lorsque nous devons trouver les angles d'articulation pour une position donnée de l'effecteur. Cette méthode a plus de sens en robotique car la plupart du temps, nous voulons que le robot positionne son outil à un endroit particulier ou à des coordonnées X, Y et Z particulières.

Avec la cinématique inverse, nous pouvons calculer les angles des articulations en fonction de coordonnées données.

https://user-images.githubusercontent.com/46745468/146230436-c3f0c3c8-f216-4cb8-895f-951ab6fca8a6.mp4





https://user-images.githubusercontent.com/46745468/146230445-c7dea4e4-3e3f-4dcc-883e-c0c1942650e0.mp4


# Multi-Loop PID Control

Cette partie montre comment utiliser looptune pour régler un PID contrôleur multi-boucles.

![1](https://user-images.githubusercontent.com/46745468/146236149-269cf86b-a5d6-4118-bc54-226c3a767256.png)

Le contrôleur se compose de quatre contrôleurs PID (un par joint). Chaque régulateur PID est implémenté à l'aide du bloc "2-DOF PID Controller" de la librairie Simulink

![2](https://user-images.githubusercontent.com/46745468/146236250-670b3c7e-e028-4491-9301-d347f8c37a42.png)

En règle générale, ces contrôleurs multi-boucles sont réglés séquentiellement en réglant une boucle PID à la fois et en parcourant les boucles jusqu'à ce que le comportement global soit satisfaisant. Ce processus peut prendre du temps et il n'est pas garanti qu'il converge vers le meilleur réglage global. Vous pouvez également utiliser systune ou looptune pour régler conjointement les quatre boucles PID en fonction des exigences au niveau du système telles que le temps de réponse et le couplage croisé minimum.


Dans cet exemple, le bras doit se déplacer vers une configuration particulière en environ 1 seconde avec un mouvement angulaire fluide à chaque articulation. Le bras commence dans une position verticale complètement étendue avec tous les angles d'articulation à zéro. La configuration finale est spécifiée par les positions angulaires : Joint1 = 60 deg, Joint2 = -10 deg, Joint3 = 60 deg, Joint4 = 90 deg. Les trajectoires angulaires des paramètres PID d'origine sont indiquées ci-dessous. De toute évidence, la réponse est trop lente et l'avant-bras vacille.

![3](https://user-images.githubusercontent.com/46745468/146238661-875362c1-a72f-4ba2-8848-84fbdf44421a.png)

Par conséquence, je vais essayer une " Réglage des contrôleurs PID avec LOOPTUNE " 

Avec looptune, je peux régler directement les quatre boucles PID pour obtenir le temps de réponse souhaité avec une interaction de boucle minimale et des marges de stabilité MIMO adéquates. Le contrôleur est réglé en temps continu et discrétisé automatiquement lors de la réécriture des gains PID dans Simulink. Utilisez l'interface "slTunable" pour spécifier quels blocs doivent être réglés et où se trouve la limite usine/contrôleur.

![4](https://user-images.githubusercontent.com/46745468/146240125-eadf768f-de46-42b8-be3c-ab78b07419c3.png)

Dans son utilisation la plus simple, looptune n'a besoin de connaître que la bande passante de contrôle cible, qui doit être au moins deux fois l'inverse du temps de réponse souhaité. Ici le temps de réponse souhaité est de 1 seconde alors essayez une bande passante cible de 5 rad/s

![5](https://user-images.githubusercontent.com/46745468/146240310-8cb90940-ab6a-4946-9685-4d61ad3b7180.png)

Une valeur finale proche ou inférieure à 1 indique que looptune a atteint la bande passante demandée. Comparez les réponses à une commande pas à pas en position angulaire pour les contrôleurs initiaux et réglés.

![6](https://user-images.githubusercontent.com/46745468/146240436-cf765670-1b05-45af-ba23-40f3edd28473.png)


![8](https://user-images.githubusercontent.com/46745468/146240468-a8a18538-8226-4fb7-86df-84ebbb90dbf6.png)

Les quatre courbes s'installant près de y=1 représentent les réponses indicielles de chaque joint, et les courbes s'installant près de y=0 représentent les termes de couplage croisé. Le contrôleur accordé est une nette amélioration. 



