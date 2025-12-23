# Introduction et cas d'étude
Le terme *regression* vient des travaux de **Francis Galton** (dans le sens, ***regression vers la moyenne***)
C'est le modèle linéaire le plus utilisé.
Le but est de mettre en relation une ***variable quantitative à expliquer*** (nommée *label, étiquette, output*), avec des ***variables explicatives*** (nommées *covariables, features, prédicteurs, inputs*)
## Cas d'étude 1
Étude du lien entre *le pic d'ozone journalier* et des *facteurs potentiellement explicatifs* à des fins de *prévision*
On dispose de 112 données (recueillies à Rennes) et 14 variables (principalement météorologiques)
- Date : Date 
- maxO3 : Teneur maximale en ozone observée dans la journée
- T9, T12, T15 : Température à 9h, 12h, 15h
- Ne9, Ne12, Ne15 : Nébulosité observée à 9h, 12h, 15h
- Vx9, Vx12, Vx15 : Composante Est-Ouest du vent à 9h, 12h, 15h
- maxO3v : Teneur maximale en ozone observée la veille
- vent : Orientation du vent à 12h
- pluie : Occurrence ou non de précipitations
![[Pasted image 20251211204931.png]]
# Régression linéaire simple
## Modèle
### Hypothèses
- On note **Y** la variable à expliquer
- On note **X** la covariable 
- Le modèle de ***régression linéaire simple*** s'écrit :
	- $Y = \beta_0 + \beta_1 X + \epsilon$
	- Où :
		- $\beta_0 \space et \space \beta_1$ sont des paramètres inconnus (non observables)
		- $\epsilon$ est l'erreur du modèle, est centrée (d'espérance nulle) et de variance $\sigma^2$ 
- Dans le cas où $X = 0 \implies Y = 0$ on a :
	- $Y = \beta_1 X + \epsilon$
### L'échantillon
- Soient $(x_i, y_i)_{i \in \{1,...,n\}}$ $n$ observations de $(X, Y)$ : $$\forall i \in \{1,...,n\} : y_i = \beta_0 + \beta_1 x_i + \epsilon_i$$
- $(y_i)_{i \in \{1,...,n\}}$ sont **~={yellow}aléatoires=~**
- $(x_i)_{i \in \{1,...,n\}}$ sont **~={yellow}déterministes=~** (on peut également les considérer aléatoires dans certains cas)
- $(\epsilon_i)_{i \in \{1,...,n\}}$ sont **~={yellow}centrés, non corrélés et de variance $\sigma^2$ =~**
### Illustration
![[RegressionLineaireSimple.gif]]
### Problème des MCO
- On appelle **estimateur des moindres carrés ordinaires - MCO** (*Ordinary Least Squares - OLS*) de $\beta_0$ et $\beta_1$ les réels $\hat \beta_0$ et $\hat \beta_1$ minimisant le critère (*des moindres carrés*) $$S(\beta_0, \beta_1) = \sum_{i=1}^n (y_i - \beta_0 -\beta_1 x_i)^2$$
	- On écrit : $$(\hat \beta_0, \hat \beta_1) = arg \space \underset {\beta_0, \beta_1}{min} \space S(\beta_0, \beta_1)$$
- Il faut ensuite estimer $\sigma^2$ 
#### Remarque
- La distance minimisée n'est pas celle du point à la droite de régression :
![[Pasted image 20251221190126.png]]
- Au-delà de la pertinence du problème, cela induit la non symétrie entre la droite de régression de $Y$ sur $X$ et celle de $X$ sur $Y$
#### Alternative
- On aurait pu utiliser une autre distance $$S^*(\beta_0, \beta_1) = \sum_{i=1}^n |y_i - \beta_0 -\beta_1 x_i|$$
- Cette distance conduit à une solution plus robuste (*moins sensible aux outliers*) mais est moins aisée à manipuler que le problème des **MCO**
#### Solution des MCO
- On suppose que les $(x_i)_{i \in \{1,...,n\}}$ ne sont pas tous identiques (non colinéarité)
- Les estimateurs des **MCP** de $(\beta_0, \beta_1)$ sont :
	- $$\hat \beta_1 = \frac {s_{XY}}{s_X^2}$$
		- où :
			- $$s_{XY} = \frac {1}{n} \sum_{i=1}^n x_i y_i - \bar x \bar y$$
			- $$s_X^2 = \frac {1}{n} \sum_{i=1}^n x_i^2 - \bar x^2$$
	- $$\hat \beta_0 = \bar y - \hat \beta_1 \bar x$$
	- ~={yellow} $\bar x$ : moyenne de x
	-  $\bar y$ : moyenne de y=~
