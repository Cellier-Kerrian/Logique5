# Fiche 5 : Formes Normales (Logique du Premier Ordre)

Basé sur la section 14 du polycopié de cours "Introduction à la Logique Informatique".

## 1. Forme Normale Négative (NNF)

Une formule est en **NNF** si le symbole de négation ($\neg$) n'apparaît **que devant des formules atomiques**.

### L'Algorithme de transformation
On utilise les règles d'équivalence logique pour "pousser" les négations vers l'intérieur :

* **Double négation** : $\neg \neg \varphi \equiv \varphi$
* **Lois de De Morgan** :
    * $\neg (\varphi \vee \psi) \equiv (\neg \varphi \wedge \neg \psi)$
    * $\neg (\varphi \wedge \psi) \equiv (\neg \varphi \vee \neg \psi)$
* **Dualité des Quantificateurs** (Le point clé !) :
    * $\neg (\forall x. \varphi) \equiv \exists x. (\neg \varphi)$
    * $\neg (\exists x. \varphi) \equiv \forall x. (\neg \varphi)$

> **Astuce mnémotechnique :** Quand le $\neg$ traverse un quantificateur, le quantificateur s'inverse ($\forall \leftrightarrow \exists$).

---

## 2. Forme Prénexe

Une formule est sous **Forme Prénexe** si elle s'écrit comme une liste de quantificateurs suivie d'une formule sans quantificateur (la matrice).
Format : $Q_1 x_1 ... Q_n x_n . \psi$ (où $Q_i \in \{\forall, \exists\}$).

### L'Algorithme d'extraction
Pour mettre une formule en forme prénexe, on commence généralement par la mettre en NNF, puis on "tire" les quantificateurs vers l'extérieur en utilisant ces règles :

* $(\forall x. \varphi) \wedge \psi \equiv \forall x. (\varphi \wedge \psi)$
* $(\exists x. \varphi) \vee \psi \equiv \exists x. (\varphi \vee \psi)$
* *(Idem pour les autres combinaisons $\wedge / \vee$)*.

### ⚠️ La Condition Critique : La Variable Libre
Ces règles ne sont valides que si **$x$ n'est pas libre dans $\psi$** ($x \notin fv(\psi)$).
Si $x$ est libre dans $\psi$, il y a un conflit de nom (capture). Il faut d'abord faire un **$\alpha$-renommage** sur la partie quantifiée.

> **Exemple de conflit :** $(\forall x. P(x)) \vee Q(x)$.
> Ici, le $x$ de droite est libre. On ne peut pas sortir le $\forall x$ directement.
> 1. Renommage : $(\forall z. P(z)) \vee Q(x)$.
> 2. Extraction : $\forall z. (P(z) \vee Q(x))$.

---

## 🎓 Exercices Corrigés

### Exercice 1 : Mise en Forme Normale Négative (NNF)
Mettre la formule suivante en NNF (pousser les négations) :
$$\varphi = \neg ( \forall x. ( P(x) \Rightarrow \exists y. R(x, y) ) )$$
*(Rappel : $A \Rightarrow B$ équivaut à $\neg A \vee B$)*

<details>
<summary>✅ Voir la correction</summary>

1.  **Éliminer l'implication ($\Rightarrow$) :**
    $\neg ( \forall x. ( \neg P(x) \vee \exists y. R(x, y) ) )$
2.  **Pousser le $\neg$ à travers le $\forall x$ (Dualité) :**
    $\exists x. \neg ( \neg P(x) \vee \exists y. R(x, y) )$
3.  **Pousser le $\neg$ à travers le $\vee$ (De Morgan) :**
    $\exists x. ( \neg \neg P(x) \wedge \neg \exists y. R(x, y) )$
4.  **Double négation et Dualité sur $\exists y$ :**
    $\exists x. ( P(x) \wedge \forall y. \neg R(x, y) )$

**Résultat final :** $\exists x. ( P(x) \wedge \forall y. \neg R(x, y) )$
</details>

---

### Exercice 2 : Mise en Forme Prénexe
Mettre la formule suivante en forme prénexe :
$$\psi = (\exists x. P(x)) \vee (\forall x. Q(x))$$

<details>
<summary>✅ Voir la correction</summary>

1.  **Analyse :** Nous avons deux quantificateurs qui utilisent la même variable $x$. Pour les sortir les deux devant, il faut éviter qu'ils se mélangent.
2.  **$\alpha$-renommage :** Renommons le deuxième $x$ en $y$.
    $(\exists x. P(x)) \vee (\forall y. Q(y))$
3.  **Sortir le premier quantificateur ($\exists x$) :**
    $\exists x. ( P(x) \vee (\forall y. Q(y)) )$
    *(Possible car $x$ n'est pas libre dans la partie droite)*.
4.  **Sortir le deuxième quantificateur ($\forall y$) :**
    $\exists x. \forall y. ( P(x) \vee Q(y) )$

**Résultat final :** $\exists x. \forall y. ( P(x) \vee Q(y) )$
*(Note : L'ordre $\forall y. \exists x...$ est aussi une réponse valide ici car les quantificateurs sont indépendants).*
</details>