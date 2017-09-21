# RSA keys

## What is PKCS?
PCKS Stands for Public Key Cryptography Standards. These are standards for defining information such as Algorithms, Keys and Certificate - usually in the format of .pem files.

### PKCS 1 vs PKCS 8
PKCS 1 contain the RSA Key Information whereas the PKCS 8 will also define the version and the algorithm identifier. These are typically exchanged in base64 encoded format. PKCS 8 will have the header and footer that says -----BEGIN PRIVATE KEY----- and -----END PRIVATE KEY----- respectively (or BEGIN/END **ENCRYPTED** PRIVATE KEY, in the case of passphrase protected key). without the word RSA in them.
