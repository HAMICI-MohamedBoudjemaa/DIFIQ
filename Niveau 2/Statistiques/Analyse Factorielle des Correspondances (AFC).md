## Contexte
- On dispose de 2 **variables qualitatives** $X_1$ et $X_2$, avec respectivement $m_1$ et $m_2$ modalités, observées sur $n$ *individus*
- pour $i \in \{1,...,m_1\} et j \in \{1,...,m_2\}$ on note $n_{ij}$ le nombre d'individus ayant comme modalité $i$ pour la variable $X_1$ et $j$ pour la variable $X_2$
- On peut représenter cet ensemble de données dans le **tableau de contingence** $N$ à $m_1$ lignes et $m_2$ colonnes, de terme $n_{ij}$
### Tableau de contingence
- On peut en déduier la férquence conjointe associée :$$f_{ij} = \frac {n_{ij}}{n}$$
- On utilise les notations suivantes :$$\begin{aligned}
& \sum_{i=1}^{m_1}n_{ij} = n_{.j}, \\
& \sum_{j=1}^{m_2}n_{ij} = n_{i.}, \\
& \sum_{i=1}^{m_1}f_{ij} = f_{.j}, \\
& \sum_{j=1}^{m_2}f_{ij} = f_{i.}, \\
\end{aligned}$$
### Profil lignes
- Afin de comparer les lignes entre elles, on divise chaque ligne par la somme de la ligne
- On travaille donc sur les quantités  : $$\frac {n_{ij}}{n_{i.}}$$
- Chaque point $i$ a pour coordonnées $\frac {n_{ij}}{n_{i.}}$ pour $j \in \{1,...,m_2\}$ avec $n_{i..}$ comme poids
- Le centre de gravité des points est donc $(f_1,...,f_{m_2})^\top$ 
### Profil colonnes
- Afin de comparer les colonnes entre elles, on divise chaque colonne par la somme de la colonne
- On travaille donc sur les quantités :$$\frac {n_{ij}}{n_{.j}}$$
- Chaque point $j$ a pour coordonnées $\frac {n_{ij}}{n_{.j}}$ pour $i \in \{1,...,m_1\}$ avec $n_{.j}$ comme poids
- Le centre de gravité des points est donc $(f_1,...,f_{m_1})^\top$ 
### Métrique du Khi-Deux
- Pour deux individus $i$ et $i'$ :$$d^2(i, i') = n \sum_{j=1}^{m_2} \frac {1}{n_{.j}} (\frac {n_{ij}}{n_{i.}} - \frac {n_{i'j}}{n_{i'.}})^2$$
- Pour deux variables $j$ et $j'$ : $$d^2(j,j') = n \sum_{i=1}^{m_1} \frac {1}{n_{i.}} (\frac {n_{ij}}{n_{.j}} - \frac {n_{ij'}}{n_{.j'}})^2$$
### AFC et ACP
- Soient : $$\begin{aligned}
&D1 = diag(n_1,...,n_{m_1}) \\
&D2 = diag(n_1,...,n_{m_2})
\end{aligned}$$
- On peut alors de manière duale, effectuer une **ACP** :
	- Sur les profils lignes
		- Tableau de données considéré : $X = D_1^{-1}N$
		- Poids considérés : $W = \frac {1}{n} D_1$
		- Métrique considérée :$M = nD_2^{-1}$
	- Sur les profils colonnes
		- Tableau de données considéré : $X = D_2^{-1}N^\top$
		- Poids considérés : $W = \frac {1}{n} D_2$
		- Métrique considérée :$M = nD_1^{-1}$
### Résultat
- On peut **superposer les deux nuages projetés**, centrés sur le centre de gravité
- On s'intéresse essentiellement aux points ayant une forte contribution relative, étant donné que la contribution mesure la proximité entre les points et les axes
- On pourra observer que :
	- Deux modalités de la même variable sont proches si leurs profils sont similaires
	- Deux modalités de deux variables différentes sont proches si leurs individus respectifs ont des centres de gravité proches