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



