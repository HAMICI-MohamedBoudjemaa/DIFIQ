
# Introduction
## Cas d’étude 1 : Taux de guérison suite à un nouveau traitement
### Les données

- Considérons ce premier cas, qu’on peut qualifier de discret.

- Un laboratoire cherche à savoir si la nouvelle composition du médicament (contre une maladie bénigne) qu’il compte commercialiser améliore le taux de guérison par rapport à un médicament déjà sur le marché.

- Des tests cliniques ont été effectués sur $n = 216$ individus sur lesquels on a observé la guérison (notée « 1 ») ou la non-guérison (notée « 0 ») :$$\{x_1, . . . , x_{216}\} = \{1, 0, 1, 1, . . . , 1, 0\}$$

-  $x_i$ désigne l’observation de la guérison ($x_i = 1$) ou non ($x_i = 0$) pour l’individu $i$.

-  Il observe au total 167 guérisons, soit environ 77.3% de guérisons.
- Notons que l'éventuelle autorisation de mise sur le marché de ce médicament repose sur une procédure plus complexe (http://ansm.sante.fr/Activites/Autorisations-de-Mise-sur-le-Marche-AMM/L-AMM-et-le-parcours-du-medicament/)
### L'objectif
1. Le laboratoire aimerait connaître le taux de guérison (théorique) $p$ suite à la prise de son médicament.

2. De manière plus modeste, il souhaiterait également disposer d’un intervalle probabilisé pour ce taux de guérison.

3. Enfin, il aimerait éprouver que son nouveau médicament est (significativement) meilleur que celui actuellement sur la marché dont le taux de guérison avéré est $p_0 = 0.75$ (75%).

## Cas d’étude 2 : Consommation d’essence de cars
### Les données
- Considérons ce second cas, qu’on peut qualifier de continu.

- Un constructeur de cars souhaite appréhender la consommation d’essence de son dernier modèle. Pour cela, il lance un protocole d’essais sur 128 cars et recueille leur consommation d’essence en litres après avoir parcouru 100 km (appelée « nombre de litres aux 100 ») :$$\{x_1, . . . , x_{128}\} = \{26.23, 26.40, . . . , 35.50, 35.50, 36.07\}$$

- Il observe une consommation moyenne de 31.45 litres aux 100.
### L'objectif
1. Le constructeur aimerait connaître la consommation (théorique) d’essence $\mu$ de son modèle de car. 
2. De manière plus modeste, il souhaiterait également disposer d’un intervalle autour de cette consommation estimée, évaluée sur 128 expériences. 
3. Enfin, il souhaiterait communiquer auprès de ses clients sur un chiffre ambitieux : une consommation égale à $\mu_0 = 31$ litres aux 100.
### La solution

1. A la première question, on donnera comme réponse une estimation (ponctuelle) :
- du taux de guérison théorique $p$ dans le premier exemple.
- de la consommation d’essence théorique $\mu$ dans le second exemple (on peut vouloir aussi estimer la dispersion de cette consommation $\sigma^2$).

2. La réponse apportée à la seconde question sera un intervalle de confiance.

3. Enfin pour répondre à la troisième question, il mettra en place un test statistique pour vérifier que :
- $p > p_0$, avec $p_0 = 0.75$, dans le premier exemple,
- $\mu = \mu_0$, avec $\mu_0 = 31$, dans le second exemple.
## Enjeux de l'inférence

- En statistique descriptive, on souhaite, comme son nom l’indique, décrire un échantillon (contenant une ou plusieurs variables). Mais il est impossible d’inférer/d’extrapoler ce qui est constaté sur un échantillon à la population statistique tout entière.

- Si on revient au premier exemple, on ne peut que constater que le taux de guérison observé sur la population vaut 77,8%. Il est pourtant impossible d’affirmer qu’il s’agisse du taux de guérison théorique, il aurait été ainsi possible d’observer un taux de 74% ou 79% sur d’autres échantillons de taille similaire.

- De même, sur le second exemple, on ne peut que constater que la consommation au 100 moyenne vaut 31.45% sur notre échantillon, il est très probable qu’on observerait d’autres valeurs sur des échantillons différents.
## Inférer
![[Pasted image 20260205073843.png]]
## Sources d’aléas

- La **~={red}variabilité intrinsèque du phénomène=~** :
	- Dans le premier exemple, tous les patients présentent des spécificité, un patrimoine génétique différent par exemple, qui pourront influer sur sa guérison.
	- Dans le second exemple, les mesures sont effectués sur des cars qui peuvent présenter de légers écarts de fabrication, et sur des trajets qui présentent forcément des écarts (notamment en fonction du conducteur).
- La **~={red}variabilité due à l’échantillonnage=~** : des résultats potentiellement différents sur d’autres échantillons. . .
## Modèle probabiliste

- Introduire un modèle probabiliste permet de disposer d’outils théoriques capables de prendre en compte les aléas du problème, et d’étendre les résultats obtenus sur un échantillon à la population toute entière.

- On suppose donc ici que chaque observation $x_i$ est la réalisation d’une variable aléatoire $X_i$, c’est-à-dire le fruit d’un tirage aléatoire.

