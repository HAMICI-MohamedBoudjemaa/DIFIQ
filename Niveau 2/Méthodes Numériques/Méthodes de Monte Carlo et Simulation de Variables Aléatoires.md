# Introduction
*==Intuitivement, l'idée est de générer un grand nombre de réalisations en considérant que la moyenne de ces réalisations est un estimateur de l'espérance de la fonction de la variable aléatoire estimée f(X)==*

Les méthodes de Monte Carlo permettent d'estimer des quantités en générant une suite de réalisations pour laquelle la loi des grands nombres s'applique.

$$  
\begin{align}
\Theta = \mathbb E^\mathbb P(f(X)) = \int _{\mathbb R^d} f(x)d \mathbb P_X(x)
\end{align}
$$
Où $f : \mathbb R^d \to \mathbb R$ telle que $$\int _{\mathbb R^d} \lvert{f(x)}\rvert d \mathbb P_{X}(x) < \infty$$
Formellement, on a : $$\Theta _{n} := \frac{1}{n} \sum _{k=1} ^{n} f(X _{k}) \overset{P-p.s.}{\underset {n \rightarrow +\infty} {\longrightarrow}} \mathbb E ^{\mathbb P} [f(X)]$$
# Loi des grands nombres
_Soit X une variable aléatoire (v.a.) de loi $\mathbb P _{X}$ et $f : \mathbb R \to \mathbb R$ une fonction telle que $\mathbb E ^{\mathbb P} [\lvert{f(x)}\rvert] < \infty$ ==(f admet une espérance finie)==. Soit $(X _{n}) _{n \in \mathbb N}$ une suite de v.a. réelles i.i.d. de loi $\mathbb P _{X}$. Alors :_

## Loi faible

## Loi Forte

# Théorème Centrale Limite
