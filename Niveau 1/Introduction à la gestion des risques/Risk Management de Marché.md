# Mesure et Gestion du Risque de Marché

## 1. La Value at Risk (VaR)
La VaR est l'indicateur de référence pour mesurer le risque de perte maximale sur un horizon de temps ($h$) avec un niveau de confiance ($\alpha$).

### A. Les 3 Méthodes de calcul
1. **VaR Paramétrique (Variance-Covariance) :**
   - Repose sur l'hypothèse de **normalité** des rendements.
   - Formule : $VaR = \text{Position} \times z_{\alpha} \times \sigma \times \sqrt{h}$
   - *Avantage :* Simple et rapide. *Inconvénient :* Ne capte pas les "queues de distribution" épaisses (*Fat Tails*).

2. **VaR Historique :**
   - Ne fait aucune hypothèse de loi de probabilité. On applique les variations passées des prix au portefeuille actuel.
   - *Avantage :* Capte les corrélations réelles passées. *Inconvénient :* Suppose que le passé se répètera.

3. **VaR Monte Carlo :**
   - Génère des milliers de scénarios de prix via des modèles stochastiques.
   - *Avantage :* Très flexible pour les produits complexes (options). *Inconvénient :* Très coûteux en temps de calcul.



---

## 2. Au-delà de la VaR : Stress Testing & Backtesting

### A. Backtesting (Validation)
Consiste à compter le nombre de fois où la perte réelle a dépassé la VaR calculée.
* Si le nombre d'exceptions est trop élevé, le modèle est sous-évalué (Zone Rouge du régulateur).

### B. Stress Testing (Risque de queue)
La VaR ne dit rien sur ce qu'il se passe au-delà du seuil de confiance. 
* **Scénarios Historiques :** Rejouer une crise passée (ex: Lehman Brothers 2008, COVID 2020).
* **Scénarios Hypothetiques :** Simuler des chocs extrêmes mais plausibles (ex: hausse brutale des taux de +200 bps).

---

## 3. Gestion du Risque en Sensibilité (Grecques & Co)
Pour les produits non-linéaires (options) ou obligataires, la VaR est complétée par des mesures de sensibilité.

### A. Sensibilités Obligataires
* **Sensibilité (S) :** Variation du prix pour une hausse de 1% des taux.
* **Duration (D) :** Durée de vie moyenne pondérée des flux (mesure du risque de taux).
* **Convexité :** Courbure de la relation prix/taux. Une convexité positive est favorable à l'investisseur.



### B. Les Grecques (Options)
| Grecque | Mesure la sensibilité au... |
| :--- | :--- |
| **Delta ($\Delta$)** | Variation du prix du sous-jacent. |
| **Gamma ($\gamma$)** | Variation du Delta (courbure). |
| **Vega ($\nu$)** | Variation de la volatilité implicite. |
| **Théta ($\theta$)** | Passage du temps (érosion temporelle). |
| **Rho ($\rho$)** | Variation des taux d'intérêt. |

### C. Le Bêta ($\beta$)
Mesure la sensibilité relative d'un actif par rapport à son indice de référence.
* $\beta > 1$ : Actif agressif (amplifie les mouvements du marché).
* $\beta < 1$ : Actif défensif (amortit les mouvements).

---

## 4. Limites de la VaR et nouveaux standards
Le passage de **Bâle III** vers la **FRTB** (Fundamental Review of the Trading Book) privilégie désormais :
* **Expected Shortfall (ES) :** Moyenne des pertes dans la queue de distribution (au-delà de la VaR). Contrairement à la VaR, l'ES est une mesure de risque "cohérente".

---
**Focus Examen :**
- Savoir identifier quelle méthode de VaR est la plus adaptée selon le portefeuille.
- Comprendre le lien entre prix et taux (inversement proportionnels).
- Connaître l'impact d'une convexité négative (cas des *callable bonds*).