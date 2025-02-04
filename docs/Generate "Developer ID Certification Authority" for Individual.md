# Generate "Developer ID Certification Authority" for Individual

**Create a new certificate signing request (CSR) for the Developer ID Certification Authority for Individual.**
Run the following command in the terminal:

```bash
certstrap request-cert --common-name "Developer ID: $(whoami)" --curve "P-384"
```

The CSR will be saved to `out/SoramitsuKhmer_ECC_Developer_ID_$(whoami).csr`. Please send this file to the Soramitsu Khmer Certification Authority for signing.
