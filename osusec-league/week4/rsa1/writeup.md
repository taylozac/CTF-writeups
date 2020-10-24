# RSA-1

## Summary
This challenge teaches you how to generate an RSA private key d given primes p and q, the factors of the modulus N. It then requires you to use this generated key to decrypt the known ciphertext C.

## Brief Explanation of RSA
RSA is an asymmetric encryption scheme. This means that there are two keys that are used, one public key e and one private key d. The public key is selected and the private key d is chosen such that ed ≡ 1 (mod phi(N)) where phi() is Euler's Totient function. The public key is published (along with the modulus N) and the private key is then kept secret. These keys give us the following properties:
- C = P^e (mod N)
- P = C^d (mod N) 

Generally, it is computationally infeasible to compute d as p and q are unknown. This makes the computation of phi(N). However, if p and q are known, we can trivially solve phi(N) as phi(N) = phi(pq) = phi(p)phi(q) = (p-1)(q-1). It is easy show the the values of each phi(p) and phi(q) since they are each prime meaning all positive integers below them are relatively prime (a number x is relatively prime with a number y if and only if gcd(x,y) = 1). Since Euler's totient function returns a count of these relatively prime numbers, phi(p) = p-1 and phi(q) = q-1. Now that we know that phi(N) = (p-1)(q-1), we can compute d.

## Generating Private Key d
At this point, the private key d is computed by simply finding the modular inverse of e (mod phi(N)). I did this using the Extended Euclidean Algorithm. Plenty of implementations of this can be found online.

## Decrypting
Now that we have d, we can use the properties from the explanation to compute the plaintext, P = C^d (mod N). Now that we have the plaintext, we simply need to reverse the few other operations performed on the plaintext before encryption. The operations done to the plaintext P (in order as done in puzzle.py) are as follows:
- Encode with UTF-8.
- Pad flag of length 37 to length of 250 bytes (adds 217 bytes to end).
- Convert bytes to long.

We just need do these in the reverse order of what puzzle.py did. So we do:
- Convert C^d (mod N) from long to bytes.
- Take the first 37 bytes of byte array.
- Decode with UTF-8.

The resulting string is the flag.
