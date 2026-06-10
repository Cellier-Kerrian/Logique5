# Fiche 2 : Syntaxe (Logique du Premier Ordre)

Basé sur la section 11 du polycopié de cours "Introduction à la Logique Informatique".

## 1. Les Termes ($t$)

Les termes désignent des **objets** du domaine. Ils sont définis inductivement par la grammaire suivante :
$$t ::= x \mid f(t_1, ..., t_n)$$

* **$x$** : Une variable (issue d'un ensemble infini dénombrable $X$).
* **$f$** : Un symbole de fonction d'arité $n$ (si $n=0$, c'est une constante).

> **Attention :** Un terme ne peut jamais être "Vrai" ou "Faux". C'est un nom pour un objet (ex: "$x+1$", "la mère de Luke").

---

## 2. Les Formules ($\varphi$)

Les formules désignent des **énoncés** qui peuvent être Vrais ou Faux. Elles sont construites ainsi :

1.  **Formules Atomiques ($\alpha$)** : C'est la base. On applique un symbole de relation à des termes.
    $$\alpha ::= R(t_1, ..., t_m)$$
2.  **Formules Complexes** : Construites via les connecteurs logiques et quantificateurs.
    $$\varphi ::= \alpha \mid \neg \varphi \mid \varphi \vee \psi \mid \exists x. \varphi$$

* Les autres connecteurs ($\wedge, \Rightarrow, \forall$) sont souvent définis comme des abréviations (ex: $\forall x. \varphi \triangleq \neg \exists x. \neg \varphi$).

---

### 🎓 Exercice 1 : Terme, Formule ou Incorrect ?
On travaille avec la signature : fonctions $\{+^{(2)}, 1^{(0)}\}$, relations $\{=^{(2)}\}$.
Pour chaque expression, indiquez sa nature.

1.  $1 + 1$
2.  $1 = (1 + x)$
3.  $(1 = x) + 1$

<details>
<summary>✅ Voir la correction</summary>

1.  **Terme**. C'est une application de la fonction $+$ sur deux termes (constantes). Ça désigne un objet (le nombre 2).
2.  **Formule**. C'est l'application du symbole de relation $=$ entre deux termes. Ça exprime une vérité.
3.  **Incorrect**. Le symbole $+$ (fonction) attend des termes comme arguments. Ici, $(1=x)$ est une formule. On ne peut pas additionner une formule et un nombre.
</details>

---

## 3. Variables Libres et Liées

Il est crucial de distinguer le statut des variables dans une formule :

* **Variable Liée ($bv$)** : Une variable est liée si elle apparaît sous la portée d'un quantificateur ($\exists x$ ou $\forall x$).
* **Variable Libre ($fv$)** : Une variable est libre si elle n'est pas liée. Elle agit comme un paramètre externe.
* **Formule Close** : Une formule qui ne contient **aucune** variable libre ($fv(\varphi) = \emptyset$).

**Règles de calcul pour $fv(\varphi)$ (variables libres) :**
* $fv(x) = \{x\}$.
* $fv(\neg \varphi) = fv(\varphi)$.
* $fv(\varphi \vee \psi) = fv(\varphi) \cup fv(\psi)$.
* $fv(\exists x. \varphi) = fv(\varphi) \setminus \{x\}$ (le quantificateur "capture" la variable $x$, elle n'est plus libre).

> **💡 Comprendre la "Capture" (Approche Bottom-Up)**
> Pour comprendre pourquoi une variable cesse d'être libre, il faut imaginer la construction de la formule de l'intérieur vers l'extérieur :
> 1.  **Avant** le quantificateur : Dans la sous-formule $\varphi$ (ex: $x > 0$), la variable $x$ est **libre** ($fv = \{x\}$). Elle attend une valeur externe.
> 2.  **Ajout du quantificateur** : On applique $\exists x$ devant. Le quantificateur prend le contrôle de toutes les occurrences de $x$.
> 3.  **Résultat** : La variable est **capturée** (liée). Mathématiquement, on la **soustrait** de l'ensemble des variables libres : $fv(\exists x. \varphi) = \{x\} \setminus \{x\} = \emptyset$.

---

### 🎓 Exercice 2 : Analyse de variables
Soit la formule $\varphi = (\exists x. R(x, y)) \wedge P(x)$.

1.  Quelles sont les variables liées ?
2.  Quelles sont les variables libres ?

<details>
<summary>✅ Voir la correction</summary>

1.  **Variables liées :**
    * La variable **$x$** est liée dans la sous-formule $\exists x. R(x, y)$ car elle est sous le quantificateur $\exists x$.

2.  **Variables libres :**
    * Dans la partie gauche $(\exists x. R(x, y))$, $x$ est liée, mais **$y$** est libre.
    * Dans la partie droite $P(x)$, il n'y a pas de quantificateur, donc **$x$** est libre.
    * L'ensemble des variables libres de la formule entière est l'union des variables libres des deux parties.
    * **Résultat : $fv(\varphi) = \{x, y\}$**.
    * *Remarque :* La variable $x$ est à la fois liée (à gauche) et libre (à droite) dans cette formule, ce qui est syntaxiquement correct mais souvent déconseillé pour la lisibilité.
</details>