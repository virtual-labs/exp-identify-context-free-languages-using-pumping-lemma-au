
#### 1. Context-Free Grammar (CFG)

A **Context-Free Grammar (CFG)** is a formal grammar that generates strings belonging to a context-free language.  
It is defined as a 4-tuple:

`G = (V, Σ, P, S)`

where:  
- **V** → Finite set of variables (nonterminals)  
- **Σ** → Finite set of terminals, with `V ∩ Σ = ∅`  
- **P** → Finite set of productions of the form `A → α`, where `A ∈ V` and `α ∈ (V ∪ Σ)*`  
- **S** → Start symbol, `S ∈ V`  

A string `w ∈ Σ*` belongs to the language `L(G)` if and only if  

`S ⇒* w`  
(i.e., `w` can be derived from `S` using the productions).


#### 2. Pumping Lemma for Context-Free Languages (CFLs)

The **Pumping Lemma for CFLs** is used to prove that certain languages are **not** context-free.

**Theorem (CFL Pumping Lemma):**  
If `L` is a context-free language, then there exists a pumping length `p ≥ 1` such that every string `s ∈ L` with `|s| ≥ p` can be written as:  

`s = u v x y z`

satisfying:  
1. `v y ≠ ε` (at least one of `v` or `y` is nonempty),  
2. `|v x y| ≤ p`,  
3. For all `i ≥ 0`, the string `u v^i x y^i z ∈ L`.  

**Important clarifications:**  
- `v` and `y` are not required to be identical.  
- `x` is not a “separator”; any of `u, x, z` may be empty.  
- Only the constraints `v y ≠ ε` and `|v x y| ≤ p` are guaranteed.  



#### 3. Why the Pumping Lemma Holds (Proof Sketch)

- Convert the grammar of `L` into **Chomsky Normal Form (CNF)**.  
- Let the number of variables be `k`.  
- Any parse tree deriving a sufficiently long string (`|s| ≥ p`) must contain a **long path** from root to leaf.  
- By the **pigeonhole principle**, some variable `A` repeats along this path:  

  `S ⇒* u A z ⇒* u v A y z ⇒* u v x y z`

- The repeated variable `A` allows **pumping**: replacing the subtree derived from the second `A` by more/fewer copies gives valid derivations.  
- This proves `u v^i x y^i z ∈ L` for all `i ≥ 0`.  
- The structure of the parse tree ensures that `|v x y| ≤ p` and `v y ≠ ε`.  



#### 4. Using the Pumping Lemma to Show a Language is Not Context-Free

To prove a language `L` is not context-free, proceed by **contradiction**:

1. **Assume** `L` is context-free.  
2. Let `p` be the pumping length from the lemma.  
3. **Choose** a specific string `s ∈ L` with `|s| ≥ p`.  
4. For **every valid decomposition** `s = u v x y z` satisfying  
   `|v x y| ≤ p` and `v y ≠ ε`,  
   show there exists some `i ≥ 0` (often `i = 0` or `i = 2`) such that:  

   `u v^i x y^i z ∉ L`

   which contradicts the lemma.  
5. Therefore, `L` is **not** context-free.  
