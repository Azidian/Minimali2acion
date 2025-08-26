# DFA Minimization Algorithm Implementation

## Student Information
- **Student's Full Name:** [Tu nombre completo aquí]
- **Student's Class Number:** [Tu número de clase aquí]

## System Information
- **Operating System:** Windows 11 / macOS / Ubuntu 20.04 (especifica el tuyo)
- **Programming Language:** Java 11+
- **Tools Used:** 
  - Java Development Kit (JDK) 11 or higher
  - Any Java IDE (IntelliJ IDEA, Eclipse, VS Code) or command line

## Running Instructions

### Compilation
```bash
javac DFAMinimization.java
```

### Execution
```bash
java DFAMinimization
```

### Input Format
The program reads from standard input with the following format:
1. Number of test cases
2. For each test case:
   - Number of states
   - Alphabet symbols separated by spaces
   - Final states separated by spaces
   - Transition table (one row per state)

### Example
```
4
6
a b
1 2 5
0 1 2
1 3 4
2 4 3
3 5 5
4 5 5
5 5 5
```

## Algorithm Explanation

This implementation uses the **Table Filling Method** for DFA minimization, which is based on the algorithm presented in Kozen's "Automata and Computability" Lecture 14. The algorithm finds equivalent states that can be collapsed to create a minimal DFA.

### Algorithm Steps:

1. **Initial Marking Phase:**
   - Create a table for all pairs of states (p, q)
   - Mark pairs as distinguishable if one state is final and the other is not
   - This ensures that final and non-final states are never considered equivalent

2. **Iterative Refinement Phase:**
   - For each unmarked pair of states (p, q):
   - Check if there exists an input symbol 'a' such that δ(p,a) and δ(q,a) lead to states that are already marked as distinguishable
   - If such a symbol exists, mark (p, q) as distinguishable
   - Repeat until no new pairs are marked in an iteration

3. **Result Collection:**
   - All unmarked pairs represent equivalent states
   - These states can be merged in the minimal DFA
   - Output pairs are sorted lexicographically as required

### Key Concepts:

- **Equivalent States:** Two states p and q are equivalent if for any input string x, both states either lead to acceptance or both lead to rejection
- **Distinguishable States:** States that are not equivalent - there exists at least one string that leads to different outcomes (accept/reject) from each state
- **Minimization:** The process of merging equivalent states to create the smallest possible DFA that recognizes the same language

### Time Complexity:
- O(n² × |Σ| × k) where n is the number of states, |Σ| is the alphabet size, and k is the number of iterations
- In the worst case, this is O(n³ × |Σ|)

### Space Complexity:
- O(n²) for the distinguishability table

The algorithm guarantees to find all equivalent states and produces the minimal DFA by identifying which states can be collapsed together while preserving the language recognition properties of the original automaton.
