 # Points à réviser
## Apprentissage non supervisé
- Analyse exploratoire
	- Clustering
		- Enjeu
		- Différentes méthodes (Kmeans vs CAH)
			- Métriques
			- Détermination nb classes
			- Principes (Stratégie d'aggregation, Algorithme)
			- Avantages/Inconvénients
			- Inerties
	- ACP
		- Objectifs
		- Méthode de réduction de dimension (Matrice var-cov / Matrice correlation)
		- Inertie et information réduction de dimension
		- Interprétation des nouveaux axes
		- Interprétation d'un nuage de points projeté
		- .
### I. Clustering (Classification non-supervisée)

**Enjeu :** Le clustering consiste à répartir des objets en catégories homogènes (ayant des caractères communs) pour en faciliter l'étude. Comme le nombre de partitions possibles (nombre de Bell) explose avec le nombre d'individus, on utilise des algorithmes de recherche.

**Différentes méthodes : K-means vs CAH**

| **Caractéristique** | **K-means (Méthode de partitionnement)**                                                                                                | **CAH (Classification Ascendante Hiérarchique)**                                                                                                    |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Principe**        | Part d'une partition arbitraire et l'améliore itérativement jusqu'à convergence.                                                        | Produit une suite de partitions emboîtées (de $n$ à 1 classe) par regroupements successifs5.                                                        |
| **Algorithme**      | 1. Choisir $K$ centres. Affecter chaque point au centre le plus proche. Recalculer les centres de gravité.  Répéter jusqu'à convergence | 1. Initialisation ($n$ classes).. Agréger les deux classes les plus proches au sens d'une distance $\nabla$.  Répéter jusqu'à n'avoir qu'une classe |
| **Nb de classes**   | Doit être fixé **a priori**8.                                                                                                           | Pas nécessaire de le fixer a priori ; déterminé après coup via le dendrogramme9.                                                                    |
| **Avantages**       | Rapide, conçu pour minimiser l'inertie intra-classe10.                                                                                  | Flexible (métriques et agrégations variées).                                                                                                        |
| **Inconvénients**   | Dépend de l'initialisation ; $K$ doit être connu.                                                                                       | Complexité élevée ($O(n^2 \ln n)$), inutilisable pour de très grands effectifs.                                                                     |

**Métriques :**

* **Variables quantitatives :** Distances de Minkowski (Euclidienne, Manhattan, Chebychev). La distance de Mahalanobis utilise la matrice de variance-covariance.

* **Variables qualitatives :** Distance euclidienne sur tableau disjonctif complet.

* **Variables binaires :** Indices de Jaccard, Sokal & Sneath, Russel & Rao.

**Stratégies d'agrégation (CAH) :**

* **Saut minimal (Single linkage) :** Distance entre les points les plus proches. Risque de classes filiformes.
* **Saut maximal (Complete linkage) :** Distance entre les points les plus éloignés.
* **Méthode de Ward :** Agrège les classes dont la fusion minimise la perte d'inertie inter-classes (ou l'augmentation de l'inertie intra-classe).



**Détermination du nombre de classes :**

* **CAH :** On recherche un "coude" ou un saut important dans les indices de la hiérarchie sur le dendrogramme.



**Inerties et Théorème de Huygens :**

* **Inertie Totale ()** : Somme des distances au carré des points au centre de gravité global .
* **Inertie Intra-classe ()** : Mesure la concentration (homogénéité) au sein des classes.
* **Inertie Inter-classe ()** : Mesure l'éloignement entre les classes.
* **Théorème de Huygens :** . L'objectif est de minimiser intra-classes (classes homogènes) et maximiser  interclasses (classes bien séparées) .



---

### II. ACP (Analyse en Composantes Principales)

**Objectifs :** Réduire la dimension des variables pour analyser les données géométriquement et visualiser les individus et les variables dans un espace de dimension réduite.

**Méthode de réduction de dimension :**

* On transforme des variables corrélées en nouvelles variables décorrélées appelées **composantes principales** (axes factoriels).
* **Matrice var-cov vs corrélation :** Si les variables ont des unités ou des variances très hétérogènes, on utilise la matrice de corrélation (ACP normée) pour que chaque variable ait le même poids initial.



**Inertie et information :**
* L'inertie totale représente la variabilité globale du nuage de points.
* Chaque nouvel axe (composante) capture une part de cette inertie (valeurs propres). On conserve les premiers axes qui expliquent la plus grande partie de l'inertie totale pour réduire la dimension sans trop perdre d'information.



**Interprétation des nouveaux axes :**
* Les axes sont interprétés en regardant quelles variables initiales y sont le plus fortement corrélées.
* Un axe peut par exemple représenter un "effet de taille" ou une opposition entre deux groupes de variables.

**Interprétation d'un nuage de points projeté :**
* **Proximité :** Deux points proches sur le plan factoriel se ressemblent sur les variables qui définissent ces axes.
* **Opposition :** Des points situés aux extrémités opposées d'un axe ont des comportements inverses pour les variables structurantes de cet axe.
* **Qualité de représentation :** Il faut vérifier si l'individu est bien représenté sur le plan (cosinus carré) avant d'interpréter sa position.



## Apprentissage supervisé
- Régression 
	- Critère d'optimisation (ce qu'on cherche à minimiser)
	- Critères de performance
		- Plutôt erreur
	- Grands principes
	- Critères d'erreur
	- Colinéarité
	- Maximum de vraisemblance
	- Estimateur des moindres carrés à retenir
	- Lecture des P-valeurs
	- Lutte contre le surapprentissage (covariables)
	- Régularisation
	- Ridge Lasso et elasticnet
	- Validation test / validation croisée
