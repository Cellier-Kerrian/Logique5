# Fiche 1 : Structures (Logique du Premier Ordre)

Basé sur la section 10 du polycopié de cours "Introduction à la Logique Informatique".

## 1. Signatures (Vocabulaire)

Une **signature** du premier ordre, notée $L = (\mathcal{F}, \mathcal{P})$, définit les symboles autorisés pour écrire des formules. Elle se compose de deux ensembles disjoints munis d'une fonction d'arité (nombre d'arguments) :

* **$\mathcal{F}$ (Symboles de fonction)** : Servent à désigner des objets ou des opérations sur les objets.
    * Si un symbole $f \in \mathcal{F}$ a une arité de 0, c'est une **constante**.
    * Notation : $\mathcal{F}_n$ désigne l'ensemble des symboles de fonction d'arité $n$.
* **$\mathcal{P}$ (Symboles de relation/prédicat)** : Servent à désigner des propriétés ou des relations entre objets.
    * Si un symbole $R \in \mathcal{P}$ a une arité de 0, c'est une **proposition**.
    * Notation : $\mathcal{P}_m$ désigne l'ensemble des symboles de relation d'arité $m$.

---

### 🎓 Exercice 1 : Identifier les symboles
Soit la signature $L = (\{c, g\}, \{Q\})$.
On donne les arités suivantes : $arite(c) = 0$, $arite(g) = 2$, $arite(Q) = 1$.

**Question :** Quelle est la nature précise de chaque symbole ?

<details>
<summary>✅ Voir la correction</summary>

* **$c$** : C'est un symbole de fonction d'arité 0, donc une **constante**.
* **$g$** : C'est un symbole de fonction d'arité 2 (fonction binaire).
* **$Q$** : C'est un symbole de relation d'arité 1 (relation unaire).
</details>

---

## 2. Interprétations (Sémantique des symboles)

Une **interprétation** $I$ donne un sens concret aux symboles de la signature. Elle est constituée de :

1.  **Un Domaine ($D_I$)** : Un ensemble **non vide** d'objets (ex: $\mathbb{N}$, $\mathbb{R}$, un ensemble fini $\{0, 1\}$, etc.).
2.  **L'interprétation des fonctions ($\mathcal{F}$)** :
    * Pour chaque symbole $f \in \mathcal{F}_n$, on associe une fonction concrète $f^I : D_I^n \rightarrow D_I$.
    * Pour une constante $c$, $c^I$ est simplement un élément fixé du domaine $D_I$.
3.  **L'interprétation des relations ($\mathcal{P}$)** :
    * Pour chaque symbole $R \in \mathcal{P}_m$, on associe une relation concrète $R^I : D_I^m \rightarrow \mathbb{B}$ (où $\mathbb{B} = \{0, 1\}$ est l'ensemble des valeurs de vérité).

> **Note :** Une interprétation est souvent notée $I = (D_I, (f^I)_{f \in \mathcal{F}}, (R^I)_{R \in \mathcal{P}})$.

---

### 🎓 Exercice 2 : Évaluer dans une structure
Soit la signature Arithmétique : $\mathcal{F} = \{s^{(1)}, 0^{(0)}\}$ et $\mathcal{P} = \{<^{(2)}\}$.
On définit l'interprétation $I$ suivante :
* Domaine $D_I = \mathbb{N}$ (entiers naturels).
* $0^I = 0$ (le chiffre zéro).
* $s^I(n) = n + 2$ (attention, ici le "successeur" ajoute 2).
* $<^I(n, m)$ est vrai si l'entier $n$ est strictement plus petit que $m$.

**Questions :**
1.  Que vaut l'objet désigné par $s^I(s^I(0^I))$ ?
2.  Est-ce que la relation $<^I(0^I, s^I(0^I))$ est vraie dans cette interprétation ?

<details>
<summary>✅ Voir la correction</summary>

1.  **Calcul de l'objet :**
    * $0^I = 0$.
    * $s^I(0^I) = 0 + 2 = 2$.
    * $s^I(s^I(0^I)) = s^I(2) = 2 + 2 = 4$.
    * **Résultat : 4**.

2.  **Évaluation de la relation :**
    * Premier argument : $0^I = 0$.
    * Deuxième argument : $s^I(0^I) = 2$.
    * La question devient : est-ce que $0 < 2$ ?
    * **Résultat : Vrai (1)**.
</details>