- On se place dans le cas de figure où toutes les observations peuvent être considérées comme indépendantes, et représentatives du même phénomène ; mathématiquement les variables aléatoires sont i.i.d : indépendantes et identiquement distribuées.
### Modèles probabilistes des exemples introductifs

- Dans le premier exemple, on est dans un modèle dit de Bernoulli : les variables aléatoires suivent la même loi $\mathcal{B}(p)$, et ce de manière indépendante.

- Dans le second exemple, on peut considérer l’hypothèse gaussienne : les variables aléatoires suivent la même loi $\mathcal{N}(\mu, \sigma^2)$, et ce de manière indépendante.

- Cette hypothèse gaussienne n’est pas anodine, mais peut être émise au vu de la forme de l’histogramme, et pourra être vérifiée via un test (Kolmogorov-Smirnov, par exemple).
# Estimation ponctuelle
## Généralités
### Idée

- Dans les deux exemples traités, on a un échantillon i.i.d ($X_1, . . . , X_n$) dont la loi de probabilité est connu à un paramètre $\theta$ près :
	- dans le premier exemple : $\theta = p$,
	- dans le second exemple : $\theta = (\mu, \sigma^2)$.

- Pour appréhender ces paramètres, on ne dispose que des observations ($x_1, . . . , x_n$), réalisations des variables aléatoires i.i.d ($X_1, . . . , X_n$).

- De manière assez simple, un estimateur est une fonction des observations, qui prend ses valeurs dans le domaine de définition du paramètre.

- Il existe toujours plusieurs estimateurs pour un paramètre, l’objectif est de considérer un « bon » estimateur.

- On étudie habituellement un certain nombre de propriétés souhaitables pour un estimateur.
### Principe

- Soit un échantillon i.i.d ($X_1, . . . , X_n$) dont la loi de probabilité est paramétrée par $\theta \in \mathbb{R}^k, k \in \mathbb{N}^\star$.

- Pour appréhender le paramètre $\theta$, on ne dispose que des observations ($x_1, . . . , x_n$), réalisation de l’échantillon i.i.d ($X_1, . . . , X_n$).

- On utilise à cet effet un estimateur dont on étudie les propriétés théoriques.
### Estimateur

- On appelle estimateur du paramètre $\theta$, noté $\hat{\theta}$, une fonction (on parle aussi de statistique) de l’échantillon qui prend ses valeurs dans le domaine de définition $\Theta$ de $\theta$ :
$$\hat{\theta} = T (X_1, . . . , X_n) .$$

- Dans le premier cas d’étude, le domaine $\Theta$ est $[0, 1]$.
### Qualités attendues pour un estimateur

- On souhaite qu’un estimateur soit **~={red}exhaustif=~**, c’est-à-dire qu’il puisse capter toute la connaissance sur le paramètre contenue dans les observations, l’échantillon.

- On souhaite qu’un estimateur soit **~={red}consistant=~** (convergeant) : l’estimateur calculé sur un échantillon sera d’autant plus fin, proche de la « vérité », que la taille de l’échantillon sera importante. *(Si on pouvait faire croître indéfiniment la taille de l’échantillon, on se rapprocherait asymptotiquement de la « vraie » valeur du paramètre.)*

- On souhaiterait dans l’absolu qu’un estimateur soit **~={red}sans biais=~** (du moins pour des grands échantillons) et de **~={red}variance faible=~**.

- On peut ***~={green}synthétiser ces deux dernières qualités=~*** en souhaitant disposer d’un **~={red}estimateur au risque quadratique le plus faible possible=~**.
### Exhaustivité d’un estimateur

- Un estimateur est **~={red}exhaustif=~** si la loi de l’échantillon ($X_1, . . . , X_n$) conditionnellement à l’estimateur $\hat{\theta}$ est indépendante de $\theta$.

- On souhaite considérer un estimateur qui permette d’extraire toute l’information contenue par l’échantillon pour le paramètre $\theta$.
### Consistance d’un estimateur

- Un estimateur $\hat{\theta}$ de $\theta$ est dit **~={red}consistant=~** si :
$$\hat{\theta} \xrightarrow{P} \theta .$$

- On souhaite que l’estimateur s’approche asymptotiquement du paramètre lorsque la taille de l’échantillon grandit.

- Point de détail mathématique, la convergence presque sûre, qu’on retrouve dans la loi forte des grands nombres, entraîne la convergence en probabilité.
### Biais d’un estimateur

- Le biais de l’estimateur $\hat{\theta}$ de $\theta$ vaut :
$$Biais (\hat{\theta}, \theta) = E[\hat{\theta}] - \theta .$$

- Il s’agit de l’écart entre la moyenne théorique de l’estimateur et le paramètre.
### Estimateur sans biais ou asymptotiquement sans biais

- En pratique on n’utilise que des estimateurs sans biais ou asymptotiquement sans biais.

- Un estimateur $\hat{\theta}$ de $\theta$ est dit :
	- sans biais si son biais est nul :
$$E[\hat{\theta}] = \theta ,$$
	- asymptotiquement sans biais si son biais est asymptotiquement nul :
$$E[\hat{\theta}] \xrightarrow{n \to +\infty} \theta$$
### Risque quadratique

