# AWS KMS - Key Management Service

## Encryption and Decryption using the Master Key
You can get KMS to Encrypt or Decrypt a data using a Master Key that reside in KMS. Even we don't get to access the contents of the key directly.

### Encryption using the AWS CLI
`aws kms encrypt --key-id {key-id} --plaintext "ABC" --output text --query CiphertextBlob | base64 --decode > ExampleCiphertextFile`

The ExampleCiphertextFile will contain the binary data that is encrypted using the Master Key associated for the Key ID

### Decryption using the AWS CLI
`aws kms decrypt --ciphertext-blob fileb://{filepath} --output text --query Plaintext | base64 --decode > ExamplePlaintextFile`

The ExamplePlaintextFile should contain "ABC".
