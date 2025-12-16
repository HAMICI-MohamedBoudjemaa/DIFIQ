Le terme anglais **Clustering** désigne la classification **non-supervisée** en Français (le terme anglais *classification*)
***Définition*** : Action de répartir en classes, en catégories, des choses, des objets, ayant des caractères communs.
*Exemple* : Astronomie, Géographie, Marketing...
*Problème* : Le nombre de partitions possible est explosif, le nombre de Bell $B_n$ donne le nombre de partitions possibles pour $n$ individus.

| n     | 4   | 6   | 10      |
| ----- | --- | --- | ------- |
| $B_n$ | 15  | 203 | 115 975 |
*Solution* : Utiliser des **Algorithmes de recherche**

# Les méthodes de clustering
- **Partitionnement hiérarchique** : CAH, CDH
- **Partitionnement non hiérarchique** : K-means, K-medoids
- **Méthodes basées sur les densités de points** : DBSCAN, OPTICS
- **Méthodes basées sur les mélanges de lois** : EM, SEM
- **Méthodes Neuronales** : Carte de Kohonen (SOM \[Self Organizing Map])
# Problème de dimension
On parle de "Fléau de la dimension" ("Curse of dimension") car les algorithmes de clustering sont difficilement utilisables en grande dimension (P grand) car les points se trouvent à la même distance de l'origine.
$$\frac {max_{i \in \{1,...,n\}||X_i||}}{min_{i \in \{1,...,n\}||X_i||}} \overset{P \rightarrow+\infty}{\longrightarrow} 1$$

