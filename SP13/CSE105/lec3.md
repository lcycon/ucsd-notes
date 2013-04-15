# State machines

**Def**: A DFA is a state maching = $(Q,\Sigma,\delta,s,F)$ while

- Q is a finite set of states
- $\Sigma$ is a finite set of input symbols
- $\delta: Q \times \Sigma \rightarrow Q$
- $s \in Q$
- $F \in Q$

**Def**: $\delta^*: Q \times \Sigma^* \rightarrow Q$

By induction of length of $w$

(1) Base case: $( |\varepsilon| = 0)$  
    $\delta^*(q, \varepsilon) = q$
(2) Induction $( |aw| > 1 )$  
    $\delta^*(q, aw) = \delta^*(q, a)$

## Example

Multiples of three (given binary)

$\delta$  A    B   C
-------   --   --  ---
0         A    C   B
1         B    A   C

\begin{equation*}
    f_M: \Sigma^* \rightarrow {0,1}
\end{equation*}

\begin{equation*}
    f_M(w)= \begin{cases}
      0, \text{if } \delta^*(s,w) \notin F \\
      1, \text{if } \delta^*(s,w) \in F
    \end{cases}
\end{equation*}

\begin{equation*}
    \delta^*(B,01101) = A
\end{equation*}

## Operational Description of computation

Definition                        For DFA
-----------                       --------
(1) $C$: Set of conjugations      $C=Q \times \Sigma^*$
(2) $R \subseteq C \times C$      $R = {(q, aw), (\delta(q,a), w)}$  
                                  $q \in Q, a \in \Sigma, w \in \Sigma^*$
(3) $I: \Sigma^* \rightarrow C$   $I(w) = (s, w)$
(4) $O: C_F \rightarrow {0,1}$    

**Def**: A computation on input $w$ in a sequence of conjugations
$c_1, c_2, c_3,..., c_n \in C$ such that

(1) $c_1 = I(w)$
(2) $c_i \rightarrow c_(i + 1), \forall i=1$
(3) $c_n \in C_F$
