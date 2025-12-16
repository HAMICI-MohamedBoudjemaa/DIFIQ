- Le principe est de partir d'une partition arbitraire puis de l'améliorer itérativement jusqu'à **convergence**
- Il existe plusieurs variantes de K-means qui nécessitent toutes un chois **a priori du nombre de classes**
- On cherche une partition $\mathcal P = \{C_1,...,C_k\}$ qui permet de **minimiser l'inertie intra-classes**
$$\sum_{ k = 1 }^K \sum_{i  \ in C_k} \omega_i d^2(i,g_$k)$$
- Poids de la classe : $\mu_k = \sum_{i \in C_k} \omega_i$ 
- Centre de gravité de la classe : $g_k = \frac {1}{\mu_k} \sum_{i \in C_k} \omega_i x_i$ 
- Il n'existe pas de solution explicite au problème de K-means

## Algorithme de Lloyd / Forgy
1. **Initialisation des centres de classe** : Choisir $K$ centres de classes dans l'espace des individus
2. **Boucle (*à réitérer jusqu'à convergence*)** :
	1. **Affectation des points** : Affecter chacun des $n$ individus au centre de classe le plus proche
	2. **Recalcul des centres de classe** : Remplacer les $K$ centres de classes par les $K$ centres de gravité des classes ainsi constituées
	![[Kmeans.gif]]
## Algorithme de Mac Queen
1. **Initialisation des centres de classe** : 
	1. Choisir $K$ centres de classes dans l'espace des individus
	2. Affecter chacun des $n$ individus à la classe dont le centre lui est le plus proche
	3. Remplacer les anciens $K$ centres de classes par les nouveaux
2. **Boucle (*à réitérer jusqu'à convergence*)** : 
   Pour $i \in \{1,...,n\}$
	a) **Affectation des points** : Affecter l'individu $i$ à la classe dont le centre lui est le plus proche
	b) **Recalcul des centres de classe** : Si $i$ change de classe, recalculer les centres de classes des deux classes modifiées
## Quelques choix
Voici quelques choix pour choisir/définir les éléments suivants
- **Nombre de classes** :
	- A partir d'une **connaissance à priori**
	- A la suite d'une **CAH**
	- A l'aide d'une règle du *coude*, à partir de différents *K-means* (de 2 à $K_{max}$ classes)
- **Métrique** : 
	- Distance euclidienne
- **Centres de classes** :
	- **K-means** : On considère les centres de gravité des classes, les centroïdes
	- **K-medoids** : On considère les médoïdes \[élément le plus central de la classe] des classes, ce qui rend la méthode plus robuste aux outliers
$$Médoïde = arg \space \underset {i \in C_k}{min} \underset {j \in C_k, j \ne i}{\sum} \omega_j d^2(i,j)$$
- **Centres de classes initiaux** :
	- $K$ individus **choisis au hasard**
	- $K$ individus **très éloignés les uns des autres : *K-means++***
	- $K$ individus **choisis au hasard parmi les classes obtenus par une CAH préalable**
## Avantages et Inconvénients
### Avantages
- Concept simple
- Complexité en $O(NKn)$ avec $N$ nombre d'itérations
### Inconvénients
- Nombre de classes **à définir à priori**
- **Résultat très variable en fonction des centres de classes initiaux** choisis (ainsi que de l'ordre de traitement des individus sur certains algorithmes comme *Mac Queen* et *Hartigan & Wong*)
- Classes constituées à partir de **centres de classes fictifs, non observés** (centres de gravité).
- Méthode **sensible aux outliers** (soluble via les algorithmes *PAM* et *CLARA*)