# puppet ssl

[INDEX](../../README.md)

## Overview:
Manage SSL keys and certificates to communicate with your puppet infra.

## Examples

```bash
# Generate a certificate signing request (CSR) and submit it to the CA
$ puppet ssl submit_request

# Download a certificate for this host
$ puppet ssl download_cert

# Verify if certicates are present and match
$ puppet ssl verify

# Remove private key and certificates related files
$ puppet ssl clean
```