- Classification supervisée
	- Critère d'optimisation (ce qu'on cherche à minimiser)
	- Critères de performance
		- Plutôt qualité 
	- Grands principes
	- Critères d'erreur
	- Colinéarité
	- Maximum de vraisemblance
	- Estimateur des moindres carrés à retenir
	- Lecture des P-valeurs
	- Lutte contre le surapprentissage (covariables)
	- Régularisation
	- Ridge Lasso et elasticnet
	- Validation test / validation croisée 
## Régression
### I. Grands principes et Modèles

- **Enjeu** : Mettre en relation une variable quantitative à expliquer ($Y$) avec une ou plusieurs variables explicatives ou covariables ($X_1, ..., X_p$).
    
- **Modèle de régression simple** : $Y = \beta_0 + \beta_1 X + \epsilon$.
    
- **Modèle de régression multiple** : $Y = \beta_0 + \beta_1 X_1 + ... + \beta_p X_p + \epsilon$ .
    
- **Maximum de vraisemblance** : Sous l'hypothèse de normalité des erreurs ($\epsilon \sim \mathcal{N}(0, \sigma^2)$), l'estimateur du maximum de vraisemblance coïncide avec celui des moindres carrés 5555.
    

### II. Critères d'optimisation et Estimation

- **Critère à minimiser** : On cherche à minimiser la **Somme des Carrés des Résidus (SCR)**, c'est-à-dire la distance entre les valeurs observées et les valeurs ajustées par le modèle.    
    - $S(\beta) = \sum_{i=1}^{n} (y_i - \beta_0 - \beta_1 x_{i1} - ...)^2$.        
- **Estimateur des Moindres Carrés Ordinaires (MCO)** : À retenir, la formule matricielle est $\hat{\beta} = (X^\top X)^{-1} X^\top y$.    
- **Colinéarité** : L'estimateur MCO n'est calculable que si les colonnes de la matrice $X$ ne sont pas colinéaires (matrice $X^\top X$ inversible).    

### III. Performance et Qualité de l'ajustement

- **Critères d'erreur** :
    
    - **RMSE (Root Mean Squared Error)** : Évalue la qualité de l'ajustement (sur l'apprentissage) ou de la prévision (sur le test) 10.        
    - **$\hat{\sigma}^2$ (Variance résiduelle)** : Estimation de la variance de l'erreur $\sigma^2$.        
- **Coefficient de détermination ($R^2$)** : $R^2 = \frac{SCE}{SCT}$ représente la part de variance expliquée par le modèle. Un $R^2$ proche de 1 indique un bon ajustement, mais pas forcément un lien linéaire.    
- **Lecture des P-valeurs** : Utilisées pour tester la significativité des coefficients ($\beta_j = 0$). Une p-valeur faible (généralement $< 0,05$) permet de rejeter l'hypothèse nulle et de considérer que la covariable a un impact significatif sur $Y$.   

### IV. Lutte contre le surapprentissage et Sélection

- **Surapprentissage** : Apparaît lorsque la complexité du modèle est trop grande par rapport au nombre de données, entraînant une faible erreur d'apprentissage mais une forte erreur de prévision.
    
- **Sélection de covariables** :
    
    - **Procédures automatiques** : _Forward_ (ajout successif), _Backward_ (retrait successif) ou _Stepwise_ .        
    - **Critères d'information** : AIC et BIC pénalisent la complexité du modèle ($k$) pour favoriser la parcimonie .        
