# openSSL-cryptographic-algorithms
Tutorial for using OpenSSL Digital Signature and Hash Functions

## Create Message
1. Open your command prompt
2. Type ```echo dataencrypt > message.txt```. "dataencrypt" is the message you want to process and will be stored in a file with the name "message.txt".
   You can change "dataencrypt" to any message you want.

## Generate Private/Secret Key and Public Key
### Generate RSA privatekey
1. Run ```openssl genpkey -algorithm RSA -out privatekey.pem -pkeyopt rsa_keygen_bits:1024``` from your command prompt.
   RSA is the digital signature algorithm that we want to use. ```privatekey.pem``` is the output filename to store the RSA private key. 1024 is the length of the private key in bits.

### Generate RSA publickey
1. Run ```openssl rsa -pubout -in privatekey.pem -out publickey.pem``` from your command prompt.
   ```privatekey.pem``` is the private key file that required to generate RSA public key. ```publickey.pem``` is the output filename to store RSA public key.

## Digital Signature
### Sign
1. Run ```openssl dgst -sha256 -sign privatekey.pem -out signature.bin message.txt``` from your command prompt.
```-sha256``` is the type of hash function that we want to use.
   ```-sign``` is the digital signature Signing function with the input of the RSA private key stored in the file ```privatekey.pem``` and the message to be signed in the file ```message.txt```. The output is the digital signature that is saved in the filename ```signature.bin```.

### Verify Signature
1. Run ```openssl dgst -sha256 -verify publickey.pem -signature signature.bin message.txt``` from your command prompt.
   ```-verify``` is the digital signature Verify function with the input of RSA public key stored in the file ```publickey.pem```, the message to be verified in the file ```message.txt```, and the digital signature in the file ```signature.bin```.
   The output of this function, if the verification is successful, will return ```Verified OK```. If failed, it will return ```Verification Failure```.

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