*Solution* : Réduire le nombre de variables via :
- ACP
- Analyse de Fourier
- Les ondelettes
- L'"embedding" (réseaux de neurones)
- N.B. Cela n'est pas toujours nécessaire
# Normalisation
Il faut normaliser les variables **hétérogènes** (*en nature et/ou en unité*) :
	$$\tilde x_{i,j} = \frac {x_{i,j} - \bar x_j}{s_j^{'}}$$
Où :
$$\begin{aligned} 
&\bar x_j = \frac {1}{n} \sum_{i=1}^n x_{i,j}\\
& s_j^{'2} = \frac {1}{n-1} \sum_{i=1}^n (x_{i,j} - \bar x_j)^2
\end{aligned}$$
# Partition
On dit que $P = \{C_1,...,C_k\}$ est une partition de l'espace des individus $O$ si :
- $\forall k \in \{1,...,K\} : C_k \ne \emptyset$
- $\forall (k,k') \in \{1,...,K\}^2 : C_k \cap C_{k'} \ne \emptyset$
- $\cup _{k \in \{1,...,K\}} C_k = O$
Chaque élément $C_k$ de la partition est appelé **classe** ou **cluster**
Dans une partition, chaque individu appartient à une et une seule classe
Les méthodes CAH, K-means, EM et SOM construisent des partitions, contrairement à la méthode DBSCAN qui peut identifier des individus "bruits"
## Caractérisation des classes
- La description d'une classe se fait grâce aux ***variables actives*** (sur lesquelles on a souhaité différencier les classes) et grâce à toute ***variable supplémentaire***
- Variable quantitative $\implies$ Comparaison des moyennes sur les différentes classes
- Variable qualitative $\implies$ Comparaison entre la représentation de la modalité dans la classe vs reste de la population
- Recherche d'un individu représentatif (typique de la classe)
- Il est fréquent de nommer la classe par un qualificatif la caractérisant
# Dissimilarité, distance et distance ultramétrique
- Soit une métrique $d$ finie sur $O \times O$ 
	- Pour 3 individus quelconques $(i_1,i_2,i_3) \in O^3$, on considère les propriétés suivantes :
		1. $d(i_1,i_2) \ge 0$
		2. $d(i_1,i_2) = d(i_2,i_1)$
		3. $d(i_1,i_2) = 0 \implies i_1 = i_2$
		4. $d(i_1, i_2) \le d(i_1,i_3) + d(i_3,i_2)$ (inégalité triangulaire)
		5. $d(i_1,i_2) \le max\{ d(i_1,i_3), d(i_3,i_2)\}$
- Une **dissimilarité**  vérifie : $1,2,3$ 
- Une **distance**  vérifie : $1,2,3,4$
- Une **distance ultramétrique** vérifie : $1,2,3,5$
# Similarité et distances
On appelle **similarité** une fonction $s$ définie sur $O \times O$ à valeurs dans $\mathbb R^+$ telle que pour 2 individus quelconques $i_1$ et $i_2$  
- $s(i_1, i_2) = s(i_2, i_1)$
- $s(i_1, i_2) \le s(i_1, i_1) = s_{max}$
A partir d'une similarité $s$, on peut facilement construire une dissimilarité $d$, *par exemple* :
- $d(i_1, i_2) = s_{max} - s(i_1, i_2)$
## Cas des variables quantitatives
### Distance de Minkowski
$$d(i_1,i_2) = [\sum_{i=1}^p |x_{i_1 j} - x_{i_2 j}|^q]^{\frac {1}{q}}$$
### Distance de Manhattan
$$d(i_1,i_2) = \sum_{i=1}^p |x_{i_1 j} - x_{i_2 j}|$$
### Distance de Chebychev
$$d(i_1,i_2) = max |x_{i_1 j} - x_{i_2 j}|, \space avec \space {j \in \{1,...,p\}}$$


### Distance Euclidienne (Minkowski, q=2)
$$d(i_1,i_2) = [\sum_{i=1}^p |x_{i_1 j} - x_{i_2 j}|^2]^{\frac {1}{2}}$$
Ce qui donne :
$$d^2(i_1, i_2) = (x_{i_1} - x_{i_2})^\top (x_{i_1} - x_{i_2})$$
La distance $d$ est induite par la **norme** :
$$\forall x \in \mathbb R^p : ||x||^2 = x^\top x$$
Le **produit scalaire** associé à cette norme est :
$$\forall(x,y) \in \mathbb R^p \times \mathbb R^p : \space <x,y> = x^\top y$$
#### M-distances Euclidienne
==On utilise une ***Matrice M*** pour pondérer les dimensions, dans la distance euclidienne classique on utilise une pondération uniforme==
On a :
$$d^2(i_1, i_2) = (x_{i_1} - x_{i_2})^\top M(x_{i_1} - x_{i_2})$$
La distance $d$ est induite par la **norme** :
$$\begin{aligned} &\forall x \in \mathbb R^p : ||x||_M^2 = x^\top Mx \\ \\&d^2(i_1,i_2) = ||x_{i_1} - x_{i_2}||_M^2 \end{aligned}$$
Le **produit scalaire** associé à cette norme est :
$$\begin{aligned} &\forall(x,y) \in \mathbb R^p \times \mathbb R^p : \space <x,y> = x^\top My \\ \\&d^2(i_1,i_2) = ||x_{i_1} - x_{i_2}||_M^2 = <x_{i_1} - x_{i_2}, x_{i_1} - x_{i_2}>_M \end{aligned}$$
##### Distance de Sebestyen
==Ici on utilise une pondération tenant compte de l'importance relative des dimensions, sans corrélations==
On a (avec $D$ *définie positive*) :
$$d^2(i_1, i_2) = (x_{i_1} - x_{i_2})^\top D(x_{i_1} - x_{i_2})$$
On peut considérer, *par exemple*:
$$D_{\frac{1}{s^2}} = diag(\frac{1}{s_1^2},...,\frac{1}{s_p^2})$$
##### Distance de Mahalanobis
==Ici on tient compte des corrélations==
On a (avec $S$ *matrice de variance-covariance*) :
$$d^2(i_1, i_2) = (x_{i_1} - x_{i_2})^\top S(x_{i_1} - x_{i_2})$$
## Cas des variables qualitatives
- Considérons $p$ variables qualitatives $X_1,...,X_p$, avec respectivement $m_1,...,m_p$ modalités possibles
- $(a_{j_1},...,a_{jm_j})$ désignent les $m_j$ modalités de la variable $X_j$ 
- Le **tableau disjonctif complet** $D$ est défini par :
	- $D = [D_1,...,D_p]$
	- Avec $\forall j \in \{1,...,p\},\forall i \in \{1,...,n\},\forall k \in \{1,...,m_j\} : (D_j)_{ik} = \mathbb 1_{xij = a_{jk}}$ 
- La distance Euclidienne entre deux lignes du tableau disjonctif complet est égale au nombre de modalités qui diffèrent entre les deux individus
*Exemple*
Voici le tableau regroupant ces informations :

|individu|Sexe|Yeux|
|---|---|---|
|père|Masculin|Marron|
|mère|Féminin|Bleu|
|enfant|Masculin|Vert|

Le tableau disjonctif complet de cette population prend la forme suivante :

|individu|sexe F|sexe M|Yeux B|Yeux M|Yeux V|
|---|---|---|---|---|---|
|père|0|1|0|1|0|
|mère|1|0|1|0|0|
|enfant|0|1|0|0|1|
## Cas des variables binaires
- On se place dans le cas de variables binaires (valeurs dans $\{0,1\}$) pour deux individus $i_1,i_2$
- On a :
	- $a$ : nombre de caractéristiques non possédés par $i_1$ et $i_2$. 
	- $b$ : nombre de caractéristiques possédés par $i_2$ mais pas par $i_1$. 
	- $c$ : nombre de caractéristiques possédés par $i_1$ mais pas par $i_2$. 
	- $d$ : nombre de caractéristiques possédés par $i_1$ et $i_2$.

|       | <   | $i_2$ | <   |
| ----- | --- | ----- | --- |
|       | <   | 0     | 1   |
| $i_1$ | 0   | $a$   | $b$ |
| ^     | 1   | $c$   | $d$ |
### Similarité
#### Jaccard
$$s(i_1, i_2) = \frac {d}{b+c+d}$$
#### Sokal, Sneath and Anderberg
$$s(i_1, i_2) = \frac {d}{2(b+c)+d}$$
#### Czekanowski, Sorensen and Dice
$$s(i_1, i_2) = \frac {2d}{b+c+2d}$$
#### Russel and Rao
$$s(i_1, i_2) = \frac {d}{a+b+c+d}$$

#### Exemple : Nuage de points
##### Partition
![[Nuage_de_points.gif]]
##### Inertie intra-classe
![[Inertie_Intra_Classe.gif]]

# Inerties
## Poids des individus
Si les données proviennent d'un plan de sondage, il est possible d'affecter un **poids** $\omega_i$ à chaque individu $i$
Les poids vérifient :
- $\forall i \in \{1,...,n\} : \omega_i \gt 0$
- $\sum_{i=1}^n \omega_i = 1$
## Centre de gravité
Le **centre de gravité** $g$ du nuage est $$g = \sum_{i=1}^n \omega_i x_i$$
En supposant une partition des individus en $K$ classes $\{C_1,...,C_K\}$, la classe $C_k$ admets comme :
- Poids : $$\mu_k = \sum_{i \in C_k} \omega_i$$
- Centre de gravité : $$g_k = \frac {1}{\mu_k}\sum_{i \in C_k} \omega_i x_i$$
## Inerties et théorème de Huygens
On appelle **inertie par rapport à un point a** ($a \in \mathbb R^p$) la quantité :$$\mathcal I_a = \sum_{i=1}^n \omega_i d^2(i,a)$$ où $d$ désigne la *distance Euclidienne*

### Inertie Totale
$$\mathcal I_{tot} = \sum_{i=1}^n \omega_i d^2(i,g)$$

### Inertie Intra-classe
Mesure la concentration des points dans les K classes
$$\mathcal I_{intra} = \sum_{k=1}^K \sum_{i \in C_k} \omega_i d^2(i,g_k)$$

### Inertie Inter-classes
Mesure l'éloignement inter-classe des K classes
$$\mathcal I_{inter} = \sum_{k=1}^K \mu_k d^2(g_k,g)$$
### Les 3 inerties en image
![[Inerties.gif]]
### Théorème de Huygens
Il indique que :$$\mathcal I_a = \mathcal I_g + (\sum_{i=1}^n \omega_i) d^2(a,g)$$
Il nous permet d'obtenir que : $$\mathcal I_{tot} = \mathcal I_{intra} + \mathcal I_{inter}$$
### Pourquoi les inerties
L'objectif est de ***minimiser*** l'**inertie** **intra-classe** et ***maximiser*** l'**inertie** **inter-classes**.
Autrement dit, avoir des classes homogènes à l'intérieur et très hétérogènes entre elles.
Une méthode d'**évaluation d'un clustering** est : $$\frac {\mathcal I_{inter}}{\mathcal I_{tot}}$$
==On mesure la part de l'inertie inter-classes dans l'inertie totale, plus le rapport est élevé, plus l'inertie totale est expliquée par la distance entre les classes et non au sein des classes== 

# Les Algorithmes
## CAH vs K-means
- **Petits jeux de données** : 
	- CAH ou K-means.
	- CAH préalable à un K-means pour déterminer le nombre de classes
- **Gros jeux de données** :
	- ***~={red}CAH impossible=~***
	- Démarche hybride possible (réduction de dimensions via K-means + CAH pour déterminer le nombre de classes + K-means):
		- On lance un K-means sur les $n$ individus avec un petit nombre de classes ($K_1 \lt \lt n$)
		- On lance une CAH sur les $K_1$ centroïdes obtenus afin d'avoir le nombre de classes $K_2$
		- On lance un K-means sur les $n$ individus avec $K_2$ classes
## [[CAH]]
## [[K-means]]


