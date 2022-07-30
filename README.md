### How to create & sign SSL/TLS certificates with openssl - 

Learning with TECH SCHOOL. Thanks!

```sh
rm *.pem
```

### 1. Generate CA's private key and self-signed certificate
```sh
openssl req -x509 -newkey rsa:4096 -days 365 -nodes -keyout ca-key.pem -out ca-cert.pem -subj "/C=AR/ST=Corrientes/L=Corrientes/O=DivCor/OU=Services/emailAddress=machucajuangabriel@gmail.com"

echo "CA's self-signed certificate"
openssl x509 -in ca-cert.pem -noout -text
```
### 2. Generate web server's private key and certificate signing request (CSR)
```sh
openssl req -newkey rsa:4096 -nodes -keyout server-key.pem -out server-req.pem -subj "/C=AR/ST=Corrientes/L=Corrientes/O=DivCor/OU=Services/emailAddress=divcor.soporte@gmail.com"
```

### 3. Use CA's private key to sign web server's CSR and get back the signed certificate
```sh
openssl x509 -req -in server-req.pem -days 60 -CA ca-cert.pem -CAkey ca-key.pem -CAcreateserial -out server-cert.pem -extfile server-ext.cnf


echo "Server's self-signed certificate"
openssl x509 -in ca-cert.pem -noout -text
```

### 4. Verify if certificate is valid or not 
```sh
openssl verify -CAfile ca-cert.pem server-cert.pem
```