- Le risque quadratique d’un estimateur $\hat{\theta}$ de $\theta$ est défini par :
$$R(\hat{\theta}, \theta) = E\left[(\hat{\theta} - \theta)^2\right]$$

- Cette mesure permet d'évaluer la performance globale de l'estimateur en combinant à la fois son biais et sa variance. On peut en effet démontrer la décomposition suivante :
$$R(\hat{\theta}, \theta) = \text{Var}(\hat{\theta}) + \left(\text{Biais}(\hat{\theta}, \theta)\right)^2$$

- Un bon estimateur est un estimateur qui minimise ce risque quadratique, offrant ainsi un compromis optimal entre précision (faible variance) et exactitude (faible biais).
- Si un estimateur $\hat \theta$ de $\theta$ est sans biais alors : $$R(\hat \theta, \theta) = Var(\hat \theta)$$
### Illustrations biais et variance
![[Pasted image 20260205084035.png]]![[Pasted image 20260205084045.png]]
### Choisir un estimateur

- Sans idée sur un estimateur, on peut notamment utiliser comme méthodes pour en déterminer :
	- La **~={red}méthode des moments=~**.
	- La **~={red}méthode du maximum de vraisemblance=~**.

- On peut trouver dans la littérature de nombreux estimateurs classiques, connus pour leurs bonnes propriétés statistiques.
### Méthode des moments

- La méthode des moments consiste à trouver une fonction $m$, continue et inversible, et une fonction (continue) $\phi$ telles que $m(\theta) = E[\phi(X_1)]$.

- L’estimateur des moments pour $\theta$ vaut :
$$\hat{\theta} = m^{-1} \left( \frac{1}{n} \sum_{i=1}^n \phi(X_i) \right) .$$

- L’estimateur des moments est consistant.
### Maximum de vraisemblance

- La vraisemblance est définie :
	- dans le cas discret i.i.d :
$$p(x_1, \dots, x_n; \theta) = P(X_1 = x_1, \dots, X_n = x_n)$$
$$= \prod_{i=1}^n P(X_i = x_i) \text{ de par l’indépendance}$$
$$= \prod_{i=1}^n P(X = x_i) \text{ de par la loi identique ,}$$
	- dans le cas continu i.i.d :
$$p(x_1, \dots, x_n; \theta) = f(x_1, \dots, x_n)$$
$$= \prod_{i=1}^n f_{X_i}(x_i) \text{ de par l’indépendance}$$
$$= \prod_{i=1}^n f(x_i) \text{ de par la loi identique .}$$

- L’estimateur du maximum de vraisemblance maximise $p$.

- La vraisemblance mesure la probabilité que les observations proviennent effectivement d’un échantillon de loi paramétrée par $\theta$. Trouver le maximum de vraisemblance consiste donc à trouver le paramètre le plus vraisemblable pour l’échantillon.

- On considère usuellement la log-vraisemblance (qui facilite les calculs pour des lois de probabilité appartenant à la famille dite exponentielle) :
$$\ell (x_1, \dots, x_n; \theta) = \ln (p (x_1, \dots, x_n; \theta)) .$$

- L’intérêt de cette méthode, au-delà de trouver un estimateur dans un cas moins intuitif, est de trouver un estimateur qui est muni d’excellentes qualités dans de très nombreux cas : consistant, asymptotiquement sans biais et de variance minimale. La plupart du temps, cet estimateur est unique et se détermine explicitement.
## Proportion
### Cas du taux de guérison

- Pour estimer le taux de guérison dans le premier exemple, $p$, le choix de la moyenne empirique $\bar{x}$ paraît naturel. Cette quantité représente la fréquence de guérisons réellement observées sur les 216 individus de l’échantillon.

- On obtient comme « estimateur » du taux de guérison :
$$\bar{x} = \frac{167}{216} \simeq 0.773 .$$

- Le taux de guérison estimé vaut donc 77.3%.
### Cas général

- Dans le cas où un dispose d’un échantillon i.i.d de loi $\mathcal{B}(p)$, on considère comme estimateur de $p$ :
$$\hat{p} = \bar{X} = \frac{1}{n} \sum_{i=1}^n X_i .$$

- Cet estimateur est doté de bonnes propriétés (consistant et sans biais), cela nous conforte dans la décision intuitive de choisir la moyenne empirique (la fréquence empirique) comme estimateur.
## Moyenne et variance
### Cas de la consommation d’essence I

- Pour estimer la consommation moyenne (théorique) dans le second exemple, $\mu$, le choix de la moyenne empirique $\bar{x}$ paraît là encore naturel.

- On obtient comme « estimateur » cette consommation moyenne :
$$\bar{x} = \frac{1}{128} \sum_{i=1}^{128} x_i \simeq 31.45 .$$

- La consommation moyenne (théorique) d’essence au 100 est donc estimée à 31.45 litres.

- Pour estimer cette fois la variance de cette consommation, $\sigma^2$, on choisit de manière analogue la variance empirique.

- On peut donc considérer comme « estimateur » cette variance de consommation :
$$v = \frac{1}{128} \sum_{i=1}^{128} (x_i - \bar{x})^2 \simeq 4.63 .$$

