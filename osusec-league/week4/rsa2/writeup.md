# RSA-2

## Summary
This challenge relies on the public key e being small and our plaintext P being short. In particular if P < N^(1/e), then we know that P^e < N. If this is case, it is trivial to break the encryption.

## Accessing Challenge
You start this challenge by decrypting the tar archive using the the flag from RSA-1. The command to run: 
```bash
openssl enc -d -aes-256-ctr -pbkdf2 -nosalt -p -in rsa2.tar.gz.enc -out rsa2.tar.gz
```
Input the flag from RSA-1 as the key. We can now open the tar archive and proceed with the challenge.

## Decrypting
Since the public key e and the plaintext P satisfy the conditions laid out in the summary, we can trivially find P by simply taking the ciphertext C and finding C^(1/e). This gives us the plaintext. We can then get the flag from this plaintext in the same way we got it from RSA-1, just skip the padding portion since we observe that padding is not present in the plaintext from puzzle.py.

The resulting string is the flag.
