# qosf-2020-tasks

## Task 2 and Task 3 submissions for QOSF 2020

**Approach to completing tasks:** 

### Task 2 

#### Requirements: 

*Implement a circuit that returns |01> and |10> with equal probability.
Requirements :
The circuit should consist only of CNOTs, RXs and RYs. 
Start from all parameters in parametric gates being equal to 0 or randomly chosen. 
You should find the right set of parameters using gradient descent (you can use more advanced optimization methods if you like). 
Simulations must be done with sampling (i.e. a limited number of measurements per iteration) and noise.*

*Compare the results for different numbers of measurements: 1, 10, 100, 1000. 

*Bonus question:
How to make sure you produce state |01> + |10> and not |01> - |10> ?

*(Actually for more careful readers, the “correct” version of this question is posted below:
How to make sure you produce state  |01⟩  +  |10⟩  and not any other combination of |01> + e(i*phi)|10⟩ *(for example |01⟩  -  |10⟩)?)

## Approach: 

|01> + |10> and |01> - |10> are Bell pairs 
The chance of getting |01> and |10> are both 50% each. 
One way of doing this would be implementing an X, CNOT and Hadamard gate

|Φ+⟩ = CNOT ⋅ H1|00⟩ 
|Ψ+⟩=X2|Φ+⟩=X2⋅CNOT⋅H1|00⟩

A Hadamard gate can be decomposed into RY(-pi/2) and RX(pi) or RX(-pi) and RY(pi/2)
The RY gate shifts the phase of the first qubit by pi/2 and an RX gate will be applied to the second qubit to flip it from |0> to |1>. Once both qubits are run through a CNOT, the measurement results will be |01> and |10>. 

Applying gradient descent: the values of the parameters will be randomly set and gradient descent will be applied for the RY gate to have (pi/2) mapped to |+> in qubit one and for the RX gate to have pi mapped to |1> in qubit two. 

Bonus Question: 
Differentiating between |01> + |10> and |01> - |10>  require more gates. With an RX and RY gate, the state is mapped |+> to |0> and |-> to |1>. The |+> state of the first qubit with the CNOT gate results in the state |01> + |10>  while the |-> state with the CNOT gate results in the state |01> - |10>. The first qubit must be in the |+> state. In order to do that, with a starting qubit at |0>, a pi/2 rotation on the y-axis will map it to |+> and a 3pi/2 rotation on the y-axis will map it to |->. 

# Task 3

## Requirements: 

*Please write a simple compiler – program, which translates one quantum circuit into another, using a restricted set of gates.

*You need to consider just the basic gates for the input circuit, such as (I, H, X, Y, Z, RX, RY, RZ, CNOT, CZ).

*The output circuit should consist only from the following gates: RX, RZ, CZ. In other words, each gate in the original circuit must be *replaced by an equivalent combination of gates coming from the restricted set (RX, RZ, CZ) only.

*For example, a Hadamard gate after compilation looks like this:

*RZ(pi/2)
*RX(pi/2)
*RZ(pi/2)

## Approach: 

The compiler takes a quantum circuit with an arbitrary sample 1 and 2 qubit gates while compiling it to a quantum circuit with the CZ, RX and RZ gates. 
It is a very simple translator that takes any quantum circuit made up of the basic gates I, S, H, X, Y, Z, RX, RY, RZ, CNOT, CZ to convert into a combination of gates RX, RZ and CZ.

Mathematical operations and definitions of the quantum logic gates:




