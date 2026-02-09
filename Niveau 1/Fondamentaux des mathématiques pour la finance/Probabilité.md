# Cours de Probabilités — Partie 1

## Chapitre I : Espaces probabilisés

---

## 1. Ensemble fondamental et évènements

### Définition — Expérience aléatoire
Une **expérience aléatoire** est une expérience qui, répétée dans les mêmes conditions, ne donne pas toujours le même résultat.

### Exemples
- Tirer une carte au hasard dans un jeu de 52 cartes.
- Compter le nombre de particules émises par une source radioactive entre les instants 0 et t.
- Mesurer la distance au centre du point d’impact d’une fléchette sur une cible.

---

### Définition — Ensemble fondamental
L’**ensemble fondamental** est l’ensemble de tous les résultats possibles d’une expérience aléatoire.  
On l’appelle aussi **univers** et on le note généralement **Ω**.

Il peut être :
- fini ou infini
- dénombrable ou non dénombrable

### Exemples
- Jeu de cartes : ensemble fini représentant les 52 tirages possibles.
- Ω = {0,1,2,3,...} = ℕ : ensemble infini dénombrable.
- Intervalle `[0,a]` : ensemble infini non dénombrable (continu).

---

### Définition — Évènement
Un **évènement** est un sous-ensemble de Ω.  
Les éléments de Ω peuvent être considérés comme des **évènements élémentaires**.

👉 La notion d’évènement est fondamentale en probabilités.

### Exemples
- A : « tirer un pique » → ensemble de 13 cartes.
- B : « obtenir un nombre pair » → `{0,2,4,...}`.

---

## 2. Opérations sur les évènements

### Identités
- $A \cup \varnothing = A$ (neutre pour l’union)
- $A \cap \varnothing = \varnothing$ (absorbant pour l’intersection)
- $A \cup Ω = Ω$
- $A \cap Ω = A$

### Inclusion
Si $A \subset B$ alors :
- $A \cap B = A$
- $A \cup B = B$

### Complémentarité
- $A \cup A^c = Ω$
- $A \cap A^c = \varnothing$

On dit que **A et son complément forment une partition de Ω**.

### Lois de De Morgan
- $(A \cup B)^c = A^c \cap B^c$
- $(A \cap B)^c = A^c \cup B^c$
- $(A^c)^c = A$

---

## 3. Fonction probabilité

Avant la réalisation d’une expérience aléatoire, on ne sait pas si un évènement va se produire.  
La probabilité mesure les chances qu’il se réalise.

### Définition
Une probabilité est une application :

$$
P : A \rightarrow [0,1]
$$

qui vérifie les **axiomes de Kolmogorov (1933)** :

1. $P(Ω) = 1$ (évènement certain)
2. Si A et B sont disjoints :  
   $$
   P(A \cup B) = P(A) + P(B)
   $$
3. **σ-additivité** pour une famille d’évènements disjoints.

On appelle **(Ω, A, P)** un **espace probabilisé**.

---

### Tribu (σ-algèbre)
On suppose que l’ensemble des évènements A vérifie :

- $Ω \in A$
- Si $A \in A$ alors $A^c \in A$
- Stable par unions finies ou dénombrables.

---

## Propriétés importantes

- $P(A^c) = 1 - P(A)$
- $P(\varnothing) = 0$
- $P(A \cup B) = P(A) + P(B) - P(A \cap B)$

---

### Formule de Poincaré (inclusion-exclusion)

Pour plusieurs évènements :

$$
P(A_1 \cup ... \cup A_n)
= \sum P(A_i)
- \sum P(A_i \cap A_j)
+ \sum P(A_i \cap A_j \cap A_k)
- ...
$$

---

## 4. Probabilité conditionnelle et indépendance

### Définition — Probabilité conditionnelle
Pour deux évènements A et B avec $P(B) > 0$ :

$$
P(A|B) = \frac{P(A \cap B)}{P(B)}
$$

👉 Interprétation : on calcule la probabilité de A **en supposant que B est déjà réalisé**.

La connaissance de B réduit l’univers des possibles à B.

---

### Théorème de multiplication
$$
P(A \cap B) = P(A|B) \times P(B)
$$

---

### Formule des probabilités totales
Si $A_1, A_2, ..., A_n$ forment une partition de Ω :

