regular grammar(tyte 3)을 accept되게 만들어주는 것이 NDFSA이지만 기계가 난해하게 만들어져있기 때문에 DFSA로 바꿔주는 것임. NDFSA에서도 accept되겠지만 NDFSA를 바탕으로 한 DFSA에서도 accept되는 것은 당연하다.

# DFSA 만들기

다음과 같은 regular grammar에 의해 정의된 NDFSA 가 주어졌을 때

- $N = \{\sigma, c, F\}$

- $T = \{a, b\}$

- $$
  \sigma \to bC \\
  \sigma \to aC \\
  C \to bC \\
  C \to bF \\
  F \to \lambda
  $$

- 



1. $s\closure = ​$ 만들기
2. DFSA의 accepting state s*중 기존 NDFSA의 accepting state를 포함하는 원소를 accepting state로 결정
   1. $\sigma \to a \to C$
   2. $\sigma \to b \to \sigma$
   3. $C \to a \to \emptyset$
   4. $C \to b \to \{C,F\}$
   5. $\{\sigma, F\} \to a \to C$
3. 도달 불가능한 state들을 지워 냄.

695page 그림 5.1 label의 b로 표기된 내용을 a로 바꿔야 함

NDFSA의 accepting state는 double circle

DFSA의 accepting state s*중 기존 NDFSA의 accepting state 포함하는 원소를 accepting state로 결정

NDFSA를 DFSA로 만들기 위해 필요한 state의 수는 2^n(s)