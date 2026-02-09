# Risk Management en Asset Management (AM)

## 1. Cadre des OPC (Contraintes et Engagement)
L'Asset Management est régi par des règles strictes visant à protéger l'investisseur, notamment via le format européen **OPCVM (UCITS)**.

### Caractéristiques clés des OPCVM :
* **Liquidité :** Les fonds sont ouverts (rachats possibles à tout moment).
* **Diversification :** Ratios **"5/10/40"** (limitation de l'exposition par émetteur pour éviter la concentration).
* **Actifs éligibles :** Liste précise des instruments autorisés (actions, obligations, monétaire, dérivés sous conditions).
* **Calcul de l'engagement :** Mesure de l'exposition globale liée aux instruments dérivés (méthode de l'engagement ou méthode VaR).

---

## 2. Mesure de la Performance (Le Rendement)
La performance se décompose en plusieurs indicateurs :
* **Performance Absolue :** Rendement total du portefeuille sur une période.
* **Performance Relative (Alpha) :** Surperformance par rapport à un indice de référence (Benchmark).
* **Tracking Error :** Volatilité de l'écart de rendement entre le fonds et son benchmark (mesure du "risque actif").

---

## 3. Attribution de Performance
L'objectif est d'expliquer d'où vient la performance (ou la sous-performance) :
* **Effet d'Allocation :** Choix des secteurs ou zones géographiques (ex: être surpondéré sur la technologie).
* **Effet de Sélection (Stock Picking) :** Choix des titres spécifiques au sein de chaque secteur.
* **Effet de Change :** Impact des variations de devises pour les actifs étrangers.

---

## 4. Ratios de Risque et de Performance (Ex-post)
Ces ratios permettent de juger si le rendement obtenu justifie le risque pris.

### A. Ratios de rentabilité ajustée au risque
* **Ratio de Sharpe :** $\frac{R_p - R_f}{\sigma_p}$
  * Mesure l'excès de rendement par unité de volatilité totale.
* **Ratio de Treynor :** $\frac{R_p - R_f}{\beta}$
  * Mesure l'excès de rendement par unité de risque systématique (Marché).
* **Ratio d'Information :** $\frac{\text{Alpha}}{\text{Tracking Error}}$
  * Évalue la capacité du gérant à générer de la performance relative par rapport au risque actif pris.

### B. Mesures de risque de perte (Downside Risk)
* **Maximum Drawdown (MDD) :** La plus forte baisse historique entre un sommet et un creux.
* **Drawdown Recovery :** Temps nécessaire pour retrouver le niveau d'avant la baisse.
* **Ratio de Calmar :** $\frac{\text{Rendement Annuel}}{\text{Max Drawdown}}$
* **Ratio de Sortino :** Similaire à Sharpe, mais ne considère que la volatilité à la baisse (*Downside Deviation*).

---

## 5. Contrôle et Gouvernance
Le Risk Management en AM est une fonction indépendante de la gestion :
* **Contrôle de 1er niveau :** Effectué par les gérants eux-mêmes.
* **Contrôle de 2ème niveau :** Effectué par le Risk Manager (indépendance).
* **Reporting :** Publication régulière du profil de risque (KIID/DIC) pour les investisseurs.

---
**Concepts clés pour l'examen :**
- Différence entre risque absolu (volatilité) et risque relatif (Tracking Error).
- Interprétation des ratios (plus ils sont élevés, meilleure est la gestion).
- Importance du Max Drawdown pour les investisseurs averses au risque.