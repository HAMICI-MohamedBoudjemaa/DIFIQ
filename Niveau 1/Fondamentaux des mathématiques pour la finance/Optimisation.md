
# 1. Rappel sur les matrices

Dans tout ce chapitre, $n$, $p$, $q$ désignent des entiers naturels non nuls.

## I - Notion de matrice et vocabulaire

> [!abstract] Définition 1
> Une matrice $A$ à $n$ lignes et $p$ colonnes est un tableau défini par $n \times p$ éléments de $\mathbb{R}$ notés $a_{i,j}$ pour $1 \le i \le n$ et $1 \le j \le p$.
> - $a_{i,j}$ est le coefficient d'indice $(i, j)$ (ligne $i$, colonne $j$).
> - La taille (ou format) est notée $(n, p)$.
> - L'ensemble des matrices de taille $(n, p)$ est noté $\mathcal{M}_{n,p}(\mathbb{R})$.

### Représentation générale
$$A = \begin{pmatrix} 
a_{1,1} & a_{1,2} & \dots & a_{1,p} \\
a_{2,1} & a_{2,2} & \dots & a_{2,p} \\
\vdots & \vdots & a_{i,j} & \vdots \\
a_{n,1} & a_{n,2} & \dots & a_{n,p}
\end{pmatrix} \in \mathcal{M}_{n,p}(\mathbb{R})$$



### Vocabulaire spécifique (Définition 2)
- **Matrice carrée :** Si $n = p$, noté $\mathcal{M}_n(\mathbb{R})$.
- **Matrice ligne :** Taille $(1, p)$.
- **Matrice colonne :** Taille $(n, 1)$.
- **Matrice triangulaire supérieure :** $a_{i,j} = 0$ si $i > j$.
- **Matrice triangulaire inférieure :** $a_{i,j} = 0$ si $i < j$.
- **Matrice diagonale :** $a_{i,j} = 0$ si $i \neq j$. Notée $\text{diag}(a_{1,1}, \dots, a_{n,n})$.
- **Matrice symétrique :** $a_{i,j} = a_{j,i}$ pour tout $(i, j)$.
- **Matrice nulle ($0_{n,p}$) :** Tous les coefficients sont nuls.
- **Matrice Identité ($I_n$) :** Matrice carrée diagonale avec des $1$ sur la diagonale.

---

## II - Opérations de base sur les matrices

### II.1 - Addition et multiplication par un scalaire

> [!info] Définition 3
> - **Addition :** Si $A, B \in \mathcal{M}_{n,p}(\mathbb{R})$, alors $C = A + B$ est définie par $c_{i,j} = a_{i,j} + b_{i,j}$.
> - **Multiplication par un réel :** Si $\lambda \in \mathbb{R}$, alors $\lambda A$ est la matrice dont chaque coefficient est multiplié par $\lambda$.

> [!warning] Remarque importante
> Il est possible d'additionner deux matrices **uniquement** lorsqu'elles ont les mêmes dimensions.

### II.2 - Multiplication matricielle

> [!important] Définition 4
> Soient $A \in \mathcal{M}_{n,p}(\mathbb{R})$ et $B \in \mathcal{M}_{p,q}(\mathbb{R})$. Le produit $AB$ est une matrice de taille $(n, q)$ dont les coefficients sont :
> $$(AB)_{i,j} = \sum_{k=1}^{p} a_{i,k}b_{k,j}$$



**Méthode visuelle :**
Le coefficient $(i, j)$ du produit $AB$ est le produit scalaire de la $i$-ème ligne de $A$ par la $j$-ème colonne de $B$.

---

## III - Exercices d'application