#### Valeur ajustée et résidus
- On appelle **valeurs ajustées** les quantités : $$\forall i \in \{1,...,n\} : \hat y = \hat \beta_0 + \hat \beta_1 x_i$$
- On a : $$\bar {\hat y} = \bar y$$
- On appelle **résidus** les estimations des erreurs : $$\forall i \in \{1,...,n\} : e_i : y_i - \hat y_i$$
- On a : $$\bar e = 0$$
#### Droite de régression estimée
![[Pasted image 20251221210853.png]]
#### Estimateur de la variance des erreurs
On considère comme estimateur de $_sigma^2$ la **variance résiduelle** $$\hat \sigma^2  = \frac {1}{n-2} \sum_{i=1}^n e_i^2$$
#### Propriétés
- Les paramètres estimés sont dotés de bonnes propriétés
- Ils sont :
	- Consistants
	- Sans biais
	- "~={yellow}BLUE=~" : **~={yellow}B=~est ~={yellow}L=~inear ~={yellow}U=~nbiased ~={yellow}E=~stimator**
## Coefficient de détermination
### Idée
- L'intérêt d'un modèle de régression linéaire est de pouvoir expliquer une partie des variations de la variable $Y$ par les variations de la variable $X$
- On a : $$y_i - \bar y = \hat y_i - \bar y + y_i - \hat y_i$$
	- où : 
		- $\hat y_i - \bar y$ est la variation expliquée (*restituée*) par le modèle
		- $y_i - \hat y_i$ est la variation non expliquée par le modèle
- On peut démontrer la formule de décomposition de la variance
### Décomposition de la variance (*ANOVA*)
- La formule d'***ANOVA*** (ANalysis Of VAriance) est : $$\begin{aligned}
&SCT &= &SCE &+ &SCR \\
&{\sum_{i=1}^n(y_i - \bar y)^2} &= &{\sum_{i=1}^n(\hat y_i - \bar y)^2} &+ &{\sum_{i=1}^n(y_i - \hat y_i)^2}
\end{aligned}$$
- **SCT** (*Somme des Carrés Totale*) traduit la variance totale
- **SCE** (*Somme des Carrés Expliquée*) traduit la variance expliquée par le modèle
- **SCR** (*Somme des Carrés Résiduelle*) traduit la variance inexpliquée par le modèle
### Définition
- Le **coeffivient de détermination** noté $R^2$, vaut : $$R^2 = \frac {SCE}{SCT}$$
	- $R^2 = 1 \iff SCE = SCT \iff$ Toute la variance est expliquée
	- $R^2 = 0 \iff SCR = SCT \iff$ Aucune variance n'est expliquée
- On a : $$R^2 \in [0,1]$$
- Dans le cas de la ~={yellow}**régression linéaire (et non multiple)**=~ simple avec constante, on peut également montrer que $$R^2 = r_{x,y}^2$$
### Limites
La relation entre $R^2$ et le lien linéaire n'est pas une équivalence
- Bon ajustement linéaire $\implies R^2 = 1$ (d'où : $R^2 = 0 \implies$ mauvais ajustement linéaire)
- $R^2 = 1 \enclose{updiagonalstrike}{\implies}$ Bon ajustement linéaire (et $R^2 = 0 \enclose {updiagonalstrike}{\implies}$ aucune relation entre les variables)
![[Pasted image 20251221214238.png]]

## Prévision
A partir d'une observation $x_k, (k \enclose{updiagonalstrike}{\in} \{1,...,n\})$ \[$k$ n'étant pas dans l'échantillon d'ajustement] la **prévision** (*ou valeur prédite*) $\hat y_k^{(p)}$ la quantité suivante : $$\hat y_k^{(p)} = \hat \beta_0 + \hat \beta_1 x_k$$
C'est la valeur prédite du point $y_k$ $$y_k = \beta_0 + \beta_1 x_k + \epsilon_k$$
On parle ici de **prévision** et non d'**ajustement** car le point $(x_k, y_k)$ n'a pas servi à l'estimation des paramètres $\beta_0$ et $\beta_1$
### Erreur de prévision
- On appelle **erreur de prévision** la quantité :$$e_k^{(p)} = y_k - \hat y_k^{(p)}$$
- L'erreur de prévision admet comme espérance : $$\mathbb E(e_k^{(p)}) = 0$$
- Et comme variance :$$var(e_k^{(p)}) = \sigma^2(1+\frac {1}{n}+\frac {(x_k - \bar x)^2}{\sum_{i=1}^n (x_i - \bar x)^2})$$
## Modèle linéaire gaussien simple
- Afin de pouvoir déterminer des intervalles de confiance sur les paramètres $\beta_0$ et $\beta_1$ ainsi que leur significativité, une hypothèse supplémentaire est nécessaire sur la loi de l'erreur ~={red} $\epsilon$ =~ et donc sur celle de la variable à expliquer $Y$
- Le **~={yellow}modèle linéaire gaussien simple=~** considère l'hypothèse d'une **~={yellow}distribution normale=~ de l'~={red}erreur=~**
- On en déduit **la loi** des *estimateurs des MCO* $(\hat \beta_0, \hat \beta_1)$ qui permet d'établir des **tests** et **intervalles de confiance** sur les *paramètres* $(\beta_0, \beta_1)$
### Hypothèse
$$\begin{aligned}
&\epsilon &\sim \space &\mathcal N(0, \sigma^2) \\
L'échantillon \space &(\epsilon_i)_{i \in \{1,...,n\}} &\sim \space &\mathcal N(0, \sigma^2)
\end{aligned}$$
### Test de significativité sur $\beta_0$ et $\beta_1$
- Pour $j \in \{0,1\}$, on effectue le **test de Student** $$\begin{aligned}
\begin{cases}
&H_0 : \beta_j = 0 \\
&H_1 : \beta_j \ne 0
\end{cases}
\end{aligned}$$
- En pratique, on ne teste pas la constante si elle figure dans le modèle
- On considère la statistique de test : $$T_j = \frac {\hat \beta_j}{\hat \sigma_{\hat \beta_j}}$$ Qui converge vers la loi $T(n-2)$ sous $H_0$
- On rejette $H_0$ au niveau de test $\alpha$ si :$$|t_j| \gt t_{n-2,1-\frac {\alpha}{2}}$$
- En pratique, on analyse les **p-valeurs**
## Retour au cas d'étude
![[CasEtude1.gif]]
# Régression linéaire multiple
## Modèle
### Hypothèses
- Soit $Y$ la **variable à expliquer**
- Soient $(X_1,...,X_p)$ les **covariables** (ou variables explicatives ou *features*)
- Le modèle de **régression linéaire multiple** s'écrit : $$Y = \beta_0 + \beta_1 X_1 + \beta_2 X_2 +...+ \beta_p X_p + \epsilon$$ où
	-  $(\beta_0, \beta_1,...,\beta_p)$ sont des paramètres inconnus (non observables)
	- ~={red} $\epsilon$ =~, l'~={red}erreur du modèle=~, centrée \[ $\mathbb E = 0$ ] et de variance $\sigma^2$
