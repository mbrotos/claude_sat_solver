# Claude SAT Solver with Tool Use
 
A demonstration of Claude 3 Opus's tool use capabilities through a SAT (Boolean Satisfiability) solver implementation. The system uses structured tool definitions to parse natural language logic problems into a symbolic theorem prover format.

Dependencies:
- anthropic
- z3-solver (Z3 is a symbolic theorem prover from [Microsoft Research](https://github.com/Z3Prover/z3).)
- pydantic

You will need an Anthropic API key to run the code.

See [claude_sat_solver.ipynb](claude_sat_solver.ipynb)

Run it yourself on colab:

<a href="https://colab.research.google.com/github/mbrotos/claude_sat_solver/blob/main/claude_sat_solver.ipynb" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>
---
### Example I/O
```
==================================================
Test Case 1:

        Consider the following SAT problem in propositional logic:
        1. If it rains, the ground will be wet.
        2. If it is cloudy, it will rain.
        3. If the ground is not wet, then it is not cloudy.
        4. The ground is not wet.
        Determine if this set of statements is consistent (satisfiable) using propositional logic and the resolution method.
        
Claude's response:
	<thinking>
	To analyze this SAT problem, we need to first convert the given statements into propositional logic clauses. Let's define the following variables:
	
	r: It rains
	w: The ground is wet 
	c: It is cloudy
	
	The statements can be converted as follows:
	
	1. If it rains, the ground will be wet. 
	   r → w
	   This can be written as (~r ∨ w)
	
	2. If it is cloudy, it will rain.
	   c → r 
	   This can be written as (~c ∨ r)
	
	3. If the ground is not wet, then it is not cloudy.
	   ~w → ~c
	   This can be written as (w ∨ ~c)
	
	4. The ground is not wet.
	   ~w
	
	So the set of clauses is:
	(~r ∨ w), (~c ∨ r), (w ∨ ~c), ~w
	
	To put this into the SATParser tool, we need to specify:
	- The variables used: r, w, c 
	- The list of clauses, with each clause being a list of literals. Use '~' to represent negation.
	
	With this information specified, we can use the SATParser tool to convert this into a structured format that can be used to check satisfiability.
	</thinking>
	Tool use: SATParser
	Tool input: {'variables': ['r', 'w', 'c'], 'clauses': [['~r', 'w'], ['~c', 'r'], ['w', '~c'], ['~w']]}


Result: Satisfiable

Ground truth Z3 clauses: [Or(Not(r), w), Or(Not(c), r), Or(w, Not(c)), Or(Not(w))]
Z3 result: Satisfiable
==================================================
```