### Exercice 1 (Extraits)
1. **Appartenance :**
   - $A = \begin{pmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 & 8 & 9 \end{pmatrix} \in \mathcal{M}_3(\mathbb{R})$
   - $B = \begin{pmatrix} 1 & -1 & e \\ \pi & \sqrt{2} & 0,2 \end{pmatrix} \in \mathcal{M}_{2,3}(\mathbb{R})$
   - $C = \begin{pmatrix} 1 \\ 2 \\ 3 \end{pmatrix} \in \mathcal{M}_{3,1}(\mathbb{R})$ (Vecteur colonne)

2. **Construction :** Écrire $M = (i-j)$ pour $1 \le i \le 3$ et $1 \le j \le 4$.
$$M = \begin{pmatrix} 
0 & -1 & -2 & -3 \\
1 & 0 & -1 & -2 \\
2 & 1 & 0 & -1 
\end{pmatrix}$$

### Exercice 4 (Calculs de produits)
Soient $E = \begin{pmatrix} 2 & 1 \\ 0 & 0 \end{pmatrix}$ et $D = \begin{pmatrix} 1 & -2 \\ -2 & 4 \end{pmatrix}$.
1. **Calculer $ED$ :**
   $ED = \begin{pmatrix} 2(1)+1(-2) & 2(-2)+1(4) \\ 0(1)+0(-2) & 0(-2)+0(4) \end{pmatrix} = \begin{pmatrix} 0 & 0 \\ 0 & 0 \end{pmatrix}$
2. **Calculer $DE$ :**
   $DE = \begin{pmatrix} 1(2)-2(0) & 1(1)-2(0) \\ -2(2)+4(0) & -2(1)+4(0) \end{pmatrix} = \begin{pmatrix} 2 & 1 \\ -4 & -2 \end{pmatrix}$

> [!danger] Attention
> On remarque que $ED \neq DE$. La multiplication matricielle n'est **pas commutative**.

![[Pasted image 20260207174611.png]]

---
## II.3 - Propriétés du produit matriciel

> [!abstract] Proposition 1
> 1. **Associativité :** $(AB)C = A(BC)$
> 2. **Distributivité à gauche :** $A(B + C) = AB + AC$
> 3. **Distributivité à droite :** $(A + B)C = AC + BC$
> 4. **Produit externe :** $(\lambda A)B = \lambda(AB) = A(\lambda B)$
> 5. **Élément neutre :** $A \cdot I_p = A$ et $I_n \cdot A = A$
> 6. **Non-commutativité :** En général, $AB \neq BA$
> 7. **Pas de propriété de produit nul :** On peut avoir $AB = 0$ alors que $A \neq 0$ et $B \neq 0$.

> [!example] Exercice 5
> Soit $M = \begin{pmatrix} -1 & -3 \\ 2 & 4 \end{pmatrix}$. 
> Vérifier que $M^2 - 3M + 2I_2 = 0_{2,2}$ puis factoriser l'expression.

---

# III - Puissances de matrice

> [!info] Définition 5
> Soit $k \in \mathbb{N}$ et $A \in \mathcal{M}_n(\mathbb{R})$.
> - $A^k = A \times \dots \times A$ ($k$ fois)
> - Par convention, $A^0 = I_n$

### Propriétés de calcul
Si $A$ et $B$ sont deux matrices qui **commutent** ($AB = BA$), alors :
- $(AB)^k = A^k B^k$
- $(A - B)(A + B) = A^2 - B^2$
- **Binôme de Newton :** $(A + B)^n = \sum_{i=0}^{n} \binom{n}{i} A^i B^{n-i}$

> [!warning] Attention
> Ces formules sont **fausses** si $A$ et $B$ ne commutent pas.



---

# IV - Inverse d’une matrice

> [!abstract] Définition 6
> Une matrice carrée $A \in \mathcal{M}_n(\mathbb{R})$ est dite **inversible** s'il existe une matrice $A^{-1}$ telle que :
> $$AA^{-1} = I_n = A^{-1}A$$
> L'ensemble des matrices inversibles est noté $GL_n(\mathbb{R})$.

### Propriétés de l'inverse
1. **Unicité :** Si elle existe, l'inverse est unique.
2. **Inverse de l'inverse :** $(A^{-1})^{-1} = A$
3. **Inverse d'un produit :** $(AB)^{-1} = B^{-1}A^{-1}$ (Attention à l'ordre !)

### Simplifications
Si $C$ est inversible ($C \in GL_n(\mathbb{R})$) :
- $CA = B \iff A = C^{-1}B$
- $AC = B \iff A = BC^{-1}$

---

## Cas particulier : Matrices 2x2