### L'échantillon
- Soient $(x_{i,1},...,x_{i,p},y_i)_{i \in \{1,...,n\}}$, $n$ observations de $(X_1,...,X_p,Y)$ : $$\forall i \in \{1,...,n\} : y_i = \beta_0 + \beta_1 x_{i,1} +...+ \beta_p x_{i,p} + \epsilon_i$$
- $(y_i)_{i \in \{1,...,n\}}$ sont **aléatoires**
- $(x_{i,j})_{i \in \{1,...,n\}, j \in \{1,...,p\}}$ sont **déterministes** (*on peut également les considérer aléatoires dans certains cas*)
- $(\epsilon_i)_{i \in \{1,...,n\}}$ sont centrés, non corrélés et de variance $\sigma^2$
### Ecriture matricielle
On a $$
\left(\begin{matrix} y_1\\.\\.\\.\\y_n \end{matrix}\right) =
\left[\begin{matrix} 1 &x_{1,1} &{...} &x_{1,p}\\.&. &. &.\\. &x_{i,1} &{...} &x_{i,p}\\. &. &. &.\\1 &x_{n,1} &. &x_{n,p} \end{matrix}\right]
\left(\begin{matrix} \beta_0\\.\\.\\.\\\beta_p \end{matrix}\right) +
\left(\begin{matrix} \epsilon_1\\.\\.\\.\\\epsilon_n \end{matrix}\right)$$
On utilise les notations suivantes : $$y = X \beta + \epsilon$$
### Linéarisation de modèles de regression
On peut faire du **feature engineering** :
- En transformant les *~={orange}covariables=~* $(X_1,...,X_p)$ \[via des opérations comme des puissances, exponentielle, logarithme...] et en considérant cette transformation comme *~={orange}covariable=~*
#### Estimateur des MCO
- Comme vu sur le modèle linaire simple, on appelle **estimateurs des moindres carrés ordinaires (MCO)** de $\beta_0, \beta_1,..., \beta_p$ les valeurs $\hat \beta_0, \hat \beta_1,..., \hat \beta_p$ **~={yellow}minimisant=~** la somme des moindres carrés des résidus : $$S(\beta_0, \beta_1,..., \beta_p) = \sum_{i=1}^n (y_i - \beta_0 - \beta_1 x_{i,1} - ... -\beta_p x_{i,p})^2$$
- Si les $p$ colonnes de $X$ ne sont pas colinéaires alors l'estimateur des **MCO** de $\beta$ vaut : $$\hat \beta = (X^\top X)^{-1}X^\top y$$
#### Valeurs ajustées
- On appelle **valeurs ajustées** les quantités : $$\forall i \in \{1,...,n\} : \hat y_i = \hat \beta_0 + \hat \beta_1 x_{i,1}+...+\hat \beta_p x_{i,p}$$
- On a : $$\bar {\hat y} = \bar y$$
- On peut écrire vectoriellement : $$\hat y = X \hat \beta$$
#### Résidus
- On appelle **résidus** les estimations des erreurs : $$\forall i \in \{1,...,n\} : e_i = y_i - \hat y_i$$
- On a : $$\bar e = 0$$
- On peut écrire vectoriellement : $$e = y - \hat y$$
- On considère comme estimateur de $\sigma^2$ la **variance résiduelle** : $$\hat \sigma^2 = \frac {1}{n-(p+1)} \sum_{i=1}^n e_i^2$$  
#### Propriétés
Les paramètres sont :
- Consistants
- Sans biais
- "~={yellow}BLUE=~" : **~={yellow}B=~est ~={yellow}L=~inear ~={yellow}U=~nbiased ~={yellow}E=~stimator**
#### Cas des covariables qualitatives
- Dans le cas d'une **covariable qualitative** $X_j$ avec $m$ modalités, on peut considérer un modèle avec $m$ indicatrices (*dummy variables*) : $$\mathbb 1_{X_j = 1},...,1_{X_j = m}$$
- Le modèle est indéterminé si on considère en sus la constante dans le modèle, on doit alors poser une contrainte du type :
	- $\beta_{j_1} = 0$
	- $\sum_{k=1}^n \beta_{j_k} = 1$
	- où $\beta_{j_k}$ désigne le coefficient devant $\mathbb 1_{x_j = k}$ 

