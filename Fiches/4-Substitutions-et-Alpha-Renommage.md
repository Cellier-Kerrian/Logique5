# Fiche 4 : Substitutions et $\alpha$-renommage

Basé sur la section 13 du polycopié de cours "Introduction à la Logique Informatique".

## 1. Substitutions ($\sigma$)

Une substitution, c'est l'action de **remplacer une variable libre par un terme**. C'est une opération purement **syntaxique** (on réécrit du texte).

* **Notation :** $\sigma = [t/x]$
* **Signification :** "Remplacer toutes les occurrences **libres** de $x$ par le terme $t$."
* **Exemple sur un terme :**
    * Terme : $g(x, h(y, x))$
    * Substitution : $[a/x]$ (remplacer $x$ par la constante $a$)
    * Résultat : $g(a, h(y, a))$

---

## 2. Le Piège : La "Capture" de variable

Appliquer une substitution à une formule est dangereux. On dit qu'une substitution $\sigma$ n'est **pas applicable** à une formule $\varphi$ si elle change le sens de la formule en "capturant" une variable.

**Scénario de la capture :**
1.  Tu as une formule $\varphi = \exists y. (x < y)$. (Sens : "il existe un $y$ plus grand que $x$").
2.  Tu veux appliquer la substitution $\sigma = [y/x]$ (remplacer $x$ par $y$).
3.  Tu remplaces naïvement : $\exists y. (y < y)$.
4.  **Catastrophe !** Le sens a changé. La formule signifie maintenant "il existe un $y$ plus grand que lui-même", ce qui est faux. Le $y$ que tu as inséré a été capturé par le quantificateur $\exists y$ qui était déjà là.

---

## 3. La Solution : L'$\alpha$-renommage

Pour éviter la capture, on utilise l'$\alpha$-renommage.
C'est simplement le fait de **renommer une variable liée (muette)**, ce qui ne change pas le sens de la formule.

* $\exists y. (x < y)$ est **$\alpha$-équivalent** à $\exists z. (x < z)$.

**Comment on l'utilise pour substituer :**
1.  Formule : $\varphi = \exists y. (x < y)$
2.  Substitution : $\sigma = [y/x]$
3.  **Étape 1 (Renommage)** : On renomme $\varphi$ en $\varphi' = \exists z. (x < z)$ pour éviter le conflit.
4.  **Étape 2 (Substitution)** : On applique $\sigma$ à $\varphi'$ : $\exists z. (y < z)$.
5.  Le sens est préservé !

---

## 🎓 Exercices Corrigés

### Exercice 1 : Substitution simple
* **Terme :** $t = f(x, y)$
* **Formule :** $\varphi = P(x) \vee R(z, a)$
* **Substitution :** $\sigma = [g(y)/x, b/z]$

**Questions :**
1.  Quel est le terme $t\sigma$ ?
2.  Quelle est la formule $\varphi\sigma$ ?

<details>
<summary>✅ Voir la correction</summary>

1.  **Terme $t\sigma$ :**
    * $f(x, y) \sigma = f(g(y), y)$
    * **Résultat :** $f(g(y), y)$ (On remplace $x$ par $g(y)$. La variable $z$ n'est pas dans le terme, et $y$ n'est pas remplacée par $\sigma$).

2.  **Formule $\varphi\sigma$ :** On remplace $x$ par $g(y)$ et $z$ par $b$.
    * $(P(x) \vee R(z, a)) \sigma = P(g(y)) \vee R(b, a)$
    * **Résultat :** $P(g(y)) \vee R(b, a)$
</details>

---

### Exercice 2 : Substitution avec capture
* **Formule :** $\varphi = (\forall x. R(x, y)) \vee P(x)$
* **Substitution :** $\sigma = [f(x)/y]$

**Questions :**
1.  La substitution $\sigma$ est-elle **applicable** directement ? Pourquoi ?
2.  Quel est le résultat correct $\varphi\sigma$ (en utilisant l' $\alpha$-renommage s'il le faut) ?

<details>
<summary>✅ Voir la correction</summary>

1.  **Applicabilité : Non.**
    * La variable à remplacer est $y$ (qui est libre).
    * Le terme remplaçant est $f(x)$.
    * La variable $y$ apparaît dans la sous-formule $(\forall x. R(x, y))$.
    * Le $x$ du terme $f(x)$ serait "capturé" par le quantificateur $\forall x$, ce qui change le sens de la formule.

2.  **Résultat correct :**
    * **Étape 1 ($\alpha$-renommage) :** On doit renommer la variable liée $\forall x$ qui pose problème. Prenons $z$.
    * $\varphi' = (\forall z. R(z, y)) \vee P(x)$.
    * **Étape 2 (Substitution) :** On applique $\sigma = [f(x)/y]$ à $\varphi'$.
    * Le $y$ de la partie gauche est remplacé. Le $P(x)$ de droite n'est pas affecté (car $y$ n'y est pas libre).
    * **Résultat :** $(\forall z. R(z, f(x))) \vee P(x)$
</details>