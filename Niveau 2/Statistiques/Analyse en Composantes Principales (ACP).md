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
- Pour 2 individus $i_1$ et $i_2$, on considère la distance suivante :$$d_M^2(i_1,i_2) = (x_{i_1} - x_{i_2})^\top M (x_{i_1} - x_{i_2})$$
- où 
	- $M = I_p$ en **ACP non-normée**
	- $M = D_{\frac {1}{s^2}} = diag(\frac {1}{s_1^2},...,\frac {1}{s_p^2})$ en **ACP normée**
## Principe de moindre déformation du nuage
- Pour appréhender le nuage des individus, il est nécessaire de érduier la dimension de l'espace qui le porte
- Les méthodes d'analyse factorielle (dont l'ACP fait partie) réduisent cette dimension par projection orthogonale sur des sous-espaces affines
- De telles projections orthogonales permettent de réduire la dimension mais conduisent à une perte d'information, l'enjeu est de projeter le nuage de points avec une moindre déformation
### Choisir une "bonne" projection
![[Pasted image 20251217210402.png]]
==L'image de droite donne beaucoup plus d'information que l'image de gauche==
### Nuage de points avec leurs projections orthogonales
![[Pasted image 20251217210459.png]]
### Inerties
#### Totale
- L'**inertie totale** du nuage est donnée par : $$\mathcal I_{tot} = \sum_{i=1}^n \omega_i d^2 (i,g)$$
	==Somme pondérée des distances carrées des points au centre de gravité==
- Cette quantité correspond à l'information totale contenue dans l'échantillon
	![[Pasted image 20251217211639.png]]
#### Autour du sous-espace affine
- L'inertie du nuage **~={yellow}autour du sous-espace affine $\mathcal H$**=~ est donnée par : $$\mathcal J_{\mathcal H} = \sum_{i=1}^n \omega_i d^2 (i, \Pi_{\mathcal H}(i))$$
	- où $\Pi_{\mathcal H}$ est la projection orthogonale sur $\mathcal H$
- L'inertie $\mathcal J_{\mathcal H}$ autour de $\mathcal H$ mesure la déformation du nuage lorsque celui-ci est projeté orthogonalement sur $\mathcal H$
- L'inertie $\mathcal J_{\mathcal H}$ doit être **~={red}minimale=~** afin d'avoir une moindre déformation du nuage de points, on choisit donc une **projection $\mathcal H$ la ~={red}minimisant=~**.
#### Sur le sous-espace affine
- L'inertie du nuage ~={yellow}**projeté sur le sous-espace affine $\mathcal H$**=~ est donné par :$$\mathcal I_{\mathcal H} = \sum_{i=1}^n \omega_i d^2 (\Pi_{\mathcal H}(i), \Pi_{\mathcal H}(g))$$
- L'inertie $\mathcal I_{\mathcal H}$ sur $\mathcal H$ mesure l'information subsistant du nuage lorsque celui-ci est projeté orthogonalement sur $\mathcal H$
-  L'inertie $\mathcal I_{\mathcal H}$ doit être **~={green}maximale=~** afin d'avoir une moindre déformation du nuage de points, on choisit donc une **projection $\mathcal H$ la ~={green}maximisant=~**. 
- On peut montrer que le **sous-espace affine** $\mathcal H$ **minimisant** la déformation du nuage contient $g$, on a donc : $$\mathcal I_{\mathcal H} = \sum_{i=1}^n \omega_i d^2 (\Pi_{\mathcal H}(i), g)$$
	- ~={cyan}Car $g = \Pi_{\mathcal H}(g)$ =~
#### Propriétés
- On peut montrer que :$$\mathcal I_{tot} = \mathcal I_{\mathcal H} + \mathcal J_{\mathcal H}$$
- La moindre déformation du nuage de points par projection orthogonale sur un sous-espace affine est obtenue de manière équivalente par :
	- Minimisation de l'inertie autour du sous-espace affine $\mathcal J_{\mathcal H}$
	- Maximisation de l'inertie du nuage projeté sur le sous-espace affine $\mathcal I_{\mathcal H}$
- On peut aussi montrer que :$$\mathcal I_{tot} = Tr(MS)$$
	- D'où en **ACP non-normée** : $$\mathcal I_{tot} = \sum_{j=1}^p s_j^2$$
	- En **ACP normée** : $$\mathcal I_{tot} = p$$
#### Matrice de variance-covariance
- La matrice de variance-covariance $S$ associée au nuage de points vaut :$$S = X^{\top} W X - gg^{\top}$$
- Pour $(i,j) \in \{1,...,p\}^2$, le terme général de la matrice vaut :$$s_{i,j} = cov(X_i, X_j)$$ et son terme diagonal $(i,i)$ vaut $s_i^2$ 
#### Résolution séquentiel du problème d'inertie
- Les vecteurs portant *l'inertie maximale* à chaque pas de la décomposition sont les vecteurs propres de la matrice $SM$ $$\mathcal H_k = vect(a_1,...,a_k)$$
- L'inertie du nuage projeté sur le $k$-ème vecteur propre $a_k$ vaut $\lambda_k$ $$\mathcal I_{a_k} = \lambda_k$$
- L'inertie sur $\mathcal H_k$ est la somme des inerties sur les $k$ vecteurs propres $$\mathcal I_{\mathcal H_k} = \sum_{\alpha = 1}^k \lambda_{\alpha}$$
#### Axes principaux
- Les axes principaux sont les vecteurs propres de $S$ de $M$-norme 1
- Soient $(\lambda_1,...,\lambda_p)$ les valeurs propres de $S$ classées dans l'ordre décroissant :$$\lambda_1 \ge ... \ge \lambda_p \ge 0$$
- Les axes principaux vérifient : $$\forall k \in \{1,...,p\} : SM_{a_k} = \lambda_k a_k$$
	- avec :$$\begin{aligned}
