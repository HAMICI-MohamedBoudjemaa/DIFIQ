# Cas d'étude
- Le jeu de données *~={green}voitures=~* contient 18 observations, pour des voitures, des 9 variables suivantes :
	- **~={green}Modele=~** : Modèle
	- **~={green}Cyl=~** : Cylindrée (en $l$)
	- **~={green}puis=~** : puissance (en $cm^3$)
	- **~={green}lon=~** : longueur (en $cm$)
	- **~={green}lar=~** : largeur (en $cm$)
	- **~={green}poids=~** : poids (en $kg$)
	- **~={green}vitesse=~** : vitesse maximale (en $km.h^{-1}$)
	- **~={green}finit=~** : finition ("M" : moyenne, "B" : bonne, "TB" : très bonne)
	- **~={green}prix=~**  : prix (en $F$)
- Le faible nombre de variables dans le cas d'études permet de représenter chaque individu par un diagramme en étoile
- Chaque valeur est reportée su la branche correspondante (qui va de la valeur $min$ à la valeur $max$)
![[Pasted image 20251216160527.png]]
- On constate que les étoiles sont plutôt harmonieuses avec des tailles variables
- Certaines étoiles sont de forme particulière, notamment les petites voitures sportives dont la vitesse est très élevée par rapport rapport au gabarit
## Ecart-type
| CYL   | PUIS | LON  | LAR | POIDS | VITESSE |
| ----- | ---- | ---- | --- | ----- | ------- |
| 373.9 | 20.4 | 22.1 | 5.3 | 137.0 | 12.1    |
## Boîte à moustache
![[Pasted image 20251216161655.png]]
## Scatter plots
![[Pasted image 20251216161844.png]]
## Représentations centrée et réduite
- **Moyenne** : $$\bar x_j = \frac {1}{n} \sum_{i=1}^n x_{ij}$$
- **Variance** : $$s_j^2 = \frac {1}{n} \sum_{i=1}^n (x_{ij} - \bar x_j)^2$$
- La **représentation centrée** consiste à centrer les variables (==soustraire l'espérance à chacune des valeurs afin de que la distribution soit centrée en 0==)$$\forall i \in \{1,...,n\}, \forall j \in \{1,...,p\} : y_{ij} = x_{ij} - (- \bar x_j)$$
- La **représentation réduite** consiste à réduire les variables (==diviser chacune des valeurs par l'écart type afin de que la distribution de variance 1==)$$\forall i \in \{1,...,n\}, \forall j \in \{1,...,p\} : z_{ij} = \frac {x_{ij} - (- \bar x_j)}{S_j}$$
- Les différentes variables $X_j$ pouvant être hétérogènes, et correspondre à des échelles de mesure disparates,  la représentation réduite est utilisée pour éviter que le choix de ces unités ait une influence dans le calcul des distances
- A minima, une **ACP** s'effectue toujours à partir d'une **représentation centrée**
- Lorsque la représentation est **centrée-réduite**, on parle d'**ACP normée**
## Choix d'une métrique
- L'ACP requiert un **espace vectoriel** muni d'un **produit scalaire**
- Pour 2 individus $i_1$ et $i_2$, on considère la distance suivante :$$d_M^2(i_1,i_2) = (x_{i_1} - x_{i_1})$$