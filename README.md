# researches

## Random Ideas

### The myth of TCB size and verifiability

- TCB metrics are usually to tricky: LoC, binary size
- How to extract the TCB size from the source code?
- Can we quantify TCB size in a better way?
- Can we quantify verifiability in a better way?
- Different levels of verifiability/TCB:
  - design
  - realization
  - system
- If a module is verified, how safe can we remove it from the TCB?
- How much security is gained by reducing the TCB?
- For a specific functionality, what's the minimal TCB size to achieve it?

#### TCB and Verification

- If there is a way to formally specify the functionality, there should be a minimal representation of the functionality, thus there should exist a minimal TCB size.

#### Hypervisors to Reduce TCB

- TrustVisor: Efficient TCB Reduction and Attestation
- Flicker: An Execution Infrastructure for TCB Minimization