> [!important] Proposition 5 (Calcul de l'inverse 2x2)
> Soit $A = \begin{pmatrix} a & b \\ c & d \end{pmatrix}$.
> 1. Si $ad - bc = 0$, $A$ n'est pas inversible.
> 2. Si $ad - bc \neq 0$, $A$ est inversible et :
> $$A^{-1} = \frac{1}{ad - bc} \begin{pmatrix} d & -b \\ -c & a \end{pmatrix}$$



---

## Exercices d'entraînement (Extraits)

### Exercice 6
Calculer les puissances successives de $M = \begin{pmatrix} 0 & 0 & 0 & 0 \\ 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \end{pmatrix}$.
*(Indice : Il s'agit d'une matrice nilpotente, ses puissances finissent par s'annuler).*

### Exercice 8.2
Soit $A \in \mathcal{M}_p(\mathbb{R})$ et $P \in GL_p(\mathbb{R})$.
Montrer par récurrence que pour tout $n \in \mathbb{N}$ :
$$(P^{-1}AP)^n = P^{-1}A^n P$$

> [!tip] Remarque
> Cette formule est fondamentale pour le calcul des puissances de matrices via la diagonalisation.

---
titre: Transposition et Optimisation
matière: Fondamentaux Mathématiques pour la Finance
auteur: R. Hatami / DIFIQ
année: 2024
tags:
  - mathématiques
  - algèbre_linéaire
  - optimisation
  - points_critiques
---

# V - Transposition et matrices symétriques

> [!abstract] Définition
> Soit $A = (a_{i,j}) \in \mathcal{M}_{n,p}(\mathbb{R})$. La **transposée** de $A$, notée $^tA$, est la matrice de taille $(p, n)$ obtenue en échangeant les lignes et les colonnes :
> $$\forall (i, j), \quad a'_{i,j} = a_{j,i}$$



### Proposition 6 : Propriétés de la transposition
1. **Involution :** $^t(^tA) = A$
2. **Inverse du produit :** $^t(AB) = ^tB \cdot ^tA$ (Attention au renversement de l'ordre)
3. **Linéarité :** $^t(\lambda A + B) = \lambda ^tA + ^tB$
4. **Inverse et transposition :** $^t(A^{-1}) = (^tA)^{-1}$
5. **Matrices symétriques :** Une matrice est symétrique si $^tA = A$. L'ensemble est noté $\mathcal{S}_n(\mathbb{R})$.

---

# 2. Optimisation

## 2.1 Cas particulier important
Toute fonction continue sur un **fermé borné** de $\Omega \subset \mathbb{R}^n$, à valeurs dans $\mathbb{R}$, admet un maximum global et un minimum global sur $\Omega$.

*Dans la suite, nous considérons des fonctions définies sur un **ouvert** $\Omega$ de $\mathbb{R}^n$.*

## 2.2 Condition nécessaire du premier ordre

> [!info] Définition : Point critique
> Soit $f$ une fonction admettant des dérivées partielles d'ordre 1. Le point $A$ est un **point critique** de $f$ si son gradient est nul :
> $$\nabla f(A) = 0 \iff \forall i \in \{1, \dots, n\}, \quad \frac{\partial f}{\partial x_i}(A) = 0$$

> [!important] Théorème (Condition Nécessaire)
> Si $f$ (de classe $\mathcal{C}^1$) admet un extremum local ou global en un point $A$ d'un ouvert $\Omega$, alors **$A$ est un point critique** de $f$.

*Note : La réciproque est fausse (existence de points selles).*

## 2.3 Point selle (ou point col)

> [!abstract] Définition
> On appelle **point selle** tout point critique de $f$ en lequel la fonction n'admet pas d'extremum (ni maximum, ni minimum).



### Exemple visuel
En dimension 2, la surface ressemble à une selle de cheval ou à un col de montagne : elle "monte" dans une direction et "descend" dans une autre, bien que le plan tangent y soit horizontal.

![[Pasted image 20260207175048.png]]

---

---
titre: Optimisation - Conditions Suffisantes et Méthodologie
chapitre: 5
matière: Fondamentaux Mathématiques pour la Finance
auteur: R. Hatami / DIFIQ
année: 2024
tags:
  - mathématiques
  - optimisation
  - Hessienne
  - extrema
---

# 2.4 Condition suffisante (Étude de la Hessienne)

Une fois un point critique $A$ identifié (où $\nabla f(A) = 0$), on étudie la **matrice Hessienne** $\nabla^2 f(A)$ pour déterminer la nature de ce point.

> [!important] Théorème des extrema liés aux valeurs propres
> Soit $f$ de classe $\mathcal{C}^2$ sur un ouvert $\Omega$ et $A$ un point critique :
> - **Minimum local :** Si toutes les valeurs propres de $\nabla^2 f(A)$ sont **strictement positives**.
> - **Maximum local :** Si toutes les valeurs propres de $\nabla^2 f(A)$ sont **strictement négatives**.
> - **Point Selle (Col) :** Si $\nabla^2 f(A)$ possède au moins une valeur propre strictement positive **et** au moins une valeur propre strictement négative.
> - **Cas douteux :** Si au moins une valeur propre est nulle (et les autres de même signe), le théorème ne permet pas de conclure.



---

# 3. Méthode pour déterminer les extrema

## 3.1 Une méthode en deux étapes

1. **Recherche des points critiques :** - Calculer le vecteur gradient $\nabla f$.
   - Résoudre le système d'équations $\nabla f(x, y, z) = 0$.
2. **Examen des points critiques :** - Calculer les dérivées partielles d'ordre 2 pour former la matrice Hessienne.
   - Calculer les valeurs propres de cette matrice en chaque point critique.
   - Appliquer le théorème de la condition suffisante.

---

## 3.2 Exemple d'application détaillé

Soit $f$ définie sur $\mathbb{R} \times \mathbb{R}^* \times \mathbb{R}$ par :
$$f(x, y, z) = \frac{xz}{y} - z - x + \frac{1}{2}y^2$$

### Étape 1 : Recherche du point critique
On calcule les dérivées partielles d'ordre 1 :
- $\partial_1 f(x, y, z) = \frac{z}{y} - 1$
- $\partial_2 f(x, y, z) = -\frac{xz}{y^2} + y$
- $\partial_3 f(x, y, z) = \frac{x}{y} - 1$

En résolvant $\nabla f(x, y, z) = 0$, on obtient l'unique point critique : **$A = (1, 1, 1)$**.

### Étape 2 : Examen du point critique $A$
On calcule la matrice Hessienne $\nabla^2 f(1, 1, 1)$ en utilisant le théorème de Schwarz pour les dérivées croisées :

$$\nabla^2 f(1, 1, 1) = \begin{pmatrix} 
0 & -1 & 1 \\
-1 & 3 & -1 \\
1 & -1 & 0 
\end{pmatrix}$$



**Calcul des valeurs propres :**
Le polynôme caractéristique est $P(\lambda) = (1 + \lambda)(1 - 4\lambda + \lambda^2)$.
Les racines (valeurs propres) sont :
- $\lambda_1 = -1$ (négative)
- $\lambda_2 = 2 - \sqrt{3} \approx 0,27$ (positive)
- $\lambda_3 = 2 + \sqrt{3} \approx 3,73$ (positive)

> [!danger] Conclusion
> La matrice possède des valeurs propres de signes opposés. Le point $A(1, 1, 1)$ est donc un **point selle** (ou point col). La fonction ne possède pas d'extremum local en ce point.---
titre: Travaux Dirigés - Matrices et Optimisation
matière: Fondamentaux Mathématiques pour la Finance
auteur: R. Hatami / DIFIQ
année: 2024
tags:
  - exercices
  - matrices
  - optimisation
  - hessienne
---

# 4. Travaux Dirigés

---

## Exercice 1 : Produit de matrices
Soient les matrices suivantes :
$$A = \begin{pmatrix} 1 & 2 & 3 \\ -1 & -2 & 5 \end{pmatrix} \quad \text{et} \quad B = \begin{pmatrix} 1 & 2 & 0 & 2 \\ 2 & 3 & -1 & 4 \\ -1 & -1 & 7 & 0 \end{pmatrix}$$

1. Peut-on calculer le produit $AB$ ? Si oui, effectuer le calcul.
2. Peut-on calculer le produit $BA$ ? Justifier.

---

## Exercice 2 : Matrice inverse
Soit la matrice $A = \begin{pmatrix} 1 & 0 & 1 \\ 0 & 1 & 0 \\ -1 & 0 & 1 \end{pmatrix}$.

a) La matrice $A$ est-elle inversible ?
b) Si oui, calculer sa matrice inverse $A^{-1}$.
c) En déduire la résolution du système suivant :
$$\begin{cases} x + z = 1 \\ y = 5 \\ -x + z = -3 \end{cases}$$

