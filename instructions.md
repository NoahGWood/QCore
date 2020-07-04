# Instructions

## Supported Gates
### Unitary Gates
* Pauli-X
* Pauli-Y
* Pauli-Z
* Hadamard

### Controlled Gates
* Controlled-X
* Controlled-Y
* Controlled-Z
* Controlled-H

### Additional Operations
* SWAP
* MEASURE

## Quantum RAM
Quantum RAM is different from digital RAM, the TTL of a photon in RAM is extremely short, and unlike digital RAM it is unable to be refreshed at this time. Future revisions may introduce some form of RAM refreshing, but that is beyond the scope of the current project.

The QRAM consists of a physical loop of fiberoptic wire intersected by a MEMS switch which when set HIGH allows the photon to exit the delay loop. The size of each loop is variable with the number of qubits to ensure that the time to travel to any point in the circuit does not vary, reducing the workload in synchronization.

### MEMS Toggle
Each qubit in the Quantum RAM has a toggle pin, when set to HIGH it will open releasing the trapped photon.
Additionally, the controlled gates have N+1 toggle pins, where N is equal to the number of qubits.

The total number of toggle pins for the QRAM is 2N+1 qubits, although this should be manually verified when qubits are added.

## Qubit Set/Reset
Each qubit has a single pin for setting/resetting the state of the Qubit. HIGH sets the qubit state to 1 and LOW sets the qubit state to 0.

## Triggers
### Qubit
Each qubit has a Qubit Trigger. At the start of any computation, for any Qubit in the system this pin is pulled HIGH to trigger the single-photon source.
### Controlled Gateds
Each controlled gate has a toggle pin which is used to generate the ancilla photons; this must be pulsed HIGH every time the controlled gate command is issued.

## Post-processing
### Qubit Results
Each Qubit has an output and a secondary bit which are compared in circuit; this pin should remain HIGH, if the pin goes LOW this means more than 1 photon was detected and the results of that trial should be discarded

### Controlled Gate Results
Each Controlled Gate has two auxiliary modes and detectors wired into a NAND gate, the output should be normally LOW, pulse HIGH when the controlled gate is used, and then back to LOW. If the controlled gate is called and the gate does not return a HIGH state, the gate has failed and a new trial of processing should begin.


