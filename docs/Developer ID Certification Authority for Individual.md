# Generate "Developer ID Certification Authority" for Individual


**Create a new certificate signing request (CSR) for the Developer ID Certification Authority for Individual.**
Run the following command in the terminal:

```bash
# Create a ~/PKI directory to store the CSR
mkdir -p ~/PKI

# Change the current directory to the PKI directory
cd ~/PKI

# Create a new certificate signing request (CSR) for the Developer ID Certification Authority for Individual
certstrap request-cert --common-name "Developer ID: $(whoami)" --curve "P-384"
```

The CSR will be saved to `out/Developer_ID_$(whoami).csr`. Please send this file to the Soramitsu Khmer Certification Authority for signing.

Once you receive the signed certificate, please import it into `~/PKI/out`. Please make sure the certificate is named `Developer_ID_$(whoami).crt`.

### Request certificate signing using your signed Intermediate Certificate

```bash
# Request certificate signing for your domain
certstrap request-cert --common-name "example.com" --domain example.com --curve "P-384"

# Sign the certificate using the Developer ID Certification Authority for Individual
certstrap sign example.com --CA "Developer ID: $(whoami)"
```
