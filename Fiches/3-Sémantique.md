# Fiche 3 : Sémantique (Logique du Premier Ordre)

Basé sur la section 12 du polycopié de cours "Introduction à la Logique Informatique".

Cette section explique comment déterminer si une formule est **vraie** ou **fausse**.

## 1. Le Cadre de Vérité

Pour donner du sens à une formule, nous avons besoin de deux éléments :
1.  [cite_start]Une **Interprétation** $I$ (qui donne le sens des symboles $f$ et $R$) sur un domaine $D_I$[cite: 3166, 3167].
2.  [cite_start]L'ensemble des valeurs de vérité $\mathbb{B} = \{0, 1\}$ (0 pour Faux, 1 pour Vrai)[cite: 3166].

---

## 2. La Valuation ($\rho$)

Les formules contiennent des **variables** ($x, y...$). Une interprétation seule ne suffit pas à les évaluer.

* [cite_start]**Définition** : Une valuation est une fonction $\rho : X \rightarrow D_I$ qui associe à chaque variable une valeur concrète dans le domaine[cite: 3167].
* [cite_start]**Notation de mise à jour** : $\rho[e/x]$ désigne une nouvelle valuation identique à $\rho$, sauf pour la variable $x$ qui prend la valeur $e$[cite: 3168].

> **Exemple :**
> Si le domaine est les entiers $\mathbb{N}$ et $\rho(x) = 0$.
> Alors $\rho[5/x](x) = 5$.

---

## 3. Sémantique des Termes et Formules

L'évaluation se fait inductivement (du plus petit élément vers le plus grand).

### A. Sémantique d'un Terme $[[t]]_{\rho}^{I}$
[cite_start]Cela retourne un **objet** du domaine $D_I$[cite: 3159].

* [cite_start]**Variable** : $[[x]]_{\rho}^{I} = \rho(x)$[cite: 3169].
* [cite_start]**Fonction** : On évalue les arguments, puis on applique la fonction de l'interprétation : $[[f(t_1...)]]_{\rho}^{I} = f^I([[t_1]]_{\rho}^{I}...)$[cite: 3171].

### B. Sémantique d'une Formule $[[\varphi]]_{\rho}^{I}$
[cite_start]Cela retourne une **valeur de vérité** (0 ou 1)[cite: 3160]. [cite_start]On note $I, \rho \models \varphi$ si cette valeur est 1[cite: 3176].

1.  [cite_start]**Atome ($R(t...)$)** : Vrai si les termes évalués appartiennent à la relation $R^I$[cite: 3177].
2.  [cite_start]**Négation ($\neg \varphi$)** : Vrai si $I, \rho \not\models \varphi$[cite: 3178].
3.  [cite_start]**Disjonction ($\vee$)** : Vrai si l'un ou l'autre est vrai[cite: 3179].
4.  **Quantification Existentielle ($\exists$)** :
    $I, \rho \models \exists x. \varphi$ si **il existe** un élément $e \in D_I$ tel que $I, \rho[e/x] \models \varphi$[cite: 3180, 3184].

---

## 4. Satisfiabilité, Modèle et Validité

Ces trois notions définissent le "degré de vérité" d'une formule.

| Notion | Définition | Notation |
| :--- | :--- | :--- |
| **Satisfiable** | [cite_start]Il existe au moins un couple $(I, \rho)$ tel que la formule est vraie[cite: 3185]. | N/A |
| **Modèle** | [cite_start]Une interprétation $I$ est un modèle si la formule est vraie pour **toutes** les valuations $\rho$[cite: 3186]. | $I \models \varphi$ |
| **Valide** | [cite_start]La formule est vraie pour **toutes** les interprétations et **toutes** les valuations[cite: 3186]. | $\models \varphi$ |

> **Exemple de Validité :** La "formule du buveur" $\exists x. (B(x) [cite_start]\Rightarrow \forall y. B(y))$ est valide[cite: 3241]. Peu importe qui sont les gens ($D_I$) et qui boit ($B^I$), c'est toujours mathématiquement vrai.

---

## 🎓 Exercices Corrigés

### Exercice 1 : Mécanique de la Valuation
**Contexte :**
* Signature Arithmétique : $L = (\{+^{(2)}\}, \{=^{(2)}\})$.
* Interprétation $I$ : Domaine $\mathbb{N}$, $+^I$ est l'addition classique, $=^I$ est l'égalité.
* Valuation $\rho$ : $\rho(x) = 10$, $\rho(y) = 5$.

**Question :** Est-ce que $I, \rho \models \exists z. (x = y + z)$ ?

<details>
<summary>✅ Voir la correction détaillée</summary>

1.  **Analyse de la formule :** On cherche à savoir si $\exists z. (x = y + z)$ est vrai.
2.  **Définition du quantificateur :** D'après la règle du $\exists$, cela est vrai s'il existe un entier $e \in \mathbb{N}$ tel que la formule $(x = y + z)$ soit vraie avec la valuation $\rho[e/z]$.
3.  **Évaluation des termes :**
    * $[[x]]_{\rho[e/z]}^{I} = \rho(x) = 10$.
    * $[[y + z]]_{\rho[e/z]}^{I} = [[y]] + [[z]] = 5 + e$.
4.  **Résolution :** On cherche $e \in \mathbb{N}$ tel que $10 = 5 + e$.
    * Si on choisit $e = 5$, alors $10 = 10$.
5.  **Conclusion :** Puisqu'un tel $e$ existe (5), la formule est **Vraie**.
</details>

---

### Exercice 2 : Modèle vs Validité
**Contexte :**
* Formule : $\varphi = \forall x. \forall y. (R(x,y) \Rightarrow R(y,x))$. (Cette formule exprime la symétrie).

**Questions :**
1.  Donnez une interprétation $I_1$ qui est un **modèle** de $\varphi$.
2.  Donnez une interprétation $I_2$ qui **n'est pas** un modèle de $\varphi$.
3.  La formule est-elle **valide** ?

<details>
<summary>✅ Voir la correction détaillée</summary>

1.  **Modèle ($I_1$) :**
    * Prenons le domaine $D = \mathbb{N}$ et $R^{I_1}$ comme la relation d'égalité $=$.
    * Si $x = y$, alors forcément $y = x$. La symétrie est respectée.
    * $I_1 \models \varphi$.

2.  **Contre-modèle ($I_2$) :**
    * Prenons le domaine $D = \mathbb{N}$ et $R^{I_2}$ comme la relation "strictement inférieur" $<$.
    * Prenons une valuation où $x=1$ et $y=2$.
    * $R(1, 2)$ est vrai ($1 < 2$), MAIS $R(2, 1)$ est faux ($2 \not< 1$).
    * L'implication Vrai $\Rightarrow$ Faux est Fausse.
    * $I_2 \not\models \varphi$.

3.  **Validité :**
    * Une formule est valide si elle est vraie dans **toutes** les interprétations.
    * Puisqu'on a trouvé une interprétation ($I_2$) où elle est fausse, **la formule n'est pas valide**.
</details>