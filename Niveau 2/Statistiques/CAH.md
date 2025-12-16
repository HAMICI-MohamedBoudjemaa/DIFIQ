## Méthode
La **Classification Ascendante Hiérarchique** produit une suite de partitions emboîtées, à $\{n, n-1,..., 1\}$ classes par regroupements successifs.
On obtient une partition à $K$ classes en agrégeant les deux classes les plus proches de la partition à $K+1$ classes, au sens d'une **distance ultramétrique** $\nabla$ à définir
## Résultat
On obtient une hiérarchie des partitions indicée (en général par la distance $\nabla$), présentable sous forme de **dendogramme** (*arbre hiérarchique*)
## Algorithme
### 1. Initialisation ($K = n$)
On considère la partition $O_n = \{\{1\},...,\{n\}\}$ 
### 2. Agrégation ($K \in \{n-1,..,1\}$)
On construit $P_K$ en agrégeant les deux classes de $P_{K+1}$ qui ont la plus faible distance $\nabla$
#### Stratégies d'agrégation
Considérer une distance ultramétrique pour $\nabla$ est une condition nécessaire pour obtenir une hiérarchie.
Le choix de la stratégie d'agrégation conditionne fortement les résultats.
Il n'existe pas de règle explicite pour choisir la bonne stratégie, il faut essayer et observer les résultats.
- Single linkage (saut minimal)
	- $\nabla_{(C_1,C_2)} = \underset {i_1 \in C_1, i_2 \in C_2}{min} d(i_1,i_2)$ 
- Complete linkage (saut maximal)
	- $\nabla_{(C_1,C_2)} = \underset {i_1 \in C_1, i_2 \in C_2}{max} d(i_1,i_2)$ 
- Average linkage (distance moyenne)
	- $\nabla_{(C_1,C_2)} = \frac {1}{Card(C_1)Card(C_2)} \underset {i_1 \in C_1, i_2 \in C_2}{\sum} d(i_1,i_2)$ 
- Centroids linkage
	- $\nabla_{(C_1,C_2)} = d(g_{C_1},g_{C_2})$
![[Pasted image 20251215190846.png]]

- Ward Linkage : *adoptée très fréquemment en espace euclidien*
	- $\nabla_{(C_1,C_2)} = \frac {\mu_{C_1}\mu_{C_2}}{\mu_{C_1} + \mu_{C_2}} d^2(g_{C_1},g_{C_2})$
	- Où 
		- $\mu_{C_1}$ et $\mu_{C_2}$ sont respectivement les poids de $C_1$ et $C_2$
		- $g_{C_1}$ et $g_{C_2}$ sont respectivement les centres de gravité de $C_1$ et $C_2$
		- $d$ est la distance euclidienne
	- Avec la méthode de Ward, on agrège à chaque itération les classes dont l'**agrégation fait perdre le moins d'inertie inter-classe**

## Hiérarchie
On dit que H est une **hiérarchie** d'un espace $O$ si :
- $O \in H$
- $\forall i \in O : \{i\} \in H$
- $\forall (C_1, C_2) \in H^2 : C_1 \cap C_2 \in \{\emptyset, C_1, C_2\}$
==Autrement dit, une hiérarchie doit contenir tous les individus isolément ET en tant qu'ensemble. Les classes d'une hiérarchie sont soit disjointes, soit incluses l'une dans l'autre==

### Indice
L'**Indice** d'une hiérarchie $H$ et une fonction $h:H \rightarrow \mathbb R^+$ qui vérifie :
- $\forall C \in H : h(C) = 0 \iff C = \{\{1\},...,\{n\}\}$
- $\forall (C_1, C_2) \subset H^2 : C_1 \in C_2 \implies h(C1) \le h(C2)$
Une hiérarchie indicée peut se représenter sous forme de **dendogramme**
#### Propriétés des indices
- **Non-inversion** : La réunion de deux classes (non incluses l'une dans l'autre) présente toujours un indice d'agrégation plus grand que le maximum d'indice d'agrégation de chacune
- **Convexité** : Si les objets à classer sont dans un espace euclidien, les enveloppes convexes des partitions générées par la CAH sont d'intersection vide (*convex admissibility*)
- **Invariance par réplication** : Si certains objets sont répliqués, les frontières des partitions générées par la CAH ne changement pas (*point proportional admissibility*)
- **Monotonie** : Une transformation monotone des dissimilarités entre objets ne change pas la CAH (*monotone admissibility*)

| Indice           | Non-inversion | Convexité | Rélication | Monotonie |
| ---------------- | ------------- | --------- | ---------- | --------- |
| Single linkage   | Oui           | Non       | Oui        | Oui       |
| Complete linkage | Oui           | Non       | Oui        | Oui       |
| Average linkage  | Oui           | Non       | Non        | Non       |
| Ward linkage     | Oui           | Oui       | Non        | Non       |
### Dendogramme
Le **dendogramme** représente les agrégations successives (jusqu'à une seule classe) sous forme d'arbre binaire.
On parle de **racine, feulles, branches et noeuds**.
La hauteur d'une branche est égale à l'indice de la hiérarchie, elle traduit la difficulté pour deux classes à être réunies.
On peut comptabiliser le nombre de classes retenues en coupant l'arbre, *le but étant de couper lors d'un saut important*
On cherche a identifier un ***"coude"*** dans les indices.
### Exemple
![[CAH_Iterations.gif]]![[CAH_Iterations2.gif]]![[Pasted image 20251216122845.png]]![[Pasted image 20251216122905.png]]
## Avantages et Inconvénients
### Avantages
- Pas nécessaire de fixer un nombre de classes à priori
- Possible d'utiliser différentes métriques et stratégies d'agrégation
### Inconvénients
- Pour un nombre de classes donné $K$, on peut être loin de la partition optimale, surtout si le nombre de liaisons $n-K$ est élevé
- Complexité en $O(n^2 ln(n))$ très élevée