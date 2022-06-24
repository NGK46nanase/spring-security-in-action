# Generate a self-signed certificate using a tool like OpenSSL

```
openssl req -newkey rsa:2048 -x509 -keyout key.pem -out cert.pem -days 365
```
The commpand outputs two files : key.pem (the private key) and cert.pem (a public certificate). We'll use
these files further to generate our self-signed certificate for enabling HTTPS.

```
openssl pkcs12 -export -in cert.pem -inkey key.pem -out certificate.p12 -name "certificate"
```

Mind that if you run these commands in a Bash shell on a Windows system, you might need to add *winpty* before it. 

Finally, having the self-signed certificate, you can configure HTTPS for your endpoints. Copy the certificate.p12 file into the 
resources folder of the Spring Boot project and add the following lines to your *application.properties* file:

```
server.ssl.key-store-type=PKCS12
server.ssl.key-store=classpath:certificate.p12
server.ssl.key-store-password=12345
```
The value of the password is the one you specified when running the second command to generate the PKCS12 certificate file.

