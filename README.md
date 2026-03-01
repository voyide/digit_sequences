


# Universal Tuple Sequence Explorer

This tool maps the exact structural consequences of sequence-generating rules. By defining strict relationships between the elements of a tuple and the base-represented digits of an index, we isolate and observe unmapped mathematical patterns.

## The Mathematics

For any integer $n$:

1. **Base Extraction:** Represent $n$ in base $b \ge 2$ to get a sequence of $k$ digits: $n = (d_1 d_2 \dots d_k)_b$.
2. **Tuple Construction:** We define a tuple of length $k + 1$: $X = (x_1, x_2, \dots, x_{k+1})$, where every element is bounded by the base: $0 \le x_j \le b - 1$.
3. **The Rule:** The tuple is valid if it satisfies a sequential constraint for every index $i$ from $1$ to $k$. The constraint equates a **Left-Hand Side (LHS)** operation on the tuple elements (e.g., $|x_i - x_{i+1}|$) to a **Right-Hand Side (RHS)** condition dictated by $d_i$ (e.g., $= d_i$).
4. **The Value:** $a(n)$ is the exact count of unique tuples $X$ that satisfy the rule.
5. **The Mapping:** We evaluate $a(n) \pmod m$ and map the result to a discrete color palette on a 2D coordinate grid.

## The Engine

Brute-forcing $b^{k+1}$ configurations per integer is inefficient and limits discovery. The tool instead uses a $O(k \cdot b^2)$ state-transition algorithm:
* We maintain a state vector of size $b$ tracking the count of valid tuple prefixes ending in each possible integer state.
* For each digit $d_i$, we construct a boolean mask of valid RHS targets.
* We calculate the LHS operation for all current and subsequent states. If it hits a valid target in the mask, the path count carries forward.
* Addition is performed modulo $m$ at every step to prevent integer overflow. The final sum of the state vector modulo $m$ yields $a(n) \pmod m$.

## Tool Operation

The interface is built to test rules and isolate variables rapidly. 

**Ruleset**
*   **LHS:** The mechanical operation linking tuple elements.
*   **RHS 1 & 2:** The target conditions.
*   **Logic:** Combine two RHS constraints using `AND` (intersection) or `OR` (union).

**Viewer**
*   **Base ($b$):** Sets the digit extraction base and the tuple element limits.
*   **Scale:** Sets the grid dimensions ($b \times b$, $b^2 \times b^2$, or $b^3 \times b^3$).
*   **Modulo ($m$):** Bounds $a(n)$ and defines the exact number of colors in the generated palette.
*   **Block ($p$):** Offsets the starting integer $n$ by $p \times \text{total grid cells}$.
*   **Data Log:** An uneditable text field continuously outputs the exact formula and parameters of the current render for precise record-keeping.
*   **High-Res Export:** Compiles a static PNG of the exact grid state up to $4000 \times 4000$ pixels.

**Animator**
Compiles structural shifts into GIFs to observe transformations over defined parameters.
*   **Mode A:** Fixes the base, sequentially increments the Block ($p$). Maps continuous numerical space.
*   **Mode B:** Fixes the block, sequentially increments the Base ($b$). Maps structural scaling.
*   **Mode C:** Fixes the base and block, sequentially increments the Modulo ($m$). Maps internal periodicity.
