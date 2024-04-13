 ## IMPLEMENTATION OF RSA
 # AIM :
 To write a C program to implement the RSA encryption algorithm.

## ALGORITHM:
STEP-1: Select two co-prime numbers as p and q.

STEP-2: Compute n as the product of p and q.

STEP-3: Compute (p-1)*(q-1) and store it in z.

STEP-4: Select a random prime number e that is less than that of z.

STEP-5: Compute the private key, d as e *
mod-1
(z).

STEP-6: The cipher text is computed as messagee *

STEP-7: Decryption is done as cipherdmod n.

## PROGRAM:
```
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
// Function to calculate greatest common divisor (GCD)
int gcd(int a, int b) {
if (b == 0)
return a;
return gcd(b, a % b);
}
// Function to generate RSA keys
void generateRSAKeys(int *n, int *e, int *d) {
// Choose two prime numbers (p and q)
int p;
int q;
printf("enter two prime numbers:");
scanf("%d %d",&p,&q);
// Calculate n = p * q
*n = p * q;
// Calculate Euler's totient function (φ(n))
int phi = (p - 1) * (q - 1);
// Choose a public exponent (e) such that 1 < e < φ(n) and gcd(e, φ(n)) = 1
*e = 5; // You can choose a different value for e, typically a prime number
// Calculate the private exponent (d) such that (d * e) % φ(n) = 1
*d = 0;
while ((*d * *e) % phi != 1) {
(*d)++;
}
}
// Function to perform modular exponentiation (base^exponent % modulus)
int modExp(int base, int exponent, int modulus) {
int result = 1;
while (exponent > 0) {
if (exponent % 2 == 1) {
result = (result * base) % modulus;
}
base = (base * base) % modulus;
exponent /= 2;
}
return result;
}
// Function to encrypt a message using the public key
int encrypt(int message, int publicKey, int modulus) {
return modExp(message, publicKey, modulus);
}
// Function to decrypt a message using the private key
int decrypt(int ciphertext, int privateKey, int modulus) {
return modExp(ciphertext, privateKey, modulus);
}
int main() {
int n, e, d;
int plaintext;
printf("enter plaintext:");
scanf("%d",&plaintext);
generateRSAKeys(&n, &e, &d);
printf("Original message: %d\n", plaintext);
int ciphertext = encrypt(plaintext, e, n);
printf("Encrypted message: %d\n", ciphertext);
int decryptedMessage = decrypt(ciphertext, d, n);
printf("Decrypted message: %d\n", decryptedMessage);
return 0;
}
```
## OUTPUT:
![Screenshot 2024-04-13 082053](https://github.com/surrey-78/19CS412---CRYPTOGRAPHY---ADVANCED-ENCRYPTION/assets/119559366/e4e95c75-c52a-4cbf-9704-e749b773ad91)



## RESULT :

Thus the C program to implement RSA encryption technique had been
implemented successfully

## IMPLEMENTATION OF AES
## AIM:
To use Advanced Encryption Standard (AES) Algorithm for a practical
application like URL Encryption.
## ALGORITHM:
1. AES is based on a design principle known as a substitution–permutation.
2. AES does not use a Feistel network like DES, it uses variant of Rijndael.
3. It has a fixed block size of 128 bits, and a key size of 128, 192, or 256 bits.
4. AES operates on a 4 × 4 column-major order array of bytes, termed the state
## PROGRAM:
## AES.java
```
import java.io.UnsupportedEncodingException;
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;
import java.util.Arrays;
import java.util.Base64;
import javax.crypto.Cipher;
import javax.crypto.spec.SecretKeySpec;
public class AES {
 private static SecretKeySpec secretKey;
 private static byte[] key;
 public static void setKey(String myKey) {
 MessageDigest sha = null;
 try {
 key = myKey.getBytes("UTF-8");
 sha = MessageDigest.getInstance("SHA-1");
 key = sha.digest(key);
 key = Arrays.copyOf(key, 16);
 secretKey = new SecretKeySpec(key, "AES");
 } catch (NoSuchAlgorithmException e) {
 e.printStackTrace();
 } catch (UnsupportedEncodingException e) {
 e.printStackTrace();
 }
 }
 public static String encrypt(String strToEncrypt, String secret) {
 try {
 setKey(secret);
 Cipher cipher = Cipher.getInstance("AES/ECB/PKCS5Padding");
 cipher.init(Cipher.ENCRYPT_MODE, secretKey);
 return
Base64.getEncoder().encodeToString(cipher.doFinal(strToEncrypt.getBytes("UTF-8")));
 } catch (Exception e) {
 System.out.println("Error while encrypting: " + e.toString());
 }
 return null;
 }
 public static String decrypt(String strToDecrypt, String secret) {
 try {
 setKey(secret);
 Cipher cipher = Cipher.getInstance("AES/ECB/PKCS5PADDING");
 cipher.init(Cipher.DECRYPT_MODE, secretKey);
 return new String(cipher.doFinal(Base64.getDecoder().decode(strToDecrypt)));
 } catch (Exception e) {
 System.out.println("Error while decrypting: " + e.toString());
 }
 return null;
 }
 public static void main(String[] args) {
 final String secretKey = "annaUniversity";
 String originalString = "www.annauniv.edu";
 String encryptedString = AES.encrypt(originalString, secretKey);
 String decryptedString = AES.decrypt(encryptedString, secretKey);
 System.out.println("URL Encryption Using AES Algorithm\n------------");
 System.out.println("Original URL : " + originalString);
 System.out.println("Encrypted URL : " + encryptedString);
 System.out.println("Decrypted URL : " + decryptedString);
 }
}
```
   ## OUTPUT:
![Screenshot 2024-04-13 082435](https://github.com/surrey-78/19CS412---CRYPTOGRAPHY---ADVANCED-ENCRYPTION/assets/119559366/4ac9756e-eb74-4bdb-aa7f-9fd96409713a)


## RESULT:
Thus the Java program to implement AES encryption technique had been implemented successfully


## IMPLEMENTATION OF DIFFIE HELLMAN KEY EXCHANGE ALGORITHM

## AIM:

To implement the Diffie-Hellman Key Exchange algorithm using C language.


## ALGORITHM:

STEP-1: Both Alice and Bob shares the same public keys g and p.

STEP-2: Alice selects a random public key a.

STEP-3: Alice computes his secret key A as g
a mod p.

STEP-4: Then Alice sends A to Bob.


STEP-5: Similarly Bob also selects a public key b and computes his secret
key as B and sends the same back to Alice.


STEP-6: Now both of them compute their common secret key as the other
one’s secret key power of a mod p.

## PROGRAM: 

```
#include <math.h>
#include <stdio.h>
// Power function to return value of a ^ b mod P
long long int power(long long int a, long long int b,
long long int P)
{
if (b == 1)
return a;
else
return (((long long int)pow(a, b)) % P);
}
int main()
{
long long int P, G, x, a, y, b, ka, kb;
// Both the persons will be agreed upon the
// public keys G and P
printf("Enter the value of P:");
scanf("%lld",&P); // A prime number P is taken
printf("The value of P : %lld\n", P);
printf("Enter the value of G:");
scanf("%lld",&G); // A primitive root for P, G is taken
printf("The value of G : %lld\n\n", G);
// Alice will choose the private key a
a = 4; // a is the chosen private key
printf("The private key a for Alice : %lld\n", a);
x = power(G, a, P); // gets the generated key
// Bob will choose the private key b
b = 3; // b is the chosen private key
printf("The private key b for Bob : %lld\n\n", b);
y = power(G, b, P); // gets the generated key
// Generating the secret key after the exchange
// of keys
ka = power(y, a, P); // Secret key for Alice
kb = power(x, b, P); // Secret key for Bob
printf("Secret key for the Alice is : %lld\n", ka);
printf("Secret Key for the Bob is : %lld\n", kb);
return 0;
}
```
## OUTPUT:
![Screenshot 2024-04-13 082816](https://github.com/surrey-78/19CS412---CRYPTOGRAPHY---ADVANCED-ENCRYPTION/assets/119559366/a6f5e2ad-69db-4726-aec2-0f2d6d1fc8e6)



## RESULT: 

Thus the Diffie-Hellman key exchange algorithm had been successfully
implemented using C.





## IMPLEMENTATION OF DES ALGORITHM

## AIM:
To write a program to implement Data Encryption Standard (DES)

## ALGORITHM :

STEP-1: Read the 64-bit plain text.

STEP-2: Split it into two 32-bit blocks and store it in two different arrays.

STEP-3: Perform XOR operation between these two arrays.

STEP-4: The output obtained is stored as the second 32-bit sequence and the
original second 32-bit sequence forms the first part.

STEP-5: Thus the encrypted 64-bit cipher text is obtained in this way. Repeat the
same process for the remaining plain text characters.

### PROGRAM :

```
from cryptography.fernet import Fernet
message = input()
key = Fernet.generate_key()
fernet = Fernet(key)
encMessage = fernet.encrypt(message.encode())
print("original string: ", message)
print("encrypted string: ", encMessage)

decMessage = fernet.decrypt(encMessage).decode()
 
print("decrypted string: ", decMessage)
```
## OUTPUT:
![2024-04-13 at 08 36 14_d4acb556](https://github.com/surrey-78/19CS412---CRYPTOGRAPHY---ADVANCED-ENCRYPTION/assets/119559366/287863cb-9d30-4aec-969b-5e183682a499)

## RESULT:

Thus the data encryption standard algorithm had been implemented
successfully.

