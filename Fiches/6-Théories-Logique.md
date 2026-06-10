# Fiche 6 : Théories Logiques

Basé sur la section 15 du polycopié de cours "Introduction à la Logique Informatique".

## 1. Qu'est-ce qu'une Théorie ?

Une **Théorie** $T$ est un ensemble de formules closes (sans variables libres) qui est "fermé par conséquence logique".
Cela veut dire que si une formule $\varphi$ est une conséquence logique de la théorie (si $T \models \varphi$), alors $\varphi$ doit appartenir à la théorie ($\varphi \in T$).

> **Analogie :** Une théorie est comme une "base de connaissances" infinie qui contient tout ce qui est vrai sur un sujet donné.

Il y a deux façons principales de définir une théorie :

### A. La Théorie d'une Structure ($Th(I)$)
C'est l'approche "Observation". On prend un monde (une interprétation $I$) et on met dans le sac **toutes** les phrases qui sont vraies dans ce monde.
* **Définition :** $Th(I) = \{ \varphi \text{ close } \mid I \models \varphi \}$.
* **Exemple :** $Th(\mathbb{N}, <)$ contient toutes les vérités sur l'ordre des entiers naturels.

### B. La Théorie Axiomatique ($Th(A)$)
C'est l'approche "Règlement". On pose une liste de règles de base (les axiomes $A$) et la théorie est tout ce qu'on peut déduire de ces règles.
* **Définition :** $Th(A) = \{ \varphi \text{ close } \mid A \models \varphi \}$.
* **Exemple :** La théorie des groupes, la théorie des ordres, etc.

---

## 2. L'Égalité et les Interprétations Normales

En logique, le symbole $=$ est un symbole de relation comme les autres. On pourrait très bien décider que $1 = 2$ est Vrai dans une interprétation bizarre.

Pour éviter ça, on impose des axiomes ou des contraintes.

### Les Axiomes de l'Égalité ($A_{eq}$)
Pour que $=$ ressemble à une égalité, il doit être une **relation d'équivalence** :
1.  **Réflexivité** : $\forall x. x = x$
2.  **Symétrie** : $\forall x \forall y. (x = y \Rightarrow y = x)$
3.  **Transitivité** : $\forall x \forall y \forall z. (x = y \wedge y = z \Rightarrow x = z)$

### Les Axiomes de Congruence ($A_{cgr}$)
Si $x = y$, alors $x$ et $y$ doivent être interchangeables dans n'importe quelle fonction ou relation.
* Exemple : $\forall x \forall y. (x = y \Rightarrow f(x) = f(y))$.

