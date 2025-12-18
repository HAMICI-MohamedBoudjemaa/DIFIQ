# Contexte
- Il s'agit d'une généralisation de l'**AFC**
- On dispose de $p$ **variables qualitatives** $X_1,...,X_p$ avec respectivement $m_1,...,m_p$ modalités, observées sur $n$ individus
# Tableau disjonctif complet
- On appelle **tableau disjonctif complet** la matrice $D$ constituée des $m_1+...+m_p$ indicatrices pour chacune des modalités des $p$ variables :$$D = [D_1,...,D_p]$$
- avec :$$\forall i \in \{1,...,n\}, \forall j \in \{1,...,p\}, \forall k \in \{1,...,m_j\} : [D_j]_{i,k} = \mathbb 1_{x_{ij} = a_{jk}}$$
	- où $(a_{j1},...,a_{jm_j})$ désignent les $m_j$ modalités de la variable $X_j$
# Tableau de Burt
- On appelle **tableau de Burt** la matrice $B$ suivante : $$B = D^\top D$$
- Il s'agit d'une généralisation du tableau de contingence
# Lien entre ACM, AFC et ACP
- Une **ACP** sur le tableau disjonctif complet fournit les axes de l'**ACM**
- Une **AFC** sur le *tableau de Burt* fournit les axes de l'**ACM**
