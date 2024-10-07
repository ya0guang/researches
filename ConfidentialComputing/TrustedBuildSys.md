# Trusted Build System

## Attestation of Data

- For AI applications, ensuring the trustworthiness of training data is important.
- The software supply chain of AI models are not only the executable code, but also the model, and even the training data/process
- We should be able to conduct *backward* attestation not only to the build environment, but also to the training data/process.
- This might be achieved via the blockchain.

## Concerns

- Proprietary Code
- Policy Compliance

## Potential Solutions

- Correspondence between users' requests and responses: non-interference
- Add another layer to obfuscate users

## Related Work

- [Why Should I Trust Your Code?: Confidential computing enables users to authenticate code running in TEEs, but users also need evidence this code is trustworthy.](https://dl.acm.org/doi/abs/10.1145/3623460)

## Related Projects

- [https://reproducible-builds.org/](https://reproducible-builds.org/)
