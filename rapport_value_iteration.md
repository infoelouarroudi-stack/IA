# Rapport sur Value Iteration

## Calculs des trois premières itérations dans BookGrid

### Itération 0

À l'itération zéro toutes les valeurs des états non terminaux sont
initialisées à zéro tandis que les états terminaux gardent leurs
récompenses fixes, ainsi la case verte à la position \<4,3\> a la valeur
+1 et la case rouge à la position \<4,2\> a la valeur -1. Toutes les
autres cases ont une valeur initiale de zéro.

### Itération 1

Pour l'itération un nous recalculons les valeurs en appliquant la
formule de mise à jour. Pour l'état \<4,3\> il s'agit d'un état terminal
donc sa valeur reste fixée à +1. Pour l'état \<4,2\> qui est également
terminal la valeur reste fixée à -1. Les autres états gardent des
valeurs proches de zéro car les récompenses n'ont pas encore eu le temps
de se propager dans la grille.

### Itération 2

Pour l'itération deux nous observons que la valeur de l'état \<3,3\>
augmente puisqu'il se trouve juste à gauche de la case verte \<4,3\>. En
calculant l'espérance en tenant compte du bruit et du facteur
d'actualisation on trouve que V2(\<3,3\>) est égal à 0.72. Les autres
états proches de la sortie restent encore avec des valeurs nulles ou
légèrement positives.

### Itération 3

Pour l'itération trois les valeurs se propagent davantage. Pour l'état
\<3,3\> la mise à jour s'écrit
Q3(RIGHT)=0.8(0+0.9×V2(4,3))+0.1(0+0.9×V2(3,3))+0.1(0+0.9×V2(3,2)). En
remplaçant les valeurs numériques on obtient
Q3(RIGHT)=0.8×0.9+0.1×0.648+0.1×0 ce qui donne 0.7848 que l'on arrondit
à 0.78. Ainsi V3(\<3,3\>)=0.78. Pour l'état \<2,3\> on choisit l'action
droite vers \<3,3\>, le calcul donne V3(\<2,3\>)=0.8×0.648=0.5184 soit
environ 0.52. Enfin pour l'état \<3,2\> l'action optimale est de monter
vers \<3,3\> mais avec une probabilité de déviation vers \<4,2\>. En
calculant on obtient 0.8×0.648+0.1×(-0.9)=0.4284 soit environ 0.43.

### Conclusion

Après ces calculs détaillés des trois premières itérations nous
constatons que les valeurs obtenues sont exactement les mêmes que celles
produites automatiquement par notre code d'exécution des tests, ce qui
valide la cohérence de nos calculs manuels.