- **Validation** :    
    - **Validation test** : Découpage des données en un échantillon d'apprentissage (estimation) et un échantillon de test (évaluation de la prévision) .        
    - **Validation croisée** : Technique plus robuste pour évaluer la performance en moyennant l'erreur sur plusieurs découpages (notée dans le plan du cours).        

### V. Régularisation (Ridge, Lasso, ElasticNet)

Bien que mentionnées dans votre demande, les définitions détaillées de Ridge, Lasso et ElasticNet n'apparaissent pas explicitement dans les pages extraites ici (elles figurent généralement dans la section "Contre le sur-apprentissage"). Ces méthodes ajoutent une pénalité à la fonction de coût pour limiter la taille des coefficients $\beta$ :

- **Ridge** : Pénalité $L_2$ (carré des coefficients), réduit la variance sans annuler les coefficients.
    
- **Lasso** : Pénalité $L_1$ (valeur absolue), peut annuler certains coefficients (sélection de variables).
    
- **ElasticNet** : Combinaison des pénalités $L_1$ et $L_2$.

## Classification
### I. Grands principes et Modèles

- **Enjeu** : Prédire une variable qualitative $Y$ (souvent binaire $0/1$) à partir de variables explicatives $X$.
    
- **Régression Logistique** : On ne modélise pas directement $Y$, mais la probabilité que $Y=1$ sachant $X$.
    
    - **Fonction Logit** : $logit(P(Y=1|X)) = \ln\left(\frac{P}{1-P}\right) = \beta_0 + \beta_1 X_1 + \dots + \beta_p X_p$.
        
    - La prédiction finale dépend d'un **seuil** (souvent 0.5) : si $P > 0.5$, alors $\hat{Y}=1$.
        

### II. Critères d'optimisation et Estimation

- **Maximum de Vraisemblance (MV)** : Contrairement à la régression linéaire, on n'utilise pas les moindres carrés car $Y$ n'est pas quantitative. On cherche les paramètres $\beta$ qui maximisent la probabilité d'observer les données réelles.
    
- **Critère à minimiser** : On minimise la **Log-vraisemblance négative** (souvent appelée _Deviance_).
    
- **Colinéarité** : Comme en régression linéaire, une forte corrélation entre les variables $X$ rend l'estimation des $\beta$ instable et augmente leur variance.
    

### III. Critères de performance (Qualité du modèle)

En classification, on évalue la qualité via la **matrice de confusion** :

- **Exactitude (Accuracy)** : Taux de bonnes prédictions globales.
    
- **Sensibilité (Rappel)** : Capacité à bien détecter les "Malades" (Vrais Positifs).
    
- **Spécificité** : Capacité à bien détecter les "Non-malades" (Vrais Négatifs).
    
- **Précision** : Proportion de vrais malades parmi ceux prédits malades.
    
- **Courbe AUC** : L'AUC (Aire sous la courbe) mesure la capacité du modèle à distinguer les classes, quel que soit le seuil choisi. Une AUC proche de 1 est excellente.
    

### IV. Lutte contre le surapprentissage

Le surapprentissage survient quand le modèle est trop complexe (trop de variables) et "apprend par cœur" le bruit des données d'entraînement.

- **Sélection de variables** : Utilisation de procédures _Stepwise_ (AIC/BIC) pour ne garder que les covariables significatives (via la lecture des **P-valeurs** : si $p < 0.05$, la variable est conservée).
    
