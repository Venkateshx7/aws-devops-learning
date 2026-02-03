[ExampleSecretFile.txt](https://github.com/user-attachments/files/24614053/ExampleSecretFile.txt)
AWS-KMS[kms-demo-cli.sh](https://github.com/user-attachments/files/24614061/kms-demo-cli.sh)
# 1) encryption
aws kms encrypt --key-id alias/AWS-KMS-key --plaintext fileb://ExampleSecretFile.txt --output text --query CiphertextBlob  --region ap-south-1 > ExampleSecretFileEncrypted.base64

# base64 decode for Linux or Mac OS 
cat ExampleSecretFileEncrypted.base64 | base64 --decode > ExampleSecretFileEncrypted

# base64 decode for Windows
certutil -decode .\ExampleSecretFileEncrypted.base64 .\ExampleSecretFileEncrypted

<img width="1853" height="917" alt="Screenshot 2026-01-14 124806" src="https://github.com/user-attachments/assets/35c709d8-8fe7-406c-8f38-c5fbfb4d8316" />

# 2) decryption

aws kms decrypt --ciphertext-blob fileb://ExampleSecretFileEncrypted   --output text --query Plaintext > ExampleFileDecrypted.base64  --region ap-south-1

# base64 decode for Linux or Mac OS 
cat ExampleFileDecrypted.base64 | base64 --decode > ExampleFileDecrypted.txt


# base64 decode for Windows
certutil -decode .\ExampleFileDecrypted.base64 .\ExampleFileDecrypted.txt
