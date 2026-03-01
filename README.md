Universal Tuple Sequence Explorer

This tool maps the exact structural consequences of sequence-generating rules. By defining strict relationships between the elements of a tuple and the base-represented digits of an index, we isolate and observe unmapped mathematical patterns.

The Mathematics

For any integer 
𝑛
n
:

Base Extraction: Represent 
𝑛
n
 in base 
𝑏
≥
2
b≥2
 to get a sequence of 
𝑘
k
 digits: 
𝑛
=
(
𝑑
1
𝑑
2
…
𝑑
𝑘
)
𝑏
n=(d
1
	​

d
2
	​

…d
k
	​

)
b
	​

.

Tuple Construction: We define a tuple of length 
𝑘
+
1
k+1
: 
𝑋
=
(
𝑥
1
,
𝑥
2
,
…
,
𝑥
𝑘
+
1
)
X=(x
1
	​

,x
2
	​

,…,x
k+1
	​

)
, where every element is bounded by the base: 
0
≤
𝑥
𝑗
≤
𝑏
−
1
0≤x
j
	​

≤b−1
.

The Rule: The tuple is valid if it satisfies a sequential constraint for every index 
𝑖
i
 from 
1
1
 to 
𝑘
k
. The constraint equates a Left-Hand Side (LHS) operation on the tuple elements (e.g., 
∣
𝑥
𝑖
−
𝑥
𝑖
+
1
∣
∣x
i
	​

−x
i+1
	​

∣
) to a Right-Hand Side (RHS) condition dictated by 
𝑑
𝑖
d
i
	​

 (e.g., 
=
𝑑
𝑖
=d
i
	​

).

The Value: 
𝑎
(
𝑛
)
a(n)
 is the exact count of unique tuples 
𝑋
X
 that satisfy the rule.

The Mapping: We evaluate 
𝑎
(
𝑛
)
(
m
o
d
𝑚
)
a(n)(modm)
 and map the result to a discrete color palette on a 2D coordinate grid.

The Engine

Brute-forcing 
𝑏
𝑘
+
1
b
k+1
 configurations per integer is inefficient and limits discovery. The tool instead uses a 
𝑂
(
𝑘
⋅
𝑏
2
)
O(k⋅b
2
)
 state-transition algorithm:

We maintain a state vector of size 
𝑏
b
 tracking the count of valid tuple prefixes ending in each possible integer state.

For each digit 
𝑑
𝑖
d
i
	​

, we construct a boolean mask of valid RHS targets.

We calculate the LHS operation for all current and subsequent states. If it hits a valid target in the mask, the path count carries forward.

Addition is performed modulo 
𝑚
m
 at every step to prevent integer overflow. The final sum of the state vector modulo 
𝑚
m
 yields 
𝑎
(
𝑛
)
(
m
o
d
𝑚
)
a(n)(modm)
.

Tool Operation

The interface is built to test rules and isolate variables rapidly.

Ruleset

LHS: The mechanical operation linking tuple elements.

RHS 1 & 2: The target conditions.

Logic: Combine two RHS constraints using AND (intersection) or OR (union).

Viewer

Base (
𝑏
b
): Sets the digit extraction base and the tuple element limits.

Scale: Sets the grid dimensions (
𝑏
×
𝑏
b×b
, 
𝑏
2
×
𝑏
2
b
2
×b
2
, or 
𝑏
3
×
𝑏
3
b
3
×b
3
).

Modulo (
𝑚
m
): Bounds 
𝑎
(
𝑛
)
a(n)
 and defines the exact number of colors in the generated palette.

Block (
𝑝
p
): Offsets the starting integer 
𝑛
n
 by 
𝑝
×
total grid cells
p×total grid cells
.

Data Log: An uneditable text field continuously outputs the exact formula and parameters of the current render for precise record-keeping.

High-Res Export: Compiles a static PNG of the exact grid state up to 
4000
×
4000
4000×4000
 pixels.

Animator
Compiles structural shifts into GIFs to observe transformations over defined parameters.

Mode A: Fixes the base, sequentially increments the Block (
𝑝
p
). Maps continuous numerical space.

Mode B: Fixes the block, sequentially increments the Base (
𝑏
b
). Maps structural scaling.

Mode C: Fixes the base and block, sequentially increments the Modulo (
𝑚
m
). Maps internal periodicity.