## Interprétation géométrique
- $\hat Y$ est la projection orthogonale de $Y$ sous le sous espace vectoriel engendré par les colonnes de $X$ : $$sp\{1_n,x_1,...,x_p\}, \space avec \space 1_n = (1,...,1)^\top \in \mathbb R^n$$ ==ici $sp$  veut dire "span : sous espace vectoriel engendré" et non "spectre"==
- La matrice de projection sur cet espace, communément notée $H$ (pour "*hat*") dans le cadre des modèles linéaires, vaut : $$H = X(X^\top X)^{-1}X^\top$$
- On a bien :$$\hat y = X \hat \beta = X(X^\top X)^{-1}X^\top y = Hy$$
![[Pasted image 20251222090300.png]]
## Coefficient de détermination 
### [[#Décomposition de la variance (*ANOVA*)]]
Exactement la même définition et limites que pour le modèle linéaire vu plus haut \[*cliquer sur lien*]
#### Cas de la régression sans constante
Dans le cas où $\beta_0 = 0$, il existe une autre formule de **décomposition de la variance** :$$\sum_{i=1}^n y_i^2 = \sum_{i=1}^n \hat y_i^2 + \sum_{i=1}^n (y_i - \hat y_i)^2$$
- ==On ne peut donc plus interpréter le coefficient de détermination $R^2$ ==
#### Coefficient de détermination ajusté
- Plus on ajoute de covariables, plus le coefficient de détermination croît
- Le coefficient de détermination ajusté tient compte du nombre de covariables :$$R_{ajusté}^2 = 1 - \frac {n-1}{n-(p+1)} (1-R^2)$$
- L'utilisation de ce coefficient de détermination ajusté ne prémunit pas contre le sur-apprentissage
## Prévision
- A partir d'une nouvelle observation $(x_{k,1},...,x_{k,p}), avec \space k \enclose{updiagonalstrike}{\in} \{1,...,n\}$, on appelle **prévision (ou valeur prédite)** la quantité suivante : $$\hat y_k^{(p)} = \hat \beta_0 + \hat \beta_1 x_{k,1} +...+ \hat \beta_p x_{k,p} = (1,x_{k,1},...,x_{k,p}) \hat \beta = x_k^\top \hat \beta$$
- Il s'agit de la prévision de : $$y_k = \beta_0 + \beta_1 x_{k,1} +...+ \beta_p x_{k,p} + \epsilon_k$$
- On parle ici de prévision et non d'ajustement car l'observation $(x_{k,1},...,x_{k,p},y_k)$ n'a pas servi à l'ajustement des paramètres $(\beta_0,...,\beta_p)$ 
### Erreur de prévision
- On appelle **erreur de prévision** la quantité : $$e_k^{(p)} = y_k - \hat y_k^{(p)}$$
- L'erreur de prévision admet comme espérance : $$\mathbb E(e_k^{(p)}) = 0$$ et comme variance $$var(e_k^{(p)}) = \sigma^2 [1+x_k^\top (X^\top X)^{-1}x_k]$$
## Modèle linéaire gaussien multiple
- Sans hypothèse supplémentaire, on ne peut pas déterminer d'intervalles de confiance sur les paramètres $\beta_0,...,\beta_p$ 
- On ajoute donc une hypothèse sur l'erreur $\epsilon$ et donc sur la variable à expliquer $Y$
- Le modèle linéaire gaussien multiple considère la normalité de l'erreur
- On en déduit la loi des estimateurs des CO qui permet d'établir tests et intervalles de confiance su les paramètres
### Hypothèse
On ajoute aux hypothèses du modèle linéaire multiple : $$\epsilon \sim \mathcal N(0, \sigma^2)$$
### Test de validité globale du modèle
- Dans le cas de la régression avec constante $(\beta_0 \ne 0)$, on effectue le **test de Fisher** :$$\begin{aligned}
\begin{cases}
&H_0 : \beta_0 = \dots = \beta_p = 0 \\
&H_1 : \exists j \in \{0,\dots,p\} | \beta_j \ne 0 
\end{cases}
\end{aligned}$$
- La statistique de test utilisée est : $$F = \frac {n-(p+1)}{p} \frac {SCE}{SCR} = \frac {n-(p+1)}{p} \frac {R^2}{1-R^2} = $$
- On rejette $H_0$ au niveau de test $\alpha$ si : $$f \gt f_{(p, n-(p+1)), 1-\alpha}$$ou $f_{(p, n-(p+1)), 1-\alpha}$ désigne le quantile d'ordre $1 - \alpha$ de la **loi de Fisher** à $(p, n-(p+1))$ degrés de liberté $\mathcal F(p, n-(p+1))$.

