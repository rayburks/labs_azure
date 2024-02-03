
Referenz:
https://www.golinuxcloud.com/openssl-view-certificate/#:~:text=Here%20server.crt%20is%20our%20final%20signed%20certificate%20bash,bash%20~%5D%23%20openssl%20x509%20-noout%20-text%20-in%20%3CCERTIFICATE%3E

# Show Content of Private Key

```bash
openssl rsa -noout -text -in <PRIVATEKEY_FILE>
```

# View the content of CSR (Certificate Signing Request)

PEM-Format
```bash
openssl req -noout -text -in <CSR_FILE>
```
# View the content of CA certificate

PEM-Format
```bash
openssl x509 -noout -text -in <CA_CERTIFICATE>
```

