# Course Info 
## Time & score
- 2 discussion-identical: <u>Wed 18.30-19.30</u> or <u>Thu 16.30-17.30</u>
- Office hour: 助教 GSI+教授 Prof
- Piazza
- 15% HW, 85% Exam

## Final& Mid Term
- Mid: Oct sec half
- Final: 12.8 13.30-15.30

# Mathematical Arguments & Proof Techniques 
## Notation of Variables 
Eg. 
	$\mathbb{N}$,  
	$\mathbb{Z}=\{\cdots,-3,-2,-1,0,1,2,3, \cdots\}$, $\mathbb{Q}=\{m/q, q!=0, m,q \ with \ no \ common \ factors\}$ rational numbers,
	$\mathbb{R}$ =real numbers, 
	$\mathbb{C}=\{\alpha+j\beta, j^2=-1\}$ complex numbers
$\forall$ means for every, for each
$\exists$ means for some, there exists, for at least one
$\in$ means element of
$\text{s.t.}$ such that 使得
Eg.  
	Every real number x can be arbitrarily closely approximated by a rational number, how close is defined by epsilon:
$$
\DeclareMathOperator{\st}{s.t.}
\begin{gather}
\forall x \in \mathbb{R}, 
\ \forall \epsilon \in \mathbb{R}, 
\ \epsilon> 0, 
\\ \ \exists q \in \mathbb{Q},
\ \st |x-q|< \epsilon 
\end{gather}
$$
## Logic Notation 
~ means not 
$\wedge$ means logical and  
$\vee$ means logical or
p $\Rightarrow$ q means if p is true then q is true, p implies q
```ad-note
does not means q$\Rightarrow$p
The <u>__contrapositive__</u> of p $\Rightarrow$ q $\ \Leftrightarrow  \ \neg q \Rightarrow \neg p$
__useful for proof__
	P $\Leftrightarrow$ q means p is true if and only if q is true
	(P $\Leftrightarrow$ q) $\Leftrightarrow$ ((p $\Rightarrow$ q) $\wedge$ (q $\Rightarrow$ p))
```

Q.E.D. or QED is an abbreviation of the Latin “quod erat demonstrandum” which means “thus it was demonstrated”; it is used to alert the reader that a proof has been completed. Nowadays, you more frequently see □ or ■ instead of QED.

## Proof method
### Direct Proof 
### Proof by contrapositive   
```ad-note
$(p \Rightarrow q) \Leftrightarrow (\neg q \Rightarrow \neg p)$
```
### Proof by introduction
````ad-note
title: Standard induction
 Let P(n) denote a statement about the natural numbers with the following properties:
 
 (a) Base case: P(1) is true
 
 (b) Induction hypothesis: If P(k) is true, then P(k + 1) is true.
 
 Then P(n) is true for all n ≥ 1.

```ad-example
title:Example for Standard induction
 - claim:$\quad \forall n \ge 1, \ 1+3+5+\cdots + (2n+1)=n^2$
 
 - Step 1: Check the base case, P(1): For k = 1, we have that $1=1^2$, and hence the base case is true.
 
 - Step 2: Show the induction hypothesis is true. That is, using the fact that P(k) is true, show that P(k + 1) is true. Often, this involves re-writing P(k + 1) as a sum of terms that show up in P(k) and another term.
```
````

```ad-note
title: Strong induction
 Let P(n) be a statement about the natural numbers with the following properties:
 
 (a) Base Case: P(1) is true.
 
 (b) Induction hypothesis: If P(j) is true for all 1 ≤ j ≤ k, then P(k + 1) is true.
 
 Then P(n) is true for all n ≥ 1 (or, n greater than or equal to the n0 used in the Base Case).
```
###  Proof by contradiction
```ad-note

 - to prove p, just to assume $\neg p$ and prove $\exists R, \ \neg p \Rightarrow (R \wedge \neg R) = T$
 - to prove $(p \Rightarrow q)$, just to prove $\neg (p \wedge (\neg q))$
```

we assume $\neg q$ is true, then we assume $(p\wedge \neg q)$ is true, and we follow logical step to derive a statement that it is <u>false</u>. Hence it can not be that $p\Rightarrow \neg q$, hence it has to be that $p\Rightarrow q$.

```ad-example
title: proof by contradiction
theorem: $\sqrt{2}$ is irrational number
p:$\sqrt{2}$ is irrational numbers
$\neg p$: $\sqrt{2}$ is rational numbers
assume $\neg p$:
then $\exists m,n \in \mathbb{Z}$ s.t.
	$R_1:$ m,n have no common factors\
	$R_2:$ $\sqrt{2}=\frac{m}{n}$
$R_{2} \Rightarrow 2=\frac{m^{2}}{n^{2}}\Rightarrow2n^2=m^{2} \Rightarrow$ m is even
thus $\exists k\in \mathbb{N}$ s.t. m=2k
then $2n^{2}=m^{2}=4k^{2} \Rightarrow n^{2}=2k^{2}\Rightarrow n^{2}$ is even$\Rightarrow$ n is even
so we have proved that $R_{2}\wedge \neg R_{2}$ is True $\Rightarrow \ \neg p is false$
therefore p is true.
```
