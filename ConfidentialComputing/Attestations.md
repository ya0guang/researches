# Ideas on Attestation

## Attestation of Data

- For AI applications, ensuring the trustworthiness of training data is important.
- The software supply chain of AI models are not only the executable code, but also the model, and even the training data/process
- We should be able to conduct *backward* attestation not only to the build environment, but also to the training data/process.
- This might be achieved via the blockchain.

## Attestation and FaaS

- On heterogeneous backends in FaaS, measurement can be different (e.g. because architecture, applied optimizations, etc.). We want a unified view of measurements across different backends.
- Another thing is about the workflow. When several functions are orchestrated as a workflow, we then not only need to conduct attestation to a single task, but to the whole workflow. *what are the challenges here?*