- On considère souvent la version dite « non biaisée » de cette variance (on divise par $127$ au lieu de $128$) :
$$s'^2 = \frac{1}{127} \sum_{i=1}^{128} (x_i - \bar{x})^2 \simeq 4.66 .$$

- Cette version est souvent celle par défaut dans les logiciels statistiques.
### Cas général

- On se place dans le cas où un dispose d’un échantillon i.i.d dont la loi admet $\mu$ comme moyenne théorique (l’espérance mathématique) et $\sigma^2$ comme variance.

- On considère comme estimateur consistant et sans biais de $\mu$ :
$$\hat{\mu} = \bar{X} = \frac{1}{n} \sum_{i=1}^n X_i$$

- On considère comme estimateur consistant de $\sigma^2$ (asymptotiquement sans biais) :
$$\hat{\sigma}^2_{biaisé} = V = \frac{1}{n} \sum_{i=1}^n (X_i - \bar{X})^2$$

- Ou plutôt sa version sans biais (par défaut dans les logiciels) :
$$\hat{\sigma}^2_{non \ biaisé} = S'^2 = \frac{1}{n - 1} \sum_{i=1}^n (X_i - \bar{X})^2$$
# Tests statistiques
## Cas du taux de guérison
### Cas du taux de guérison I

- Le laboratoire cherche à savoir si la nouvelle composition du médicament présente un taux de guérison meilleur que le précédent. Il considère comme a priori que son efficacité est similaire au précédent médicament et ne prendra la responsabilité de proposer la nouvelle composition que si le nouveau taux de guérison s’avère être significativement supérieur à celui de l’ancien médicament $p_0 = 0.75$.

- Son a priori correspond à ce qu’on appellera l’hypothèse nulle, notée $H_0$. Quant à l’autre hypothèse, l’alternative, notée $H_1$, elle permet d’indiquer dans quel cas de figure on rejettera cet a priori.

- On considère donc ici le test suivant :
$$
\begin{cases}
H_0 : p = p_0 \\
H_1 : p > p_0 
\end{cases}
$$

- L’hypothèse $p = p_0$ paraît intuitivement d’autant moins crédible que $\bar{x}$ (correspondant à la fréquence empirique de guérisons) est plus fort. Quand $\bar{x}$ sera jugé « suffisamment plus élevé » que $p_0$ (significativement supérieur à $p_0$), le laboratoire pourra rejeter l’hypothèse $p = p_0$.

- C’est le rejet de $H_0$ qui, s’il est fait à mauvais escient, sera considéré comme le plus coûteux pour le laboratoire, car ayant des répercussions humaines et économiques néfastes : on parle de **~={red}risque de première espèce=~**.

- On parle ici d’**~={red}hypothèse simple=~** pour $H_0$ et d’**~={red}hypothèse alternative=~** (ou composite) pour $H_1$.

- En pratique on recherche la valeur $c \geq 0$ telle qu’on rejettera l’hypothèse nulle si :
$$\bar{X} > p_0 + c ,$$
	c’est-à-dire quand la proportion de guérison observée est « vraiment » supérieure à $p_0$.

- Pour fixer ce seuil $c$ qui détermine la région de rejet, on doit demander au laboratoire de fixer une borne supérieure à la probabilité qu’il juge tolérable pour ce rejet à mauvais escient : **~={red}le niveau de test=~** (souvent noté $\alpha$).

- Ensuite, sous cette contrainte, on cherchera à choisir $c$ de manière à minimiser la probabilité de non-rejet de $H_0$ à mauvais escient : **~={red}le risque de seconde espèce=~** (noté $\beta$).

- On constate que la première préoccupation (sur le risque de première espèce) conduit à souhaiter prendre la frontière $c$ assez élevée, et la seconde (sur le risque de seconde espèce) pousse au contraire à l’abaisser.
## Cas de la consommation d'essence
### Cas de la consommation d’essence I

- Le fabricant de cars souhaite communiquer sur une consommation moyenne (théorique) d’essence égale à $\mu_0 = 31$ litres aux 100. Il ne souhaite pas sous-estimer ou sur-estimer cette valeur seuil.

- De la même manière que précédemment, on considère le test :
$$
\begin{cases}
H_0 : \mu = \mu_0 \\
H_1 : \mu \neq \mu_0
\end{cases}
$$

- Ce test est dit **bilatère** car il existe deux motifs de rejet de son hypothèse de travail (soit la consommation est significativement plus faible, soit elle est significativement plus élevée).

- L’hypothèse $\mu = \mu_0$ paraît intuitivement d’autant moins crédible que $\bar{x}$, consommation moyenne observée sur son échantillon, est jugé « suffisamment différente » de $\mu_0$ (significativement inférieure ou supérieure à $\mu_0$).

- C’est toujours ce rejet qui, s’il est fait à mauvais escient, sera considéré comme plus coûteux pour le constructeur...

- En pratique on recherche la valeur $c > 0$ telle qu’on rejette l’hypothèse nulle si :
$$|\bar{x} - \mu_0| > c ,$$
	c’est-à-dire si la consommation d’essence moyenne observée est « vraiment différente » de $\mu_0$.

