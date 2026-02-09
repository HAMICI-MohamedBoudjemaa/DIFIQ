# Évaluer les options
## Le modèle binomial : intuition

**Exemple :**
Un parapluie vaut aujourd’hui 100 €.

- +10 % s’il pleut → 110 €
- -10 % sinon → 90 €
- Taux d’intérêt : 0 %
- Probabilité de pluie : 90 %

Call de strike 100 :

- Payoff = 10 s’il pleut
- Payoff = 0 sinon

Espérance naïve :  
$$
0.9 \times 10 + 0.1 \times 0 = 9
$$

👉 Pourtant, le prix du call **n’est pas 9 €**.

---

## Structure du modèle binomial

Modèle à une période avec deux états :

- Actif risqué :
$$
S_0 \rightarrow 
\begin{cases}
uS_0 & (p) \\
dS_0 & (1-p)
\end{cases}
$$

- Actif sans risque :
$$
B_0 = 1,\quad B_1 = 1+r
$$

---

## Condition d’absence d’arbitrage

$$
d < 1+r < u
$$

Sinon :

- Si $1+r \le d$ → arbitrage en achetant l’actif risqué
- Si $u \le 1+r$ → arbitrage en vendant l’actif

---

## Payoff du call

$$
C_u = (uS_0 - K)^+
$$
$$
C_d = (dS_0 - K)^+
$$

---

## Portefeuille de réplication

Construisons un portefeuille :

- $a$ unités d’actif risqué  
- $b$ unités d’actif sans risque  

Valeur initiale :

$$
V_0 = aS_0 + b
$$

Valeurs futures :

$$
V_u = auS_0 + b(1+r)
$$
$$
V_d = adS_0 + b(1+r)
$$

On cherche :

$$
auS_0 + b(1+r) = C_u
$$
$$
adS_0 + b(1+r) = C_d
$$

👉 $a$ correspond au **delta**.

---

## Exemple du parapluie

Données :

- $S_0 = 100$
- $u = 1.1$
- $d = 0.9$
- $r = 0$
- $C_u = 10$
- $C_d = 0$

Solution :

$$
a = 0.5,\quad b = -45
$$

Donc :

$$
C_0 = 5€
$$

👉 Différent de l’espérance naïve, car le prix du parapluie n’intègre pas correctement la probabilité de pluie.

---

## Probabilité risque-neutre

On définit :

$$
q = \frac{(1+r) - d}{u-d}
$$

Avec :

$$
0 < q < 1
$$

Le prix devient :

$$
C_0 = \frac{qC_u + (1-q)C_d}{1+r}
$$

👉 Sous la **mesure risque-neutre**, le prix est l’espérance actualisée du payoff.

---

## Interprétation financière

Sous la probabilité risque-neutre :

👉 **Rendement espéré = taux sans risque**

Le prix actualisé d’un actif est une **martingale**.

⚠️ Ce n’est pas une probabilité réelle — seulement un outil de calcul.

---

## Un prix n’est pas une espérance objective

Loterie :

- 1 M€ avec probabilité 0.5  
- 0 sinon  

Espérance : **500 K€**

Mais la plupart préfèrent **400 K€ certains** → aversion au risque.

Si la loterie vaut 100 K€ sur le marché, cela revient à utiliser une probabilité risque-neutre :

- 0.1 pour le gain  
- 0.9 pour la perte  

---

# Le modèle de Black & Scholes

Issu de la limite d’un modèle binomial multi-périodes.

Hypothèse : le prix du sous-jacent suit une **dynamique log-normale**.

Le mouvement brownien $W_T$ est normalement distribué avec variance $T$.

👉 Donc :

$$
\ln(S_T) \sim \mathcal{N}
$$

---

## Interprétation

Black & Scholes suppose :

👉 des rendements gaussiens.

En pratique ?  
➡️ Pas totalement réaliste (queues épaisses, krachs…).

---

## Volatilité

La volatilité $\sigma$ est :

👉 l’écart-type annualisé des rendements.

Sous B&S, le rendement logarithmique sur $\Delta t$ suit une loi normale d’écart-type :

$$
\sigma \sqrt{\Delta t}
$$

---

## Estimer la volatilité historique

Méthode :

1. Calculer les rendements
2. Estimer leur écart-type
3. Annualiser

Exemple CAC 40 :

$$
\Delta t \approx \frac{1}{255}
$$

---

## Formule de Black & Scholes

Permet de calculer directement le prix :

- d’un call
- d’un put

à partir des paramètres de marché.

---

## Inputs du modèle

- $T$ : maturité (années)
- $K$ : strike
- $S_0$ : prix actuel
- $\sigma$ : volatilité
- $r$ : taux sans risque (continu)

---

## Black & Scholes avec dividendes

On introduit un taux continu de dividendes $d$.

Les formules de pricing sont ajustées en conséquence.

---

## Volatilité implicite

Définition :

La volatilité implicite est la valeur de $\sigma$ telle que :

$$
Prix_{BS} = Prix_{marché}
$$

👉 C’est une **donnée de marché majeure**.

Sur certains marchés (FX), les options sont cotées directement en volatilité.

---

## Smile de volatilité

Pour une même maturité :

👉 la volatilité implicite varie selon le strike.

Conséquence :

➡️ Le modèle B&S est incomplet.

- Forme en U → **smile**
- Vol décroissante → **skew**

---

## Surface de volatilité

La volatilité dépend :

- du strike  
- de la maturité  

$$
\sigma = f(K, T)
$$

On parle de **surface de volatilité**.

---

## Valeur intrinsèque et valeur temps

Prix d’une option :

$$
Prix = Valeur\ intrinsèque + Valeur\ temps
$$

---

### Valeur intrinsèque

Partie positive du forward.

Pour un call (sans dividendes) :

$$
\max(S_0 - Ke^{-rT}, 0)
$$

👉 C’est le **minorant** du prix de l’option.

Dans un monde sans incertitude ($\sigma = 0$),  
le prix = valeur intrinsèque.

---

### Valeur temps

$$
Valeur\ temps = Prix\ de\ l’option - Valeur\ intrinsèque
$$

Elle représente :

👉 le **prix de l’incertitude**.

Caractéristiques :

- maximale **à la monnaie**
- augmente avec la volatilité
- augmente avec le temps jusqu’à maturité

---

## Effet du temps

Plus la maturité est longue :

👉 plus l’option vaut cher.

Cela vaut pour :

- les calls
- les puts
