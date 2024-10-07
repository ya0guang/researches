# TEE Firmware Security

## Papers

- [EL3XIR: Fuzzing COTS Secure Monitors](https://nebelwelt.net/files/24SEC2.pdf)

## Formal Verification

- [Design and Verification of the Arm Confidential Compute Architecture](https://www.usenix.org/conference/osdi22/presentation/li)

## Fuzzing

- [QEMU 9.1 Supports Firmware Emulation](https://wiki.qemu.org/ChangeLog/9.1#Tricore)

## Known Vulnerabilities

Seems like some vulnerabilities are found by [trivy](https://github.com/aquasecurity/trivy)? See [this post](https://github.com/aquasecurity/trivy/discussions/7302).

### SEV

- [freax13's blog](https://blog.freax13.de/)
- [Blackhat Talk: All Your Secrets Belong to Us: Leveraging Firmware Bugs to Break TEEs](https://www.blackhat.com/us-24/briefings/schedule/#all-your-secrets-belong-to-us-leveraging-firmware-bugs-to-break-tees-40137) PoC listed in presentation
- [CVE-2024-21980](https://nvd.nist.gov/vuln/detail/CVE-2024-21980)
- [QEMU Emulation](https://www.phoronix.com/news/QEMU-9.1-Released)

### TDX

- [microsoft/Cornelius](https://github.com/microsoft/Cornelius)
- [Technical Report from MS](https://www.intel.com/content/dam/www/public/us/en/security-advisory/documents/intel_tdx_joint_security_review_with_microsoft.pdf)
- [Blackhat Slides](https://i.blackhat.com/BH-US-24/Presentations/US24-Villard-Compromising-Confidential-Compute-One-Bug-Wednesday.pdf)