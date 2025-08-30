### Theory

#### 1. Context-Free Grammar (CFG)

A **Context-Free Grammar (CFG)** is a formal grammar used to generate strings of a context-free language. A CFG is a 4-tuple  
\[
G = (V, \Sigma, P, S)
\]
where:
- **V**: finite set of variables (nonterminals).
- **Σ**: finite set of terminals, with \(V \cap \Sigma = \varnothing\).
- **P**: finite set of productions of the form \(A \rightarrow \alpha\), where \(A \in V\) and \(\alpha \in (V \cup \Sigma)^*\).
- **S**: start symbol, \(S \in V\).

A string \(w \in \Sigma^*\) is in the language \(L(G)\) if \(S \Rightarrow^* w\) (i.e., \(w\) can be derived from \(S\) using the productions).

---

#### 2. Pumping Lemma for Context-Free Languages (CFLs)

The **pumping lemma for CFLs** is typically used to prove that a language is **not** context-free.

##### Theorem (CFL Pumping Lemma)
If \(L\) is a context-free language, then there exists a pumping length \(p \ge 1\) such that **every** string \(s \in L\) with \(|s| \ge p\) can be written as
\[
s = u v x y z
\]
satisfying:
1. \(v y \neq \varepsilon\) (i.e., at least one of \(v\) or \(y\) is nonempty),
2. \(|v x y| \le p\),
3. For **all** \(i \ge 0\), the string \(u\,v^{\,i}\,x\,y^{\,i}\,z \in L\).

> **Important fixes to common errors (Step 4 misconceptions):**
> - \(v\) and \(y\) are **not** required to be identical or “copies” of each other.  
> - \(x\) is **not** a special “separator”; any of \(u, x, z\) may be empty.  
> - The only guaranteed constraints are \(v y \neq \varepsilon\) and \(|v x y| \le p\).

---

#### 3. Why the Pumping Lemma Holds for CFLs (Proof Sketch)

- Convert the grammar of \(L\) to **Chomsky Normal Form (CNF)**. Let the number of variables be \(k\).
- Any parse tree deriving a sufficiently long string (\(|s| \ge p\) for some \(p\) depending on \(k\)) must contain a **long path** from the root to a leaf.
- By the **pigeonhole principle**, some variable \(A\) repeats along that path:  
  \(S \Rightarrow^* u A z \Rightarrow^* u v A y z \Rightarrow^* u v x y z\).
- The portion derived by the lower occurrence of \(A\) can be “pumped”: replacing that subtree by either **more** or **fewer** copies preserves a valid derivation because \(A \Rightarrow^* x\) and \(A \Rightarrow^* v x y\).  
  This yields \(u\,v^{\,i}\,x\,y^{\,i}\,z \in L\) for all \(i \ge 0\).
- Structural bounds on the parse tree ensure \(|v x y| \le p\) and that \(v y\) is not empty.

---

#### 4. How to Use the Pumping Lemma to Show \(L\) is **Not** Context-Free

To prove a language \(L\) is **not** context-free, use a **proof by contradiction**:

1. **Assume** \(L\) is context-free.  
2. Let \(p\) be the pumping length guaranteed by the lemma.  
3. **Choose** a specific string \(s \in L\) with \(|s| \ge p\) (choose \(s\) strategically).  
4. **For every** valid decomposition \(s = u v x y z\) satisfying  
   \(|v x y| \le p\) and \(v y \neq \varepsilon\),  
   **show there exists** some \(i \ge 0\) (often \(i=0\) or \(i=2\)) such that
   \[
   u\,v^{\,i}\,x\,y^{\,i}\,z \notin L.
   \]
   This contradicts the lemma’s condition (3).  
5. Conclude that the assumption was false, so \(L\) is **not** context-free.

> **Notes & Pitfalls**
> - You must handle **all** valid decompositions (the adversary chooses \(u,v,x,y,z\) after seeing your \(s\)).  
> - The lemma is a **necessary condition**, not sufficient: some non-CFLs may accidentally satisfy a pumping-like property for certain strings; the lemma alone does not characterize all CFLs.

---