$$
P(B) = \sum P(B|A_i) P(A_i)
$$

Cas particulier avec A et $A^c$ :

$$
P(B) = P(B|A)P(A) + P(B|A^c)P(A^c)
$$

👉 Permet de calculer une probabilité à partir de toutes les causes possibles.

---

### Formule de Bayes
Elle permet de **retrouver la cause à partir du résultat** :

$$
P(A_i|B) =
\frac{P(B|A_i)P(A_i)}
{\sum P(B|A_j)P(A_j)}
$$

Cas simple :

$$
P(A|B) =
\frac{P(B|A)P(A)}
{P(B|A)P(A) + P(B|A^c)P(A^c)}
$$

---

## Indépendance

### Définition
Un évènement A est **indépendant** d’un évènement B si :

$$
P(A|B) = P(A)
$$

Ce qui est équivalent à :

$$
P(A \cap B) = P(A)P(B)
$$

👉 La réalisation de B n’influence pas la probabilité de A.

---
## Chapitre II : Variables aléatoires

---

## 1. Variables aléatoires

### Définition
Une **variable aléatoire (v.a)** est une application :

$$
X : \Omega \rightarrow \mathbb{R}
$$

qui associe à chaque issue $\omega$ de l’espace fondamental une valeur réelle $X(\omega)$.

---

### Types de variables aléatoires

✅ **Variable discrète**  
L’ensemble des valeurs est fini ou dénombrable :

$$
X(\Omega) = \{x_1, x_2, ..., x_n\} \quad \text{ou} \quad \{x_1, x_2, ..., x_n, ...\}
$$

✅ **Variable continue**  
Les valeurs forment un intervalle de $\mathbb{R}$.

⚠️ Attention : une v.a continue n’est pas forcément une fonction continue au sens de l’analyse.

---

### Exemples

- **Somme de deux dés** : valeurs de 2 à 12 → discrète  
- **Somme des carrés de deux dés** → discrète  
- **Taille d’un individu** → discrète ou continue selon la précision de mesure  

👉 On peut définir plusieurs variables aléatoires à partir d’une même expérience.

---

## 2. Lois de probabilité

---

### Cas des variables discrètes

On note :

$$
P(X = x_i)
$$

la probabilité que la v.a prenne la valeur $x_i$.

### Définition — Loi de probabilité
La loi d’une v.a discrète est l’ensemble des probabilités $P(X = x_i)$.

Conditions :

- $0 \le P(X = x_i) \le 1$
- **Condition de normalisation :**

$$
\sum_i P(X = x_i) = 1
$$

---

### Exemple : somme de deux dés

| k | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
|----|----|----|----|----|----|----|----|----|-----|-----|-----|
| P(X=k) | 1/36 | 2/36 | 3/36 | 4/36 | 5/36 | 6/36 | 5/36 | 4/36 | 3/36 | 2/36 | 1/36 |

Exemples :

$$
P(X \le 3) = 3/36
$$

$$
P(3 < X < 4) = 0
$$

(car X est entier)

---

### Cas des variables continues

On note :

$$
P(x_1 \le X \le x_2)
$$

### Densité de probabilité

Une fonction $f(x)$ telle que :

$$
P(x_1 \le X \le x_2) = \int_{x_1}^{x_2} f(x)\,dx
$$

Propriétés :

- $f(x) \ge 0$
- $\int f(x)dx = 1$
- $P(X = x) = 0$

👉 Impossible de tomber exactement sur une valeur réelle.

---

## Fonction de répartition

### Définition
$$
F(x) = \mathbb P(X \le x)
$$

---

### Cas discret
Somme des probabilités jusqu’à $x$.

---

### Cas continu
$$
F(x) = \int_{-\infty}^{x} f(t)dt
$$

Propriétés :

- $F'(x) = f(x)$
- $F$ est croissante
- $0 \le F(x) \le 1$

---

## 3. Lois usuelles

---

### Lois discrètes

#### Loi uniforme
Toutes les valeurs ont la même probabilité :

$$
\mathbb P(X = x_i) = \frac{1}{n}
$$

Exemple : dé équilibré.

⚠️ La somme de deux dés n’est **pas** uniforme.

---

#### Loi binomiale $B(N,p)$

Nombre de succès lors de $N$ épreuves de Bernoulli.