- Pour fixer ce seuil $c$ qui détermine la région de rejet, on doit là-encore demander au constructeur de fixer une borne supérieure pour son risque de première espèce, celui de rejeter à tort son a priori.
## Objectif
### Synthèse des paramètres à tester

- On cherche à tester une hypothèse sur le paramètre $\theta$.

- Le paramètre $\theta$ est :
    - $p$ (taux de guérison) dans le premier exemple introductif.
    - $\mu$ (consommation moyenne) dans le second.
### Hypothèses $H_0$ et $H_1$

- On appelle **~={red}hypothèse nulle=~**, notée $H_0$, l’hypothèse qu’on ne souhaite pas rejeter trop facilement : c’est celle qu’on teste.

- L’**~={red}hypothèse alternative=~**, notée $H_1$, indique dans quelles conditions on rejette $H_0$ (elle fournit les informations de forme sur la région critique)
### Région critique

- La **~={red}région critique=~** $W$ indique quand on rejette l’hypothèse nulle, elle est basée sur une ***~={red}statistique de test=~***.

- Pour déterminer entièrement la région critique, il faut connaître la loi (éventuellement asymptotique) de la statistique de test sous $H_0$.
### Risques associés aux décisions I

On considère plusieurs risques pour la prise de décision, et ce de manière séquentielle :

- **~={red}Le risque de première espèce=~** désigne celui de rejeter l’hypothèse nulle $H_0$ alors que cette hypothèse est vraie. C’est le risque dont on veut se prémunir en premier lieu.

- On se fixe un **~={red}niveau de te=~st** qui représente le risque de première espèce maximum. On note $\alpha$ ce niveau. Les valeurs couramment employées sont $5\%$, $1\%$ et $5\text{‰}$.

- Une fois ce premier risque borné par le niveau de test, on minimise le **~={red}risque de seconde espèce=~** $\beta$ (de manière équivalente, on maximise la **~={orange}puissance du test=~** $1 - \beta$).

- On peut résumer ces risques dans le tableau suivant :

| Décision \ Vérité      | $H_0$ vraie                                          | $H_0$ fausse                                        |
| :--------------------- | :--------------------------------------------------- | :-------------------------------------------------- |
| **Rejet de $H_0$**     | **~={red}Erreur Type I=~** (Risque $\alpha$)         | **~={green}Bonne décision=~** (Puissance $1-\beta$) |
| **Non rejet de $H_0$** | **~={green}Bonne décision=~** (Confiance $1-\alpha$) | **~={red}Erreur Type II=~** (Risque $\beta$)        |

- Les cases en vert (Bonnes décisions) désignent les configurations de bonne décision, les cases en rouge (Erreurs) les configurations d’erreur dans la décision.
### Analogie avec la justice

- On se place dans le cadre d’un procès.
- **L’hypothèse nulle $H_0$** est « le prévenu est innocent ». (C'est la présomption d'innocence).
- **L’hypothèse alternative $H_1$** est « le prévenu est coupable ».
- **La région critique** comprend le nombre de preuves à charge qu’il faut a minima pour rejeter l’innocence.
- **Le risque de première espèce ($\alpha$)** est le risque de déclarer coupable un innocent (erreur judiciaire grave).
- **Le risque de seconde espèce ($\beta$)** est le risque de ne pas déclarer coupable un coupable (impunité).
### p-valeur

- Usuellement on travaille avec la **~={red}p-valeur=~** (ou *p-value*) du test : la plus petite valeur du niveau de test conduisant au rejet de $H_0$.

- C’est cette valeur qu’on trouve systématiquement dans les logiciels statistiques (R, Python, SPSS, etc.).

- On construit cette p-valeur de manière à avoir l’équivalence suivante pour la prise de décision :
$$\text{Rejet de } H_0 \text{ au niveau de test } \alpha \iff \text{p-valeur} < \alpha$$

- ~={green}Si la p-valeur est faible (selon un critère fixé par le domaine concerné, souvent $0.05$), cela signifie que l’observation est rare (donc peu probable) sous $H_0$, ce qui incite à rejeter l’hypothèse $H_0$.=~
### Puissance de test et taille d’effet

- Il n’est généralement pas possible d’évaluer la puissance d’un test dont l’hypothèse alternative est composite (car $H_1$ couvre une infinité de valeurs).

- On peut demander au praticien dans quelle mesure il pense qu’on s’éloigne de l’hypothèse nulle pour que la différence soit significative (d’un point de vue métier) : c’est ce qu’on nomme la **~={red}taille d’effet=~**.

- Cette pratique a notamment été introduite par **Cohen (1988)** (on parle parfois du « $d$ » de Cohen).

- On peut alors calculer la puissance du test relativement à cette taille d’effet spécifique.

- Il est souvent admis qu’une puissance de test satisfaisante doit être **supérieure à 80%** ($1 - \beta \geq 0.80$). 
    - On peut alors calculer la **taille d’échantillon minimale** ($n$) pour que la puissance de test soit effectivement supérieure à ce seuil, étant donné la taille d’effet fixée.
# Tests sur un paramètre
## Proportion
### Test considéré

