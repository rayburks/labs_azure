
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

# Creating the root CA

## Variables

common_name="Azure_IoT_Hub_CA_Cert_Test_Only"

ALGORITHM=genrsa
password_cmd=-aes256 -passout pass:${ROOT_CA_PASSWORD}

RSA_CA_KEY_BITS_LENGTH="4096"
OPENSSL_CONFIG_FILE="${CERTIFICATE_DIR}/openssl_root_ca.cnf"

ROOT_CA_PREFIX="azure-iot-test-only.root.ca"
key_file=${CERTIFICATE_DIR}/private/${ROOT_CA_PREFIX}.key.pem
cert_file=${CERTIFICATE_DIR}/certs/${ROOT_CA_PREFIX}.cert.pem

## Create root CA private key

```
openssl ${ALGORITHM} \
        ${password_cmd} \
        -out ${key_file} \
        ${RSA_CA_KEY_BITS_LENGTH}
```

## Creating the root CA certificate

```
openssl req \
        -new \
        -x509 \
        -config ${OPENSSL_CONFIG_FILE} \
        ${password_cmd} \
        -key ${key_file} \
        -subj "/CN=${common_name}" \
        -days ${DEFAULT_VALIDITY_DAYS} \
        -sha256 \
        -extensions "v3_ca" \
        -out ${cert_file}
```

# Create intermediate Certificate

root_ca_password="${ROOT_CA_PASSWORD}"
common_name="Azure_IoT_Hub_Intermediate_Cert_Test_Only"

extension="${1}"
expiration_days="${2}"
common_name="${3}"
prefix="${4}"
issuer_prefix="${5}"
key_pass="${6}"
issuer_key_pass="${7}"

subject="/CN=${common_name}"
key_file="${CERTIFICATE_DIR}/private/${prefix}.key.pem"

cert_file="${CERTIFICATE_DIR}/certs/${prefix}.cert.pem"
cert_pfx_file="${CERTIFICATE_DIR}/certs/${prefix}.cert.pfx"
cert_full_chain_file="${CERTIFICATE_DIR}/certs/${prefix}-full-chain.cert.pem"

csr_file="${CERTIFICATE_DIR}/csr/${prefix}.csr.pem"

issuer_key_file="${CERTIFICATE_DIR}/private/${issuer_prefix}.key.pem"
issuer_cert_file="${CERTIFICATE_DIR}/certs/${issuer_prefix}.cert.pem"
issuer_cert_full_chain_file="${CERTIFICATE_DIR}/certs/${issuer_prefix}-full-chain.cert.pem"
root_ca_cert_file="${CERTIFICATE_DIR}/certs/${ROOT_CA_PREFIX}.cert.pem"

## Private Key for intermediate Certificate
```
openssl ${ALGORITHM} \
        ${password_cmd} \
        -out ${key_file} \
        ${key_bits_length}
```

## CSR for intermediate Certificate

```
openssl req -new -sha256 ${password_cmd} \
        -config ${OPENSSL_CONFIG_FILE} \
        -key ${key_file} \
        -subj "${subject}" \
        -out ${csr_file}
```

## Sign CSR and create intermediate Certificate

```
openssl ca -batch -config ${OPENSSL_CONFIG_FILE} \
            -extensions ${extension} \
            -days ${expiration_days} -notext -md sha256 \
            -cert ${issuer_cert_file} \
            -keyfile ${issuer_key_file} -keyform PEM \
            ${issuer_key_passwd_command} \
            -in ${csr_file} \
            -out ${cert_file} \
            -outdir ${CERTIFICATE_DIR}/newcerts
```
