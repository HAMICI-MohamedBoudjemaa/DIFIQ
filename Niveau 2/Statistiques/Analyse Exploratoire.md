Il faut imaginer nos données d'apprentissages disposées dans un tableau comme suit :
![[Pasted image 20251202162548.png]]

## Poids et centre de gravité
- On peut attribuer à chaque individu un **poids $\omega_i$** 
	- $\forall i \in \{1,..,n\} : \omega_i \gt 0$   
	- $\sum_{i=1}^n \omega_i = 1$
- Matriciellement on peut écrire :
	- $W = diag(\omega_1,...,\omega_n)$
- On considère très souvent des poids uniformes :
	- $\forall i \in \{1,..,n\} : \omega_i = \frac {1}{n}$
	- Ou $W = \frac {1}{n} I_n$
- Le centre de gravité du nuage est :
	- $g = X^T W1_n = \sum_{i=1}^n \omega_i x_i$
	- où $1_n = (1,...,1)^T \in \mathbb R^n$
# Clustering vs ACP
- On utilise des techniques de **classification non-supervisée** (***clustering***) afin de réduire la dimension des individus
- On utilise des techniques d'**analyse factorielle** (***dimension reduction*** in English) pour réduire la dimension des variables et/ou analyser les données géométriquement

# [[Clustering]]
# [[Analyse Factorielle]]
