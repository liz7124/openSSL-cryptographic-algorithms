# openSSL-cryptographic-algorithms
Tutorial for using OpenSSL Digital Signature and Hash Functions

## Create Message
1. Open your command prompt
2. Type ```echo dataencrypt > message.txt```. "dataencrypt" is the message you want to process and will be stored in a file with the name "message.txt".

## Generate Private/Secret Key and Public Key
### Generate RSA privatekey
1. Run ```openssl genpkey -algorithm RSA -out privatekey.pem -pkeyopt rsa_keygen_bits:1024``` from your command prompt.

### Generate RSA publickey
1. Run ```openssl rsa -pubout -in privatekey.pem -out publickey.pem``` from your command prompt.

## Digital Signature
### Sign
1. Run ```openssl dgst -sha256 -sign privatekey.pem -out signature.bin message.txt``` from your command prompt.

### Verify Signature
1. Run ```openssl dgst -sha256 -verify publickey.pem -signature signature.bin message.txt``` from your command prompt.

## Cryptographic Hash Functions
In blockchain, we typically use SHA-2 and SHA-3 family. For example, **SHA-256** or **KECCAK-256** algorithm.

### Generate Hash file with SHA256
1. Run ```openssl dgst -sha256 message.txt > message-hash.txt``` from your command prompt.

### Verify Hash file
1. Run ```certutil -hashfile message.txt sha256``` from your command prompt.


### References
https://techdocs.akamai.com/download-ctr/docs/verify-checksum
https://medium.com/@bn121rajesh/rsa-sign-and-verify-using-openssl-behind-the-scene-bf3cac0aade2
https://www.openssl.org/docs/man3.1/man1/openssl-dgst.html
https://opensource.com/article/19/6/cryptography-basics-openssl-part-2