- On lit directement la $p-valeur$ dans les sorties logiciels ==elle indique la probabilité que les résultats soient dus au pur hasard==
### Tableau d'analyse de la variance
- On considère les notations suivantes (~={yellow}CM : Carrés Moyens=~): $$\begin{aligned}
&CME = \frac {SCE}{p} \\
&CMR = \frac {SCR}{n-(p+1)}
\end{aligned}$$
- Le tableau d'analyse de la variance est une synthèse du test de validité globale :

| Source                      | Degrés de liberté | Somme des Carrés | CM    | F                  | p-valeur                                    |
| --------------------------- | ----------------- | ---------------- | ----- | ------------------ | ------------------------------------------- |
| $E$ \[~={green}expliquée=~] | $p$               | $SCE$            | $CME$ | $\frac {CME}{CMR}$ | $\mathbb P(\mathcal F(p, n - (p+1)) \gt f)$ |
| $R$ \[~={red}résiduelle=~]  | $n-(p+1)$         | $SCR$            | $CMR$ |                    | <                                           |
| $T$ \[~={yellow}Totale=~]   | $n-1$             | $SCT$            |       | <                  | <                                           |
### A propos du test de Fisher
- Le test de Fisher peut être utilisé pour comparer deux modèles emboîtés
- On test alors la nullité simultanée des paramètres différenciant les deux modèles
### Test de significativité sur un des $\beta_j$
- Pour $j  \in \{0,...,p\}$, on effectue le **test de Student** $$\begin{aligned}
\begin{cases}
&H_0 : \beta_j =  0 \\
&H_1 : \beta_j \ne 0 
\end{cases}
\end{aligned}$$
- En pratique, il n'est pas utile de tester la constante (pas de risque de sur-apprentissage)
- On considère la statistique de test : $$T_j = \frac {\hat \beta_j}{\hat \sigma \sqrt{(X^\top X)_{jj}^{-1}}}$$ qui converge vers la loi $\mathcal T (n-(p+1))$ sous $H_0$
- On rejette $H_0$ au niveau de test $\alpha$ si : $$|t_j| \gt t_{n-(p+1), 1-\frac {\alpha}{2}}$$
- On lit directement les $p-valeurs$ dans les sorties logiciels
## Retour au cas d'étude
![[CasEtude2.gif]]
# Sélection de modèles
## Principe 
- On cherche à déterminer le modèle optimal avec les $k$ covariables les plus adaptées parmi les $p$ de départ
- Il existe $\left( \begin{matrix}p \\ k\end{matrix} \right)$ modèles avec $k$ covariables parmi les $p$ envisagés
- Il existe $2^P$ sous-modèles possibles au total avec $p$ covariables
- On considère un algorithme de recherche automatique faisant appel à un test de Fisher ou un critère de choix (ex : $AIC, BIC, C_p$)
## Critères d'information
- Pour un modèle $M_k$ à $k$ covariables, les critères issus de l'**information de Kullback** sont un compromis entre l'ajustement du modèle (capté par $\hat \sigma_{M_k}^2$) et la parcimonie du modèle ($k$ figure dans ces critères)
- Le critère d'Akaike ($AIC$ : Akaike Information Criterium) $$AIC(M_k) = n \space ln(\hat \sigma_{M_k}^2) + 2k$$
- Le critère de Schwarz ($BIC$ : Bayesian Information Criterium, également noté $SBC$ : Schwarz Bayesian Criterium)$$BIC(M_k) = n \space ln(\hat \sigma_{M_k}^2) + k \space ln(n)$$
- Le critère $BIC$ peut conduire à des modèles plus parcimonieux que l'$AIC$ ($ln(n) \gt 2$ dès que $n \gt 7$)
## Statistique de Mallows
- La statistique de Mallows $C_p$ pour un modèle $M_k$ à $k$ covariables est définie par : $$C_p(M_k) = \frac {SCR(M_k)}{\hat \sigma^2} - n + 2k$$ où $\hat \sigma^2$ est la variance du modèle complet (avec $p$ covariables)
- Si un sous-modèle à $k$ variables explicatives possède un pouvoir prédictif proche de celui du modèle complet, au sens de l'erreur quadratique moyenne, alors $C_p(M_k) \le k$ 
## Procédure ascendante ou forward
- On initialise la procédure avec le modèle intégrant uniquement la constante (~={yellow}modèle "**nul**"=~)
- Si on utilise un test de Fisher :
	- A chaque itération on incorpore la covariable pour laquelle la $p-valeur$ dans le test de Fisher entre les deux modèles emboîtés est la plus faible
	- On arrête lorsque toutes les covariables sont intégrées ou lorsque la $p-valeur$ est supérieure à un seuil choisi
