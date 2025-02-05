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

### Example

```sh
$ certigo connect example.com -v

# ** TLS Connection **
# Version: TLS 1.3
# Cipher Suite: AES_128_GCM_SHA256 cipher

# ** CERTIFICATE 1 **
# Serial: 82126535221637994499216007114345604740
# Valid: 2025-02-05 03:33 UTC to 2027-02-05 03:40 UTC
# Signature: ECDSA-SHA384
# Subject Info:
#         CommonName: example.com
# Issuer Info:
#         CommonName: Developer ID: socheat
# Subject Key ID: 16:69:D2:4A:FB:68:4A:44:10:1F:DD:82:53:32:DF:FA:6D:B7:C5:C1
# Authority Key ID: 08:2E:C6:7E:A3:CC:54:06:17:E0:5F:BC:E8:A6:CD:E2:74:3C:A2:83
# Key Usage:
#         Digital Signature
#         Key Encipherment
#         Data Encipherment
#         Key Agreement
# Extended Key Usage:
#         Server Auth
#         Client Auth
# DNS Names:
#         example.com

# ** CERTIFICATE 2 **
# Serial: 255929090294309643125069244528596166792
# Valid: 2025-02-05 03:30 UTC to 2027-02-05 03:40 UTC
# Signature: ECDSA-SHA384
# Subject Info:
#         CommonName: Developer ID: socheat
# Issuer Info:
#         Country: KH
#         Organization: Soramitsu Khmer
#         Organizational Unit: Soramitsu Khmer Certification Authority
#         CommonName: SoramitsuKhmer ECC Developer ID Certification Authority
# Subject Key ID: 08:2E:C6:7E:A3:CC:54:06:17:E0:5F:BC:E8:A6:CD:E2:74:3C:A2:83
# Authority Key ID: 32:27:F6:DE:29:DA:94:4A:A3:9C:36:40:18:6C:7F:4C:D0:5D:08:8C
# Basic Constraints: CA:true, pathlen:0
# Key Usage:
#         Cert Sign
#         CRL Sign

# Found 1 valid certificate chain(s):
# [0] CN=example.com
#         => CN=Developer ID: socheat
#         => CN=SoramitsuKhmer ECC Developer ID Certification Authority
#         => CN=SoramitsuKhmer ECC Root CA [self-signed]
```
