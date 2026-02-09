# Risk Management en Banque : Synthèse

## 1. La Banque : Une Approche Bilancielle
La banque assure des fonctions économiques clés qui génèrent structurellement des risques :
* **Intermédiation :** Transformation des dépôts en crédits.
* **Transformation de maturité :** Se finance à court terme pour prêter à long terme (Risque de liquidité et de taux).
* **Market-making :** Fourniture de liquidité sur les marchés.

### Les deux piliers du bilan bancaire
* **Banking Book (Portefeuille de banque) :** Activités d'intermédiation (crédits, dépôts). Risque de crédit et de taux.
* **Trading Book (Portefeuille de négociation) :** Instruments financiers destinés à être revendus à court terme. Risque de marché.

---

## 2. Le Contexte Réglementaire : Bâle III
La crise de 2008 a révélé un manque de fonds propres et de liquidité. Bâle III renforce la solidité du système financier via trois piliers.

### Les 3 Piliers de Bâle
1. **Pilier 1 (Exigences quantitatives) :** Capital minimum pour couvrir les risques de Crédit, Marché et Opérationnel.
2. **Pilier 2 (Processus de surveillance) :** Revue par le régulateur (SREP) et auto-évaluation (ICAAP/ILAAP).
3. **Pilier 3 (Discipline de marché) :** Obligations de transparence et de publication des risques.



---

## 3. Les Ratios Prudentiels Clés

### A. Ratios de Solvabilité (Fonds Propres)
L'objectif est de s'assurer que la banque peut absorber des pertes.
* **CET1 (Common Equity Tier 1) :** Le noyau dur du capital (actions, réserves).
* **Ratio de Solvabilité Global :** $\frac{\text{Fonds Propres}}{\text{RWA}} \ge 8\%$ (plus coussins additionnels).
* **RWA (Risk Weighted Assets) :** Pondération des actifs selon leur niveau de risque.

### B. Ratios de Liquidité
* **LCR (Liquidity Coverage Ratio) :** Résister à une crise de liquidité de **30 jours**. (Stock d'actifs liquides / Sorties nettes $\ge 100\%$).
* **NSFR (Net Stable Funding Ratio) :** Financer les actifs de long terme par des ressources stables (> 1 an).

### C. Ratio de Levier
Mesure non basée sur le risque (filet de sécurité) : $\frac{\text{Tier 1}}{\text{Exposition totale}} \ge 3\%$.



---

## 4. Mesure du Risque de Marché : La VaR (Value at Risk)
La VaR est l'outil principal pour quantifier la perte potentielle maximale sur un portefeuille.

> [!abstract] Définition de la VaR
> Perte maximale que l'on ne devrait pas dépasser sur un horizon de temps donné avec un niveau de confiance fixé (ex: 99%).

### Méthodes de calcul :
1. **VaR Historique :** Rejoue les variations passées du marché sur le portefeuille actuel.
2. **VaR Paramétrique (Variance-Covariance) :** Hypothèse de loi normale des rendements.
3. **VaR Monte Carlo :** Simulations stochastiques de milliers de scénarios.



---

## 5. Limites et Compléments à la VaR
* **Backtesting :** Comparer les pertes réelles avec la VaR pour vérifier la robustesse du modèle.
* **Stress Testing :** Simuler des scénarios extrêmes mais plausibles (chocs historiques ou hypothétiques) que la VaR ne capte pas.
* **Expected Shortfall (ES) :** Moyenne des pertes au-delà de la VaR (introduit par Bâle III pour mieux capter le risque de queue).

---
**Points de vigilance pour l'examen :**
- Savoir distinguer Banking Book vs Trading Book.
- Comprendre pourquoi on pondère les actifs par le risque (RWA).
- Connaître la différence entre LCR (court terme) et NSFR (long terme).