### Interprétation Normale
Une interprétation est dite **normale** si le symbole $=$ est interprété comme la **vraie égalité mathématique** (l'identité) sur le domaine.
* Si une interprétation respecte les axiomes $A_{cgr}$ mais n'est pas normale (ex: elle traite deux objets distincts comme égaux), on peut la "réparer" en faisant le **quotient** ($I / =^I$). On fusionne les objets indistinguables pour obtenir une interprétation normale équivalente.

---

## 3. Les Trois Propriétés Clés d'une Théorie

C'est souvent là-dessus que portent les questions d'examen.

### 1. Cohérence (Consistency)
Une théorie est cohérente si elle ne se contredit pas. Elle ne contient pas à la fois $\varphi$ et $\neg \varphi$.
* **Règle d'or :** Une théorie est cohérente si et seulement si elle a **au moins un modèle**.

### 2. Complétude (Completeness)
Une théorie est complète si elle a une opinion sur tout. Pour n'importe quelle phrase $\varphi$, soit elle dit "C'est vrai" ($\varphi \in T$), soit elle dit "C'est faux" ($\neg \varphi \in T$).
* **Astuce :** $Th(I)$ (théorie d'une structure) est **toujours complète** (car dans un monde précis, tout est soit vrai, soit faux).
* **Attention :** $Th(A)$ (axiomatique) n'est **pas forcément complète**. (Exemple : avec juste les axiomes d'ordre, on ne peut pas décider si l'ordre est dense ou discret).

### 3. Décidabilité
Une théorie est décidable s'il existe un algorithme (un programme) capable de dire si une formule $\varphi$ appartient à la théorie ou non.
* L'arithmétique simple ($\mathbb{N}, +, \times$) est **Indécidable** (Théorème de Gödel).
* L'arithmétique des nombres réels ou l'ordre dense ($\mathbb{Q}, <$) sont **Décidables** (souvent par élimination des quantificateurs).

---

## 🎓 Exercices Corrigés

### Exercice 1 : Théorie Axiomatique vs Structure
Soit la signature $L = \{<^{(2)}\}$.
Soit $A_{os}$ l'axiomatisation des **ordres stricts** (Irréflexivité, Transitivité).
Soit la structure $I = (\mathbb{N}, <)$ (les entiers avec l'ordre habituel).

**Questions :**
1.  Est-ce que la formule $\varphi = \exists x \forall y. (x \le y)$ (il existe un minimum) appartient à $Th(I)$ ?
2.  Est-ce que cette même formule appartient à $Th(A_{os})$ ?
3.  La théorie $Th(A_{os})$ est-elle complète ?

<details>
<summary>✅ Voir la correction</summary>

1.  **Appartenance à $Th(I)$ :**
    * On regarde dans le monde $\mathbb{N}$. Est-ce qu'il y a un minimum ?
    * Oui, $0$ est plus petit ou égal à tout le monde.
    * Donc $I \models \varphi$.
    * **Réponse : Oui.**

2.  **Appartenance à $Th(A_{os})$ :**
    * Est-ce que $\varphi$ est vraie dans **tous** les ordres stricts ? (C'est la définition de $Th(A)$).
    * Cherchons un contre-exemple : prenons les entiers relatifs $\mathbb{Z}$. C'est un ordre strict, mais il n'y a pas de minimum (ça descend vers $-\infty$).
    * Puisque c'est faux dans $\mathbb{Z}$ (qui est un modèle de $A_{os}$), ce n'est pas une conséquence logique des axiomes.
    * **Réponse : Non.**

3.  **Complétude :**
    * On vient de voir que $\varphi \notin Th(A_{os})$.
    * Est-ce que $\neg \varphi \in Th(A_{os})$ ? (Est-ce qu'il est interdit d'avoir un minimum ?).
    * Non, car $\mathbb{N}$ est un modèle de $A_{os}$ et il a un minimum.
    * La théorie ne décide ni $\varphi$, ni $\neg \varphi$.
    * **Réponse : Non, elle est incomplète.**
</details>

---

### Exercice 2 : Égalité et Quotient
Soit la signature avec un symbole de constante $c$ et un symbole de fonction $f$.
On considère l'interprétation $J$ :
* Domaine $D_J = \{0, 1, 2, 3\}$.
* $c^J = 0$.
* $f^J(x) = x$ (identité).
* $=^J = \{(0,0), (1,1), (2,2), (3,3), (0,1), (1,0), (2,3), (3,2)\}$ (Attention, ce n'est pas la vraie égalité !).

**Questions :**
1.  La relation $=^J$ est-elle une équivalence ?
2.  Décrivez l'interprétation quotient $J / =^J$.

<details>
<summary>✅ Voir la correction</summary>

1.  **Équivalence :**
    * Réflexive ? Oui (0,0), (1,1)... sont là.
    * Symétrique ? Oui (0,1) est là et (1,0) aussi.
    * Transitive ? Si $0=1$ et $1=0$, alors $0=0$. Ça a l'air bon.
    * **Réponse : Oui.**

2.  **Quotient :**
    * On regroupe les éléments liés par $=^J$.
    * $0$ est lié à $1$. Classe 1 : $\{0, 1\}$.
    * $2$ est lié à $3$. Classe 2 : $\{2, 3\}$.
    * **Nouveau Domaine :** Deux éléments abstraits $\{\{0,1\}, \{2,3\}\}$.
    * **Interprétation de $c$ :** C'était 0, c'est maintenant la classe $\{0, 1\}$.
    * **Interprétation de $f$ :** Elle renvoyait l'identique, elle renvoie maintenant la classe identique.
</details>