- Si on utilise un critère de choix (ex : $AIC, BIC, C_p$) :
	- A chaque itération on incorpore la covariable la plus favorable au sens du critère de choix
	- On arrête lorsque toutes les covariables sont intégrées ou lorsqu'on ne parvient plus à optimiser le critère de choix
## Procédure descendante ou backward
- On initialise la procédure avec le modèle intégrant toutes les covariables (~={yellow}modèle "**complet**"=~)
- Si on utilise un test de Fisher :
	- A chaque itération on retire la covariable pour laquelle la $p-valeur$ dans le test de Fisher entre les deux modèles emboîtés est la plus grande
	- On arrête lorsque toutes les covariables sont retirées ou lorsque la $p-valeur$ est inférieure à un seuil choisi
- Si on utilise un critère de choix (ex : $AIC, BIC, C_p$):
	- A chaque itération on retire la covariable la moins favorable au sens du critère de choix
	- On arrête lorsque toutes les covariables sont retirées ou lorsqu'on ne parvient plus à optimiser le critère de choix
## Procédure pas à pas ou stepwise
- Cette méthode est une procédure de sélection de type forward avec possibilité de retirer éventuellement des covariables devenues non-significatives (dans une étape backward)
# Qualité prédictive d'un modèle
## Complexité du modèle et erreur de prévision
### Impact de la complexité : Exemple
- On considère le modèle de régression suivante : $$\forall x \in [0,1] : y = cos \left( \frac {3 \pi x}{2} \right) + \epsilon$$ où $\epsilon \sim \mathcal N(0,0.1^2)$
- On simule :
	- $n_{train}$ = 30 observations $(x_i, y_i)_{i=1,...,n_{train}}$ à partir desquelles on estime cette fonction de régression par régression linéaire polynomiale de degré $d \in \{1,...,11\}$; on obtient les valeurs ajustées $(\hat y_i)_{i=1,...,n_{train}}$ 
	- $n_{test}$ = 8 observations $(x_i, y_i)_{i=1,...,n_{test}}$, non utilisées pour l'apprentissage (l'estimation) du modèle, pour lesquelles on obtient les prévisions $(\hat y_i^{(p)})_{i=1,...,n_{test}}$ qu'on compare aux réalisations $(y_i)_{i=1,...,n_{test}}$ 