- On teste l'hypothèse suivante (test unilatéral à droite) :
$$
\begin{cases}
H_0 : p = p_0 \\
H_1 : p > p_0
\end{cases}
$$
### Région critique

- La forme de la zone de rejet (région critique) est :
$$W = \{ \bar{X} - p_0 > c \}$$
On rejettera d’autant plus facilement $H_0$ que $\bar{x}$ sera plus élevée que $p_0$.

- La **statistique de test** utilisée ici est $\bar{X}$ (la moyenne ou fréquence empirique).

- Notons que la structure de la zone de rejet est donnée par l’hypothèse alternative $H_1$ : comme $H_1 : p > p_0$, on cherche uniquement les valeurs dans la queue supérieure de la distribution.
### Hypothèses et approximations

- **Petits échantillons ($n < 30$)** : On se base sur la **loi binomiale** $\mathcal{B}(n, p_0)$, qui est une loi discrète. Les calculs de probabilités se font alors via les combinaisons.

- **Grands échantillons** : Lorsque l'échantillon est suffisant et que les proportions ne sont pas extrêmes, on utilise l’approximation par une **loi normale**. On parle alors de résultat **asymptotique**.

- **Conditions de validité** (pour l'approximation normale) :
    - $n \geq 30$
    - $np_0 \geq 5$
    - $n(1 - p_0) \geq 5$

> [!NOTE] Intérêt
> L'utilisation d'une loi continue (normale) facilite grandement les calculs de seuils et de p-valeurs par rapport à la manipulation de sommes de probabilités binomiales.

### Résolution du test

- Sous $H_0$, dans les conditions posées précédemment, on peut considérer que la statistique de test centrée réduite suit une loi normale :
$$Z = \sqrt {n} \frac{\bar{X} - p_0}{\sqrt{p_0 (1 - p_0)}} = \frac{\bar{X} - p_0}{\sqrt{\frac{p_0 (1 - p_0)}{n}}} \approx \mathcal{N}(0, 1)$$

- On obtient alors la valeur critique $c$ :
$$c = \Phi_{1-\alpha} \sqrt{\frac{p_0 (1 - p_0)}{n}}$$
où $\Phi_{1-\alpha}$ désigne le quantile d’ordre $1 - \alpha$ de la loi $\mathcal{N}(0, 1)$.

- On appelle usuellement **test Z** tout test statistique dans lequel la statistique de test suit une loi normale sous $H_0$.
### Règle de décision

Les décisions prises au niveau de test $\alpha$ sont :

- **Le rejet de $H_0$** si :
$$\bar{x} > p_0 + \Phi_{1-\alpha} \sqrt{\frac{p_0 (1 - p_0)}{n}}$$

- **Le non-rejet de $H_0$** si :
$$\bar{x} \leq p_0 + \Phi_{1-\alpha} \sqrt{\frac{p_0 (1 - p_0)}{n}}$$
![[Pasted image 20260205101122.png]]
### Remarques

- **~={red}La constante est positive : $c \geq 0$.=~**
    - On retrouve la considération introductive selon laquelle si $\bar{x} \leq p_0$, on ne rejette pas l’hypothèse nulle (et donc l’ancien médicament est conservé).
    - Il en est encore ainsi si $\bar{x}$ est « trop peu supérieur » à $p_0$.
    - C’est si $\bar{x}$ est « significativement supérieur » à $p_0$ au niveau de test $\alpha$, d’au moins $\Phi_{1-\alpha} \sqrt{\frac{p_0(1-p_0)}{n}}$, que l’on rejette l’hypothèse nulle. Le nouveau médicament semble alors préférable à l’ancien.

- **~={red}La constante $c$ décroît lorsque la taille de l’échantillon $n$ croît.=~**
    - À $\alpha$ fixé, une même proportion observée $\bar{x} > p_0$, jugée non significativement supérieure à $p_0$ si elle est issue d’un échantillon d’assez petite taille, le deviendra nécessairement pour des tailles suffisamment élevées.
    - Autrement dit, pour rejeter $H_0$, il faut que :
    $$n > \Phi_{1-\alpha}^2 \frac{p_0(1-p_0)}{(\bar{x} - p_0)^2}$$
- **~={red}La constante $c$ décroît lorsque le niveau de test $\alpha$ croît.=~**
    - On sait en effet que le quantile $\Phi_{1-\alpha}$ décroît lorsque $\alpha$ croît (plus on accepte de risque, plus le seuil critique se rapproche de la moyenne).
    - À $n$ fixé, une même valeur de $\bar{x}$ peut conduire à :
        - **Rejeter l’hypothèse** si $\alpha$ est assez fort (on parle de test « peu sévère »).
        - **Ne pas la rejeter** si $\alpha$ est assez faible (on parle de test « sévère »).
### p-valeur

- On rejette $H_0$ au niveau de test $\alpha$ si :
$$\bar{x} > p_0 + \Phi_{1-\alpha} \sqrt{\frac{p_0 (1 - p_0)}{n}}$$

- Ce qui est mathématiquement équivalent à :
$$1 - \Phi \left( \frac{\bar{x} - p_0}{\sqrt{\frac{p_0 (1 - p_0)}{n}}} \right) < \alpha$$

- La **p-valeur** (pour ce test unilatéral à droite) vaut donc :
$$\text{p-valeur} = 1 - \Phi(z_{obs}) \quad \text{avec} \quad z_{obs} = \frac{\bar{x} - p_0}{\sqrt{\frac{p_0 (1 - p_0)}{n}}}$$

- **Règle de décision finale :**
    - On se fixe un niveau de test $\alpha$.
    - On calcule la p-valeur à partir des données observées.
    - On décide du :
        - **rejet de $H_0$** si $\text{p-valeur} < \alpha$
        - **non-rejet de $H_0$** si $\text{p-valeur} \geq \alpha$
![[Pasted image 20260205101450.png]]
### Cas du taux de guérison (Application numérique)

- **Le test :** On évalue l'efficacité d'un nouveau traitement :
$$
\begin{cases}
H_0 : p = 0.75 \\
H_1 : p > 0.75
\end{cases}
$$

- **Conditions de validité :** L'échantillon est suffisant pour l'approximation normale :
    - $n = 216 \geq 30$
    - $np_0 = 162 \geq 5$
    - $n(1 - p_0) = 54 \geq 5$

- **Paramètres du test ($\alpha = 5\%$) :**
    - Valeur critique (quantile) : $\Phi_{0.95} \simeq 1.64$
    - Seuil critique de proportion : $0.75 + 1.64 \sqrt{\frac{0.75 \times 0.25}{216}} \simeq 0.798$

- **Décision :**
    - La proportion observée est $\bar{x} = 0.773$.
    - Comme $0.773 \leq 0.798$, on **ne rejette pas $H_0$** au niveau de test $5\%$.

- **Calcul de la p-valeur :**
$$\text{p-valeur} = 1 - \Phi \left( \frac{0.773 - 0.75}{\sqrt{\frac{0.75 \times 0.25}{216}}} \right) \simeq 1 - \Phi(0.786) \simeq 0.216$$

- **Interprétation :**
    - Il faudrait accepter un risque $\alpha$ d'au moins **21,6 %** pour pouvoir rejeter $H_0$. 
    - En statistique, accepter de se tromper dans plus de 20 % des cas (rejeter l'innocence alors qu'il n'y a rien) est jugé beaucoup trop risqué et n'est jamais pratiqué.

- **Conclusion :**
    - Le laboratoire **ne peut pas conclure** (au niveau de test usuel de 5 %) que le nouveau médicament est meilleur que l'ancien. L'amélioration observée est trop faible par rapport à la taille de l'échantillon.
### Test alternatif (Test bilatéral)

- Si on considère cette fois le test alternatif suivant :
$$
\begin{cases}
H_0 : p = p_0 \\
H_1 : p \neq p_0
\end{cases}
$$

- On choisit comme **~={red}région critique=~** :
$$W = \{ |\bar{X} - p_0| > c \}$$

- La région critique intègre cette fois une **valeur absolue** car l'hypothèse $H_1$ regroupe les cas où $p > p_0$ ET les cas où $p < p_0$.

- La résolution mathématique conduit à :
$$c = \Phi_{1 - \frac{\alpha}{2}} \sqrt{\frac{p_0 (1 - p_0)}{n}}$$

- On utilise ici **$\Phi_{1 - \frac{\alpha}{2}}$** à la place de $\Phi_{1-\alpha}$ car le risque $\alpha$ est divisé en deux parties égales aux deux extrémités de la loi normale.

Les décisions prises au niveau de test $\alpha$ pour un test bilatéral sont :

- ~={red}**Le rejet de $H_0$**=~ si l'écart absolu est trop grand :
$$|\bar{x} - p_0| > \Phi_{1-\frac{\alpha}{2}} \sqrt{\frac{p_0 (1 - p_0)}{n}}$$

- ~={red}**Le non-rejet de $H_0$**=~ si l'écart est modéré :
$$|\bar{x} - p_0| \leq \Phi_{1-\frac{\alpha}{2}} \sqrt{\frac{p_0 (1 - p_0)}{n}}$$

- **Calcul de la p-valeur :** Dans le cas bilatéral, comme on s'intéresse aux deux directions, la p-valeur est doublée par rapport au cas unilatéral :
$$\text{p-valeur} = 2 \times P(Z > |z_{obs}|) = 2 \times (1 - \Phi(|z_{obs}|))$$
## Moyenne
### Hypothèses pour les tests sur la moyenne

Pour tester une moyenne $\mu$, on doit impérativement se trouver dans l'un des deux cas suivants :

1.  **Cas Gaussien** : On dispose d’un échantillon $(X_1, \dots, X_n)$ i.i.d. de loi normale $\mathcal{N}(\mu, \sigma^2)$. 
    - *Ici, le test est exact quelle que soit la taille de $n$.*
2.  **Cas Grand Échantillon ($n \geq 30$)** : On dispose d’un échantillon i.i.d. suivant une loi quelconque d'espérance $\mu$ et de variance $\sigma^2$.
    - *On dispose alors d’un résultat **asymptotique** grâce au Théorème Central Limite.*

> [!CAUTION] Attention
> En dehors de ces deux cas de figure (petit échantillon non normal), il n’existe pas de test paramétrique standard sur la moyenne. Il faut alors se tourner vers des tests non-paramétriques.

### Différents tests sur la moyenne

On considère les trois types de tests suivants, selon l'objectif de l'étude :

1. **Test unilatéral à droite** : 
$$\begin{cases} H_0 : \mu = \mu_0 \\ H_1 : \mu > \mu_0 \end{cases}$$
*(On cherche à savoir si la moyenne a augmenté)*

2. **Test unilatéral à gauche** : 
$$\begin{cases} H_0 : \mu = \mu_0 \\ H_1 : \mu < \mu_0 \end{cases}$$
*(On cherche à savoir si la moyenne a diminué)*

3. **Test bilatéral** : 
$$\begin{cases} H_0 : \mu = \mu_0 \\ H_1 : \mu \neq \mu_0 \end{cases}$$
*(On cherche à savoir si la moyenne est différente de $\mu_0$)*

- C’est le **test 3 (bilatéral)** qui est considéré dans le second exemple introductif (celui sur le dosage de la solution par exemple, où l'on craint aussi bien le surdosage que le sous-dosage).


- On pourrait être tenté d'utiliser $\bar{X} - \mu_0$ (ou simplement $\bar{X}$) comme statistique de test. Malheureusement, sa loi dépend du paramètre $\sigma$ (l'écart-type de la population), qui est **inconnu** en pratique.

- C’est pourquoi on utilise la statistique de test $T$, qui substitue l'écart-type théorique par l'écart-type empirique corrigé $S'$ :
$$T = \sqrt{n} \frac{\bar{X} - \mu_0}{S'}$$

- **Sous $H_0$ :**
	- Cette statistique suit une **loi de Student** à $n - 1$ degrés de liberté :
$$T \sim \mathcal{T}(n - 1)$$

Les régions critiques $W$ et les p-valeurs dépendent de la nature de l'hypothèse alternative $H_1$. On note $t_{n-1, 1-\alpha}$ le quantile d'ordre $1-\alpha$ de la loi de Student à $n-1$ degrés de liberté.

| Type de Test          | Hypothèse $H_1$  | Région Critique $W$ (Rejet de $H_0$)                | p-valeur                                 |
| :-------------------- | :--------------- | :-------------------------------------------------- | :--------------------------------------- |
| **1. Unilatéral (+)** | $\mu > \mu_0$    | $\{T > t_{n-1, 1-\alpha}\}$                         | $P(T_{n-1} \geq t_{obs})$                |
| **2. Unilatéral (-)** | $\mu < \mu_0$    | $\{T < -t_{n-1, 1-\alpha}\}$                        | $P(T_{n-1} \leq t_{obs})$                |
| **3. Bilatéral**      | $\mu \neq \mu_0$ | $\{\lvert T \rvert > t_{n-1, 1-\frac{\alpha}{2}}\}$ | $P( \lvert T_{n-1} \rvert \geq t_{obs})$ |

Où la statistique observée est : $t_{obs} = \sqrt{n} \frac{\bar{x} - \mu_0}{s'}$.
### Cas de la consommation d’essence (Application numérique)

- **Le test :** On cherche à vérifier si la consommation moyenne est différente de la valeur de référence $\mu_0 = 31$.
$$
\begin{cases}
H_0 : \mu = 31 \\
H_1 : \mu \neq 31
\end{cases}
$$

- **Données de l'échantillon :**
    - Taille : $n = 128$
    - Moyenne observée : $\bar{x} = 31.45$
    - Écart-type empirique : $s' = 2.16$

- **Paramètres du test ($\alpha = 5\%$) :**
    - Degrés de liberté : $df = n - 1 = 127$
    - Valeur critique (quantile) : $t_{n-1,1-\frac \alpha2} = t_{127, 0.975} \simeq 1.98$

- **Calcul de la statistique de test ($t_{obs}$) :**
$$|t_{obs}| = \left| \sqrt{128} \frac{31.45 - 31}{2.16} \right| \simeq 2.35$$

- **Décision :**
    - Comme $|t_{obs}| = 2.35 > 1.98$, la statistique tombe dans la zone de rejet.
    - On **rejette $H_0$** au niveau de test 5%.

- **Calcul de la p-valeur :**
Pour un test bilatéral, on double la probabilité de la queue de distribution :
$$\text{p-valeur} = 2 \times P(T(127) \geq 2.35) \simeq 0.02$$

- **Interprétation des seuils :**
    - **À $\alpha = 5\%$** : On rejette $H_0$ car $0.02 < 0.05$. Le résultat est dit "significatif".
    - **À $\alpha = 1\%$** : On **ne rejette pas** $H_0$ car $0.02 \geq 0.01$. Le résultat n'est pas "très significatif".

- **Vérification par les quantiles ($\alpha = 1\%$) :**
    - Le seuil critique pour 1% est $t_{127, 0.995} \simeq 2.62$.
    - Comme notre statistique $|t_{obs}| = 2.35$ est inférieure à $2.62$, on confirme le non-rejet à ce niveau de sévérité.

> [!ABSTRACT] Conclusion métier
> La différence de consommation est réelle au seuil standard de 5%, mais elle n'est pas assez flagrante pour être affirmée avec une certitude de 99%.