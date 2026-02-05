# Introduction et cas d'étude
## Cas d'étude
On considère des données médicales de 462 patients mâles dans une région à risque élevé de maladies cardiaques du Cap-Occidental en Afrique du Sud.
On dispose de 10 variables :
- **~={green}sbp=~** : tension artérielle systolique
- **~={green}tobacco=~** : tabaccumulé (en kg)
- **~={green}ldl=~** : cholestérol de lipoprotéine de faible densité
- **~={green}adiposity=~** : adiposité (autre indicateur de l'obesité)
- **~={green}famhist=~** : antécédents familiaux ("Absent" ou "Present")
- **~={green}typea=~** : comportement de type A
- **~={green}obesity=~**  obésité (BMI  : body mass index)
- **~={green}alcolohol=~** : consommation courante d'alcool
- **~={green}age=~** : âge (en année)
- **~={green}chd=~** : maladie coronarienne (1 si l'individu est malade, 0 sinon)
### Enjeu
- On cherche à appréhender les facteurs pouvant influencer l'apparition de cette maladie coronarienne à des fins de prévision
- On cherche à prévoir la probabilité de cette maladie en fonction de constantes de santé chez un individu
- On utilise la ~={red}**régression logistique**=~, méthode de ~={red}**classification supervisée**=~, pour prévoir cette probabilité en fonction de l'âge, puis en fonction de toutes les covariables disponibles
- La régression logistique permet de modéliser (de classifier) une variable binaire prenant ses valeurs dans $\{0, 1\}$ en fonction de covariables (quantitatives et qualitatives).
- Dans notre cas, une régression linéaire serait inintéressante car elle ne donnerait pas de résultat binaire $\{0,1\}$
- Nous utiliserons plutôt une fonction $f(x) = \frac {e^x}{1+e^x}$, nommée ~={red}**fonction sigmoïde**=~, qui nous donnera comme résultat, la probabilité $p \in [0,1]$ d'appartenir à une classe ![[sigmoide.gif]]
### Hypothèses du modèle logistique
- La variable " ~={green}**chd**=~ sachant *~={green}age=~ = ~={yellow} $x$ =~*", a pour valeur $\{0,1\}$, et suit une loi de Bernoulli de paramèter $p(x)$ : $$Y|X = x \sim \mathcal B(p(x))$$
- La probabilité $p(x)$ s'écrit sous la forme : $$p(x) = \mathcal P(Y = 1 | X = x) = \frac {e^{(\beta_0 + \beta_1 x)}}{1 + e^{(\beta_0 + \beta_1 x)}}$$
# Régression logistique
## Modèle
- La régression logistique de $Y \in \{0,1\}$ sur $p$ covariables $X_1,...,X_p$ considère que la loi de $Y$ sachant $X_1 = x_1,...,X_p = x_p$ est : $$Y | X_1 = x_1,...,X_p = x_p \sim \mathcal B(p(x_1,...,x_p)) $$ où $$p(x_1,...,x_p) = \frac {e^{\beta_0 + \beta_1 x_1 + ... + \beta_p x_p}}{1+e^{\beta_0 + \beta_1 x_1 + ... + \beta_p x_p}}$$
- On peut écrire : $$\begin{aligned}
  &\mathbb E(Y | X_1 = x_1,...,X_p = x_p) \\
  = &\mathbb P(Y = 1| X_1 = x_1,...,X_p = x_p) \\
  = &p(x_1,...,x_p)\\
  = &\frac {e^{\beta_0 + \beta_1 x_1 + ... + \beta_p x_p}}{1+e^{\beta_0 + \beta_1 x_1 + ... + \beta_p x_p}}
\end{aligned}$$
## La transformation logit
- On en déduit que : $$\begin{aligned}
  &logit(\mathbb E(Y | X_1 = x_1,...,X_p = x_p)) \\
  = &logit(\mathbb P(Y = 1| X_1 = x_1,...,X_p = x_p)) \\
  = &logit(p(x_1,...,x_p))\\
  = &\beta_0 + \beta_1 x_1 + ... + \beta_p x_p
\end{aligned}$$ où ~={red}**logit**=~ est une fonction définie sur $[0,1]$ et à valeurs dans $\mathbb R$ (bijective et dérivable) définie par : $$logit(x) = ln\left(\frac{x}{1-x}\right)$$
- Dans le modèle de régression linéaire : $$\mathbb E(Y | X_1 = x_1,...,X_p = x_p) = \beta_0 + \beta_1 x_1 + ... + \beta_p x_p$$
  On se ramène à un modèle de régression linéaire en effectuant une transformation logistique (par la fonction logit), on est ici dans le cadre plus global des modèles linéaires généralisés : ~={red}**GLM**=~
## Cas des covariables qualitatives
- Dans le cas d'une ~={yellow}**covariable qualitative**=~ $X_j$ avec $m$ ùodalités, on peut considérer un modèle avec $m$ indicatrices (*dummy variables*) : $$\mathbb 1_{x_j = 1}, \dots , \mathbb 1_{x_j=m} $$
- Le modèle est indéterminé si on considère en sus la constante dans le modèle, on doit alors poser une contrainte du type :
	- $\beta_{j_1} = 0$
	- $\sum_{k=1}^m \beta_{j_k} = 1$
	où $\beta_{j_k}$ désigne le coefficient devant $\mathbb 1_{x_j = k}$ 
## Echantillonnage
- On considère un échantillon : $$d_n = \{\{ (x_{11}, \dots, x_{1p}, y_1), \dots, (x_{n1}, \dots, x_{np}, y_n)  \}\}$$
- Dans les cas des ~={red}**données individuelles**=~, les valeurs $x_i$ sont toutes différentes; $(Y_i)_{i=\{1, \dots, n\}}$ sont alors des v.a.r. indépendantes de loi $\mathcal B\left(p \left(\beta^\top x_i \right)\right)$ où $$\beta = (\beta_0, \beta_1, \dots, \beta_p)^\top \text{ et } x_i = (1, x_i^1, \dots, x_i^p)^\top$$
- Dans les cas des données répétées, les valeurs $x_i$ ne sont pas toutes différentes et on note $\left( x_1^{(r)}, \dots, x_q^{(r)}\right)$ les $q$ valeurs distinctes de $(x_1, \dots, x_n)$, d'effectifs respectifs $\left( n_1^{(r)}, \dots, n_q^{(r)}\right); \left( Y_i^{(r)}\right)_{i=\{1, \dots, q\}}$ sont alors des v.a.r. indépendantes de loi $\mathcal B\left( n_i^{(r)}, p\left( \beta^\top x_i^{(r)}\right)\right)$ où $$\beta = (\beta_1, \dots, \beta_p)^\top \text{ et } x_i^{(r)} = \left( 1, x_{i1}^{(r)}, \dots, x_{ip}^{(r)}\right)^\top$$
## Estimation du modèle (données individuelles)
- La régression logistique ne peut pas être estimée par **MCO**, elle l'est par maximum de vraisemblance
- La vraisemblance vaut : $$v(d_n; \beta) = \overset{n}{\underset{i=1}{\Pi}} p_\beta(x_i)^{y_i} [1- p_\beta(x_i)]^{(1-y_i)}$$
- La **log-vraisemblance** vaut :$$\begin{aligned}
  \mathcal l(d_n; \beta) &= \overset{n}{\underset{i=1}{\sum}}ln(v(d_n;\beta)) \\
  &= \overset{n}{\underset{i=1}{\sum}}\left[ y_i ln(p_\beta(x_i)) + (1-y_i)ln(1-p_\beta(x_i))\right] \\
  &= \overset{n}{\underset{i=1}{\sum}} \left[ y_i ln\left( \frac {p_\beta(x_i)}{1-p_\beta(x_i)}\right) + ln(1-p_\beta(x_i))\right] \\
  &= \overset{n}{\underset{i=1}{\sum}} \left[ y_i x_i^\top \beta - ln( 1+e^{(x_i^\top \beta)})\right]
  \end{aligned}$$
- Pour déterminer le maximum de vraisemblance, on cherche à annuler le gradient de la log-vraisemblance (**~={red}équation du score=~**) : $$S(d_n; \beta) = 0$$où : $$S(d_n; \beta) = \nabla \mathcal \space l(d_n; \beta)$$
- Pour $j \in \{1, \dots, p\}$ : $$\frac {\partial \mathcal l(d_n; \beta)}{\partial \beta_j} = \overset{n}{\underset{i=1}{\sum}} \left( y_i x_i^j - \frac{x_i^j e^{(x_i^\top \beta)}}{1+e^{(x_i^\top \beta)}}\right)$$
- Le système des $p$ équations à $p$ inconnues n'admet pas de solution analytiue, on utilise un algorithme du type d'IRLS (Iterative Reweighted Lest Square)
- Sauf cas particulier (ex : séparabilité parfaite), l'estimateur du maximum du vraisemblance existe et est unique
## Retour à l'étude de cas
![[Regression Logistique Simple vs Multiple.gif]]
# Le sur-apprentissage
## Complexité du modèle et erreur de prévision
![[surapprentissage.gif]]
## Sélection automatique de modèles
- On cherche à déterminer le modèle optimal avec les $k$ covariables les plus adaptées parmi les $p$ de départ.
- Il existe $\left( \begin{matrix} p \\ k \end{matrix}\right)$ modèles avec $k$ covariables parmi les $p$ envisagés.
- On considère un algorithme de recherche automatique faisant appel à un test de la déviance ou un critère de choix (ex : AIC, BIC)
## Critères d'information
- Pour un modèle $M_k$ à $k$ covariables, les critères issus de l'**information de Kullback** sont un compromis entre l'ajustement du modèle (capté par l'oppposé de sa log-vraisemblance $\mathcal l(M_k)$ et la parcimonie du modèle ($k$ figure dans ces critères)
	- Le critère d'**Akaike** (AIC : Akaike Information Criterium) : $$AIC(M_k) = -2 \mathcal l (M_k) + 2 k$$
	- Le critère de **Schwarz** (**BIC** : **Bayesian** Information Criterium, également noté **SBC** : **Schwarz Bayesian** Criterium) : $$BIC(M_k) = -2 \mathcal l (M_k) + k \space ln(n)$$
- Le critère **BIC** peut conduireà des modèles plus parcimonieux que l'AIC ($ln(n) \gt 2 \text{ dès que }n \gt 7$)
## Procédure ascendante ou **forward**
- On initialise la procédure en intégrant uniquement la constante
- Si on utilise un test de déviance : 
	- A chaque itération on incorpore la covariable pour laquelle la $p-valeur$ dans le test de déviance entre les deux modèles emboîté est la plus faible
	- On arrête lorsque toutes les covariables sont intégrées ou lorsque la $p-valeur$ est supérieure à un seuil choisi
- Si on utilise un critère de choix (ex : AIC, BIC) :
	- A chaque itération on incorpore la covariable la plus favorable au sens du critère de choix
	- On arrête lorsque toutes les covariables sont intégrées ou lorsqu'on ne parvient plus à optimiser le critère de choix
## Procédure descendante ou backward
- On initialise la procédure en intégrant toutes les covariables
- Si on utilise un test de déviance : 
	- A chaque itération on retire la covariable pour laquelle la $p-valeur$ dans le test de déviance entre les 2 modèles emboîtés est la plus grande
	- On arrête lorsque toutes les covariables sont retirées ou lorsque la $p-valeur$ est inférieure à un seuil choisi
- Si on utilise un critère de choix (ex : AIC, BIC)
	- A chaque itération on retire la covariable la moins favorable au sens du critère de choix
	- On arrête lorsque toutes les covariables sont retirées ou lorsqu'on ne parvient plus à optimiser le critère de choix
## Procédure pas à pas ou stepwise
- Cette méthode est une procédure de sélection de type forward, avec une possibilité de retirer éventuellement des covariables devenues non significatives (dans une étape backward)
![[Pasted image 20260202185546.png]]
# Performance d'un modèle
## Découpage apprentissage-test
![[apprentissage-test.gif]]
## Critères de performance
### Prévision (cas de classification supervisée binaire)
- On procède de la manière suivante :
	- On estime un modèle sur l'échantillon d'apprentissage
	- On utilise ce modèle estimé pour calculer les probabilités prévues $\mathbb {\hat P}\left( Y = 1 | X = x_i\right)$  sur l'échantillon test
	- On en déduit les prévisions $\hat y_i^{(p)}$ sur l'échantillon test : $$\hat y_i^{(p)} = \begin{cases} 1 &\text {  si }\mathbb {\hat P}\left(Y = 1 | X = x_i \right) \ge s\\ 0 \text { (ou -1)} &\text {sinon}\end{cases}$$où $s$ est un seuil de décision fixé par l'utilisateur (usuellement $s = \frac 12$)
- S'il existe de nombreux critères de qualité possibles, il faut choisir celui (ceux) qui répond(ent) au mieux à la problématique métier
### Matrice de confusion
- Dans le cas de la classification supervisée binaire, la matrice de confusion vaut (avec les notations **TP** et **TN** pour *True Positive* et *True Negative*)

|              | <         | ***Prevision***       | <                     |
| ------------ | --------- | --------------------- | --------------------- |
|              | <         | 1                     | 0 (ou -1)             |
| ***Vérité*** | 1         | **Vrai positif (TP)** | **Faux positif (FP)** |
| ^            | 0 (ou -1) | **Faux Négatif (FP)** | **Vrai négatif (TP)** |
- Dans le cas de la classification supervisée non-binaire, on peut établir la matrice de confusion, avec autant de lignes et de colonnes que de classes, et en déduire les nombres **TP**, **FP**, **TN**, **FN**
### Critères de qualité
- On considère usuellement :
	- L'exactitude
	- La spécificité
	- La précision
	- La sensibilité
	- Le $F_1$
	- L'AUC
- Ces indicateurs prennent leurs valeurs sur $[0,1]$ : plus ils sont proches de 1, meilleur est le modèle
#### Exactitude
Taux de prévisions exactes.
$$exactitude = \frac {TP+TN}{TP+FP+TN+FN}$$
Son opposé est l'erreur de classification.
$$classification \space error = \frac {FP + FN}{TP+FP+TN+FN} = 1 - exactitude$$
#### Spécificité
Taux de vrais négatifs, noté **TNR** pour ***True Negative Rate***.
$$spécificité = \frac {TN}{FP+TN}$$
L'anti-spécificité est le taux de Faux positifs noté FPR pour **False Positive Rate**.
$$anti-spécificité = \frac {FP}{FP+TN}$$
#### Sensibilité
Taux de vrais positifs, similaire à la **spécificité** mais pour les positifs. Noté **TPR** pour ***True Positive Rate***.
$$sensibilité = \frac {TP}{TP + FN}$$
#### Précision
Taux de vrais positifs parmis ceux prédits positifs.
$$précision = \frac {TP}{TP+FP}$$

#### Score $F_1$
Le score $F_1$ est la moyenne harmonique de la précision et de la sensibilité.
$$\begin{aligned}
F_1 &= \frac {2}{\frac {1}{précision} + \frac {1}{sensibilité}} \\
&= 2 \frac {précision \times sensibilité}{précision+sensibilité}
\end{aligned}$$
### Validation croisée
1. On divise aléatoirement les données en $K$ blocs (égaux ou équivalents)
	- Usuellement $K = 5$ ou $K= 10$ 
	- Lorsque $K = n$, on parle d'estimateur "**leave one out**"ou LOO
	- Le bloc $k$ contient $n_k$ individus : $n_k = \frac nK$ si $n$ est un multiple de $K$
2. Pour $k \in \{1, \dots, K\}$ :
	1. Retirer le bloc $k$ de la base d'apprentissage
	2. Estimer la fonction de prévision sur la base d'apprentissage
	3. Calculer un critère d'erreur de prévision sur le bloc $k$ : $CV_k$ (ex : RMSE pour la régression)
3. Calculer le critère de validation croisée : $$CV = \overset{K}{\underset{k=1}{\sum}}\frac {n_k}{n}CV_k$$
![[validationCroisée.gif]]![[validationCroisée-simplevsmultiple.gif]]