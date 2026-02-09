# 4. Pour aller plus loin...

## 1. Panorama des Options Exotiques
Les options exotiques se distinguent des options standards (Vanille) par la complexité de leur payoff ou de leurs conditions d'exercice.

### Exemples classiques :
* **Options Américaines :** Exercice possible à tout moment avant l'échéance.
* **Options Digitales :** Payoff binaire (tout ou rien).
* **Options à Barrière :** S'activent (In) ou se désactivent (Out) si le sous-jacent touche un seuil.
* **Options Asiatiques :** Le payoff dépend de la moyenne des cours du sous-jacent.
* **Options Lookback :** Dépendent du maximum ou du minimum atteint par le cours.
* **Options sur Spread / Best-of / Worst-of :** Portent sur plusieurs actifs (corrélation).

---

## 2. Risques liés aux Options Exotiques

L'évaluation d'un produit exotique nécessite un modèle capable d'appréhender trois types de risques majeurs :

1. **Risque Digital (Discontinuité) :** Sensibilité extrême du prix aux variations du sous-jacent près de la barrière ou du strike.
2. **Risque de Volatilité Forward :** Sensibilité à la structure à terme de la volatilité.
3. **Risque de Corrélation :** Pour les produits multi-actifs, l'incertitude sur la dépendance entre les actifs.

> [!important] Règle d'or
> Un modèle doit avoir une dynamique adéquate mais surtout une **calibration adéquate** sur les prix de marché des instruments liquides.

---

## 3. Les Méthodes Numériques

Lorsqu'il est impossible de trouver une formule explicite (closed form), on utilise des méthodes numériques pour résoudre les équations de prix.

### 3.1 Méthodes "Backward"
Elles partent de la date d'échéance ($T$) pour remonter vers la date d'aujourd'hui ($t=0$).
* **Arbres (Binomiaux/Trinomiaux) :** Discrétisation du cours du sous-jacent.
* **Différences Finies (EDP) :** Résolution numérique de l'équation de Black-Scholes.
* **Avantage :** Idéal pour les options américaines (possibilité de vérifier l'exercice anticipé à chaque étape).



### 3.2 Méthodes "Forward"
Elles simulent les trajectoires futures du sous-jacent.
* **Méthode de Monte Carlo :** Simulation de milliers de scénarios basés sur une diffusion stochastique.
* **Avantage :** Idéal pour les options dépendant du chemin parcouru (Asiatiques, Lookback) et les problèmes en haute dimension.



---

## 4. Exercices de révision (Grecques et Stratégies)

> [!question] Exercice : Couverture Delta
> Je vends un **Risk Reversal 80/120** (Vente Call 120 + Achat Put 80). Pour me couvrir en Delta, dois-je acheter ou vendre du sous-jacent ?
> 
> **Réponse :**
> 1. En vendant le RR, je suis *Short Call* ($\Delta < 0$) et *Long Put* ($\Delta < 0$).
> 2. Ma position globale est **Delta négative**.
> 3. Pour être neutre, je dois **acheter** de l'actif sous-jacent.

> [!question] Exercice : Arbitrage Volatilité
> La volatilité implicite est très élevée par rapport à la volatilité réelle constatée. Quelle stratégie adopter ?
> - **A.** Acheter des options
> - **B.** Vendre des options et les couvrir en delta
> 
> **Réponse :** **B**. On vend la volatilité chère (implicite) et on gère le risque directionnel par le delta-hedging pour ne capter que le différentiel de volatilité.

---
**Étape suivante suggérée :** Souhaitez-vous que je détaille le fonctionnement mathématique d'un **Arbre Binomial** ou que je génère un script Python pour une **Simulation de Monte Carlo** ?