- On évalue la qualité :
	- De l'**~={yellow}ajustement=~** par le $RMSE$ (**Root Mean Squared Error**) sur l'échantillon d'apprentissage : $$RMSE_{train} = \sqrt{\frac {1}{n_{train}} \sum_{i=1}^{n_{train}} (\hat y_i - y_i)^2}$$
	- De la **~={green}prévision=~** par le $RMSE$ sur l'échantillon de test :$$RMSE_{test} = \sqrt{\frac {1}{n_{test}} \sum_{i=1}^{n_{test}} (\hat y_i^{(p)} - y_i)^2}$$
![[Impact Complexité.gif]]
### Complexité et erreur de prédiction
![[Complexité Erreur.gif]]
## Découpage apprentissage-test
![[Decoupage apprentissage test.gif]]
## Critères de performance
### Prévision
- On procède de la manière suivante :
	- On estime un modèle sur l'échantillon d'apprentissage
	- On utilise ce modèle estimé pour calculer les prévisions $\hat y_i^{(p)}$ sur l'échantillon test
- Concernant les critères d'erreur :
	- S'il existe de nombreux critères possibles, il faut choisir celui (ceux) qui répondent au mieux à la problématique métier
	- Les écarts quadratiques sont classiquement utilisés à l'aide des $RMSE$ et $nRMSE$ (ils correspondent souvent au critère qui a été optimisé)
	- On peut utiliser des écarts absolus à l'aide du MAE ou absolus relatifs à l'aide du $MAPE$ (à éviter si Y prend des valeurs proches de 0)
### MSE, RMSE, nRMSE
- Le $MSE$ (**Mean Squared Error** : *erreur quadratique moyenne*) vaut : $$MSE = \frac {1}{n_{test}} \sum_{i=1}^{n_{test}}(\hat y_i^{(p)} - y_i)^2$$
- Le $RMSE$ (**Root Mean Squared Error** : *racine carrée de l'erreur quadratique moyenne*) vaut :$$RMSE = \sqrt {\frac {1}{n_{test}} \sum_{i=1}^{n_{test}}(\hat y_i^{(p)} - y_i)^2}$$
- Le $nRMSE$ (**normalized $RMSE$** : *$RMSE$ normalisé*) vaut :$$nRMSE = \frac {RMSE}{\frac {1}{n_{test}} \sum_{i=1}^{n_{test}}\hat y_i^{(p)}}$$
### MAE et MAPE
- Le $MAE$ (**Mean Absolute Error** : *erreur absolue moyenne*) vaut : $$MAE = \frac {1}{n_{test}} \sum_{i=1}^{n_{test}}|\hat y_i^{(p)} - y_i|$$
- Le $MAPE$ (**Mean Absolute Percent Error** : *erreur absolue moyenne relative*) vaut :$$MAPE = \frac {1}{n_{test}} \sum_{i=1}^{n_{test}}|\frac {\hat y_i^{(p)} - y_i}{y_i}| \times 100$$
## Validation croisée
### Principe de la validation croisée
1. Diviser aléatoirement les données en $K$ blocs (égaux ou équivalents)
   Le bloc $k$ contient $n_k$ individus : $n_k = \frac {n}{K}$ si $n$ est un multiple de $K$
2. Pour $k \in \{1,...,K\}$ :
	1. Retirer le bloc $k$ de la base d'apprentissage
	2. Estimer la fonction de prévision sur la base d'apprentissage
	3. Calculerr un critèer d'erreur de prévision sur le bloc $k : CV_k$ (ex : $RMSE$ pour la régression) 
3. Calculer le critère de validation croisée : $$CV = \sum_{k=1}^K \frac {n_k}{n} CV_k$$
### De l'échantillon aux blocs
![[EchantillonsVsBlocs.gif]]
### Remarques
- Usuellement : $K = 5$ ou $K = 10$
- Lorsque $K = n$ : on parle d'estimateur **~={yellow}"leave one out" (LOO)=~**
## Retour au cas d'étude
![[Pasted image 20251222153534.png]]
# Liens utiles
https://www.youtube.com/watch?v=0Qb6mGozOVw