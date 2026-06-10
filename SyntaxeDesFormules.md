# Syntaxe des Formules Propositionnelles

## Notion
Comment écrire correctement les formules logiques.

## Syntaxe Abstraite
Définit la structure fondamentale des formules comme des arbres.
* Les feuilles sont des **propositions** (variables, $P, Q \in \mathcal{P}_0$).
* Les nœuds internes sont des **connecteurs** ($\neg$, $\vee$, $\wedge$).
* Définition formelle : $\varphi::=P|\neg\varphi|\varphi\vee\varphi|\varphi\wedge\varphi$ où $P\in\mathcal{P}_0$.
* Exemple : L'arbre de la Figure 1 (page 9) représente $((P \vee \neg Q) \wedge P)$.

## Syntaxe Concrète
L'écriture linéaire avec parenthèses que l'on utilise couramment.
* Exemple : $((P \vee \neg Q) \wedge P)$.
* **Abréviations courantes**:
    * $\phi\Rightarrow\psi$ est une abréviation de $\neg\phi\vee\psi$.
    * $\phi\Leftrightarrow\psi$ est une abréviation de $(\phi\wedge\psi)\vee(\neg\phi\wedge\neg\psi)$ (ou $(\phi \Rightarrow \psi) \wedge (\psi \Rightarrow \phi)$).
* **Astuce** : Bien parenthéser pour éviter les ambiguïtés, même si $\wedge$ et $\vee$ sont associatifs.

## Propositions dans une formule `fp(φ)`
L'ensemble des variables propositionnelles qui apparaissent (au moins une fois) dans $\varphi$.
* $fp(P) = \{P\}$
* $fp(\neg\varphi) = fp(\varphi)$
* $fp(\varphi\vee\psi) = fp(\varphi)\cup fp(\psi)$
* $fp(\varphi\wedge\psi) = fp(\varphi)\cup fp(\psi)$
* Exemple : $fp(((P \vee \neg Q) \wedge P)) = \{P, Q\}$.

## Représentation (Java/OCaml)
Le cours montre comment implémenter ces arbres (Sections 2.1.1, 2.1.2).