- **Validation test** : Séparer les données en _Train_ (80% pour estimer) et _Test_ (20% pour vérifier l'erreur réelle).
    
- **Validation croisée (K-fold)** : On divise les données en $K$ morceaux. On entraîne le modèle sur $K-1$ morceaux et on teste sur le dernier. On répète $K$ fois pour obtenir une erreur de prévision robuste.
    

### V. Régularisation (Ridge, Lasso, ElasticNet)

La régularisation ajoute une **pénalité** à la fonction de coût pour contraindre la taille des coefficients $\beta$ et réduire la complexité.

1. **Ridge (pénalité $L_2$)** : Ajoute $\lambda \sum \beta_j^2$. Réduit les coefficients vers 0 sans jamais les annuler. Très efficace contre la colinéarité.
    
2. **Lasso (pénalité $L_1$)** : Ajoute $\lambda \sum |\beta_j|$. Cette méthode peut annuler exactement certains coefficients, réalisant ainsi une **sélection automatique de variables** (_modèles sparses_).
    
3. **ElasticNet** : Combine les deux pénalités ($L_1$ et $L_2$). Utile quand plusieurs variables sont corrélées entre elles (le Lasso n'en choisirait qu'une seule au hasard, l'ElasticNet les traite mieux ensemble).
    

- **Paramètre $\lambda$** : C'est le coefficient de régularisation. S'il est trop fort, le modèle est trop simple (sous-apprentissage) ; s'il est trop faible, on revient aux moindres carrés (risque de surapprentissage). On le choisit par **validation croisée**.
### Séries temporelles

### 1. Grands principes

L'objectif principal des modèles GARCH est de modéliser la **volatilité** (variance conditionnelle) des séries temporelles financières, qui présentent souvent des caractéristiques particulières :

- **Hétéroscédasticité conditionnelle** : La variance n'est pas constante dans le temps.
    
- **Regroupement de la volatilité (_Volatility Clustering_)** : Les périodes de forte (ou faible) variation ont tendance à se succéder.
    
- **Queues épaisses (_Fat tails_)** : Les rendements financiers ne suivent souvent pas une loi normale (excès de kurtosis).
    

### 2. Algorithme et Enjeux

Le modèle décompose la série temporelle $X_t$ (généralement le rendement) en deux parties :

1. **L'innovation** : $X_t = \sigma_t \epsilon_t$, où $\epsilon_t$ est un bruit blanc de variance 1.
    
2. **L'équation de la variance** :
    
    - **ARCH(q)** : La variance actuelle $\sigma_t^2$ dépend des carrés des rendements passés ($X_{t-1}^2, \dots, X_{t-q}^2$).
        
    - **GARCH(p, q)** : La variance actuelle $\sigma_t^2$ dépend à la fois des carrés des rendements passés et de ses propres valeurs passées ($\sigma_{t-1}^2, \dots, \sigma_{t-p}^2$).
        

**L'enjeu** est de capturer la persistance de la volatilité pour mieux évaluer le risque (comme la Value-at-Risk).

### 3. Critères d'optimisation

L'estimation des paramètres ($\omega, \alpha, \beta$) ne se fait pas par moindres carrés car le modèle n'est pas linéaire sur les paramètres de la variance. On utilise :

- **Le Maximum de Vraisemblance (MV)** : On cherche les paramètres qui maximisent la probabilité d'avoir observé la série réelle.
    
- **Le Quasi-Maximum de Vraisemblance (QMV)** : Utilisé lorsque l'on n'est pas sûr que les résidus suivent une loi normale, mais que l'on souhaite tout de même des estimateurs convergents.
    

### 4. Critères de performance

Pour juger de la qualité d'un modèle GARCH, on vérifie :

- **La blancheur des résidus** : Après avoir divisé la série par la volatilité estimée ($\hat{\epsilon}_t = X_t / \hat{\sigma}_t$), le résidu obtenu ne doit plus présenter d'autocorrélation, ni sur ses valeurs, ni sur ses carrés.
    
- **Tests de Ljung-Box** : Appliqués aux résidus standardisés et à leurs carrés.
    
- **AIC / BIC** : Critères d'information pour choisir les ordres $p$ et $q$ (on cherche à minimiser ces valeurs pour favoriser la parcimonie).
    

### 5. Critères d'erreur

L'évaluation se fait souvent sur la capacité du modèle à prévoir la volatilité future :

- **Erreurs de prévision** : Comparaison entre la variance réalisée (souvent approximée par $X_t^2$) et la variance prédite $\sigma_t^2$.
    
- **Signification des paramètres** : Les coefficients doivent être statistiquement significatifs (p-valeur < 0,05) et respecter les conditions de stationnarité (ex: pour un GARCH(1,1), $\alpha_1 + \beta_1 < 1$).
    

### 6. Avantages et Inconvénients

|**Avantages**|**Inconvénients**|
|---|---|
|**Captation du clustering** : Très efficace pour modéliser les crises financières.|**Symétrie** : Le GARCH de base traite de la même manière les bonnes et les mauvaises nouvelles (pas d'effet de levier).|
|**Parcimonie** : Un GARCH(1,1) suffit souvent là où un ARCH(q) nécessiterait un $q$ très élevé.|**Complexité d'estimation** : Nécessite des algorithmes d'optimisation numérique parfois instables.|
|**Standardisation** : Permet de "blanchir" les données pour d'autres modèles.|**Hypothèse de distribution** : Les performances chutent si la loi des résidus est mal spécifiée (ex: loi Normale vs loi de Student).|
Formules à retenir :
~={yellow}formule ARCH et GARCH (page 36)=~epi