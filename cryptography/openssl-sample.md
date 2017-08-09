openssl version -a

openssl genrsa -aes128 -out fd.key 2048
Generage 2048 bit RSA key pairs, and encrypted with AES-128, output file name is fd.key

openssl rsa -text -in fd.key

openssl rsa -in fd.key -pubout -out fd-public.key

openssl dsaparam -genkey 2048 | openssl dsa -out dsa.key -aes128

openssl ecparam -genkey -name secp256r1 | openssl ec -out ec.key -aes128

openssl req -new -key fd.key -out fd.csr

openssl req -text -in fd.csr -noout

openssl x509 -x509toreq -in fd.crt -out fd.csr -signkey fd.key
update a certificate signing request(CSR) with an already exist certificate and a new key

openssl x509 -req -days 365 -in fd.csr -signkey fd.key -out fd.crt

openssl req -new -x509 -days 365 -key fd.key -out fd.crt