> [!tip] Rappel
> Résoudre le système revient à résoudre l'équation matricielle $AX = Y$ où $X = \begin{pmatrix} x \\ y \\ z \end{pmatrix}$. La solution est $X = A^{-1}Y$.

---

## Exercice 3 : Valeurs propres
Déterminer les valeurs propres des matrices suivantes :
- $A = \begin{pmatrix} 0 & 1 & 1 \\ 1 & 0 & 1 \\ 1 & 1 & 0 \end{pmatrix}$
- $B = \begin{pmatrix} -3 & 1 \\ 1 & 0 \end{pmatrix}$



---

## Exercice 4 : Dérivées partielles et Hessienne
Soit la fonction $f$ définie par :
$$f(x, y) = x^2y - y^2x$$

1. Calculer les dérivées partielles d'ordre 1 (le gradient).
2. Calculer les dérivées partielles d'ordre 2.
3. En déduire la **matrice Hessienne** $\nabla^2 f(x, y)$.

---

## Exercice 5 : Extremums locaux
Soit la fonction définie par :
$$f(x, y) = x^2y^2 + x^2 + y^2 + 4xy$$

1. Déterminer les points critiques de $f$ (résoudre $\nabla f(x, y) = 0$).
2. Pour chaque point critique, utiliser la matrice Hessienne et ses valeurs propres pour déterminer s'il s'agit d'un maximum local, d'un minimum local ou d'un point selle.