& \forall k \in \{1,...,p\} : ||a_k||_M = 1 \\
& \forall (k, \mathcal l) \in \{1,...,p\}^2, k \ne \mathcal l : <a_k,a_{\mathcal l}>_M = 0
\end{aligned}$$
	==Chaque vecteur est de norme 1 et tous les axes sont orthogonaux pour la métrique M, ce qui permet respectivement d'interpréter directement les valeurs propres comme inerties et de montrer que les composantes principales sont décorrélées==
### Facteurs principaux
- Les facteurs principaux $(u_1,...,u_p)$ sont s=les formes linéaires associées aux axes principaux $(a_1,..,a_p)$ : $$\forall k \in \{1,...,p\} : u_k = M_{a_k}$$
- On a :$$\forall k \in \{1,...,p\} : MS_{u_k} = \lambda_{u_k}$$
- Les facteurs principaux sont donc les vecteurs propres de $MS$ de $M^{-1}$-norme 1 
- *Pour simplifier les écritures on considère que les variables $X_1,...,X_p$ sont centrées*
### Composantes principales
- Les **composantes principales** sont les variables définies par les facteurs principaux $$\forall \alpha \in \{1,...,p\} : c_{\alpha} = \sum_{j=1}^p u_{\alpha_j}x_j = X_{u_{\alpha}} \in \mathbb R^n$$
- $c_{\alpha}$ est le vecteur renfermant les coordonnées des projections $M$-orthogonales des individus sur l'axe principal $a_{\alpha}$
- Les composantes principales sont des combinaisons linéaires, non corrélées entre elles, des variables classées par ordre décroissant de variance
### Cercle de corrélation
- En **ACP normée**
- Le cercle de corrélations permet d'interpréter les axes
- La corrélation enter la $\alpha$-ème composante principale et la $j$-ème variable vaut : $$corr(C_{\alpha},X_j) = \sqrt{\lambda_\alpha}u_{\alpha j}$$
- On a :$$\sum_{j=1}^p corr^2 (C_\alpha, X_i) = \lambda_\alpha$$
- Pour visualiser les corrélations entre les composantes principales et les variables initiales, on représente chacune des variables par un vecteur de coordonnées  à l'intérieur du cercle unité, dit **cercle des corrélations**$$(corr(X_j, C_\alpha) , corr(X_j, C_\beta))$$
- on a : $$corr(X_j, C_\alpha) = \sqrt{\lambda_\alpha} u_{\alpha j}$$![[Pasted image 20251218153712.png]]
- ![[Pasted image 20251218153951.png]]
#### Choix du nombre d'axes
##### Critère de Kayser
On ne s'intéresse qu'aux axes dont les valeurs propres sont supérieures à la moyenne (qui vaut 1 en *ACP normée*)
##### Critère du coude
- Lorsque les variables sont peu corrélées, les valeurs propres de la matrice d'inertie décroissent régulièrement, et l'ACP présente alors peu d'intérêt
- A l'inverse, lorsqu'il existe une structure sur les données, on observe des ruptures dans la décroissance des valeurs propres
- On cherche alors un point d'inflexion sur l'**éboulis des valeurs propres** (*scree plot*)
#### Qualité de projection des individus

 ![[qualité_projection.gif]]
 - La qualité de projection de l'individu $i$ sur le $\alpha$-ème axe vaut : $$CO2_\alpha (i) = cos^2(\theta_i) = \frac {(c_{i \alpha})^2}{\sum_{j=1}^p (c_{ij})^2}$$
#### Contribution à l'inertie du nuage
- La **contribution à l'inertie** portée par le $\alpha$-ème axe vaut : $$CTR_\alpha (i) = \omega_i \frac {(c_{i \alpha})^2}{\lambda_\alpha}$$
	- où $c_{i \alpha}$ désigne la valeur de la $\alpha$-ème composante pour l'individu $i$
#### Eboulis des valeurs propres
![[Pasted image 20251218160723.png]]
#### Nombre des composantes
- L'inertie $\mathcal I_{tot} = 6$  se décompose ainsi sur les premiers axes :
	- $\mathcal I_1 \approx 4.42, \tau_1 \approx 73.7\%$
	- $\mathcal I_1 \approx 0.86, \tau_1 \approx 14.3\%$
- On visualise donc de façon simplifiée, mais optimale sur le premier plan factoriel : $$\tau_{1 \oplus 2} = \frac {\mathcal I_{u_1 \oplus u_2}}{\mathcal I_{tot}} \approx 87.9\%$$
#### Cercle des corrélations pour le premier plan factoriel
![[Pasted image 20251218170446.png]]
#### Projection des individus sur le premier plan factoriel
![[Pasted image 20251218170540.png]]
### Démarche
1. On **centre** le nuage de points
2. On recherche les **valeurs propres** et **vecteurs propres** de la matrice issue de la matrice de variance-covariance
3. On détermine le **nombre d'axes** à retenir à partir de l'éboulis des valeurs propres
4. On **interprète** les **composantes principales** retenues à partir du cercle des corrélations (relations entre ces composantes principale et les variables de départ)
5. On **interprète** les **projections des individus** (proximités entre eux) en tenant compte des qualités et contributions de ces individus