$$
\mathbb P(X=k) = \binom{N}{k} p^k (1-p)^{N-k}
$$

Exemple : nombre de piles obtenues en lançant une pièce.

---

#### Loi de Poisson

Approximation de la binomiale lorsque :

- $N$ grand  
- $p$ petit  

avec $\lambda = Np$

$$
\mathbb P(X=k) = \frac{e^{-\lambda}\lambda^k}{k!}
$$

---

### Lois continues

---

#### Loi uniforme sur $[a,b]$

Densité :

$$
f(x) = \frac{1}{b-a}
$$

Fonction de répartition :

$$
F(x)=
\begin{cases}
0 & x<a \\
\frac{x-a}{b-a} & a<x<b \\
1 & x>b
\end{cases}
$$

👉 Toutes les zones de l’intervalle sont équiprobables.

---

#### Loi exponentielle

Densité :

$$
f(x)=
\begin{cases}
\lambda e^{-\lambda x} & x \ge 0 \\
0 & x<0
\end{cases}
$$

Fonction de répartition :

$$
F(x)=1-e^{-\lambda x}
$$

Exemple : temps d’attente entre deux événements.

---

#### Loi normale (Gaussienne)

$$
f(x)=\frac{1}{\sqrt{2\pi}\sigma} e^{-\frac{(x-m)^2}{2\sigma^2}}
$$

Notée :

$$
\mathcal{N}(m,\sigma^2)
$$

- $m$ : moyenne  
- $\sigma$ : dispersion  

Cas particulier : **loi centrée-réduite** $\mathcal{N}(0,1)$.

---

## 4. Fonction d’une variable aléatoire

Si $Y = h(X)$, alors Y est une v.a.

Exemples :

- $Y = aX+b$
- $Y = X^2$
- $Y = \sin(X)$

---

### Cas discret
$$
P(Y=y_i) = \sum_{x_j \in h^{-1}(y_i)} P(X=x_j)
$$

Si $h$ est bijective :

$$
P(Y=y_i)=P(X=x_i)
$$

---

### Cas continu

Relation fondamentale :

$$
f(x)|dx| = g(y)|dy|
$$

Sinon, passer par la fonction de répartition.

---

## 5. Espérance mathématique

### Définition
L’espérance est la **valeur moyenne** de la variable.

---

### Discret
$$
E(X)=\sum x_i P(X=x_i)
$$

### Continu
$$
E(X)=\int x f(x)dx
$$

---

### Espérance des lois usuelles

| Loi | Espérance |
|--------|------------|
| Binomiale | $Np$ |
| Poisson | $\lambda$ |
| Uniforme $[a,b]$ | $(a+b)/2$ |
| Exponentielle | $1/\lambda$ |
| Normale | $m$ |

---

### Propriétés

- $E(aX+b)=aE(X)+b$
- $E(X_1+X_2)=E(X_1)+E(X_2)$

👉 L’espérance est **linéaire**.

---

## 6. Variance

### Définition
$$
\mathrm{Var}(X)=E[(X-E(X))^2]
$$

Mesure la dispersion autour de la moyenne.

---

### Formule pratique
$$
\mathrm{Var}(X)=E(X^2)-E(X)^2
$$

---

### Écart-type
$$
\sigma_X=\sqrt{\mathrm{Var}(X)}
$$

---

### Propriétés

- $\mathrm{Var}(aX+b)=a^2\mathrm{Var}(X)$
- La variance n’est **pas linéaire**.

---

### Variance des lois usuelles

| Loi           | Variance        |
| ------------- | --------------- |
| Binomiale     | $Np(1-p)$     |
| Poisson       | $\lambda$     |
| Uniforme      | $(b-a)^2/12$  |
| Exponentielle | $1/\lambda^2$ |
| Normale       | $\sigma^2$    |

---

### Exemple : lancer d’un dé

$$
E(X)=3.5
$$

$$
\mathrm{Var}(X)=\frac{35}{12}\approx 2.9
$$

$$
\sigma \approx 1.7
$$

# ✅ À retenir
- Univers : ensemble des résultats possibles.
- Évènement : sous-ensemble de l’univers.
- Probabilité : mesure entre 0 et 1.
- Conditionnement : on change l’univers.
- Bayes : remonter de l’effet à la cause.
- Indépendance : aucune influence entre évènements.
