# EX-NO-9-RSA-Algorithm

## AIM:
To Implement RSA Encryption Algorithm in Cryptography

## Algorithm:


Step 1: Design of RSA Algorithm  
The RSA algorithm is based on the mathematical difficulty of factoring the product of two large prime numbers. It involves generating a public and private key pair, where the public key is used for encryption, and the private key is used for decryption.

Step 2: Implementation in Python or C 
This algorithm can be implemented in languages like Python or C by performing large integer calculations for key generation, encryption, and decryption, utilizing libraries for modular arithmetic if necessary.

Step 3: Algorithm Description  
1. Key Generation:
   - Select two large prime numbers \( p \) and \( q \).
   - Calculate \( n = p \times q \), which will be used as the modulus.
   - Compute the totient \( \phi(n) = (p - 1)(q - 1) \).
   - Choose a public exponent \( e \) such that \( e \) is coprime with \( \phi(n) \).
   - Compute the private key \( d \), which is the modular inverse of \( e \) mod \( \phi(n) \).

2. Encryption:
   - Convert the plaintext message \( M \) into a numerical form \( m \) (such that \( 0 \le m < n \)).
   - Compute the ciphertext \( c \) using the formula: \( c = m^e \mod n \).

3. Decryption:
   - Use the private key \( d \) to recover \( m \) from \( c \) using: \( m = c^d \mod n \).
   - Convert \( m \) back into the original message \( M \).

Step 4: Mathematical Representation  
- Encryption: \( E(m) = m^e \mod n \)
- Decryption: \( D(c) = c^d \mod n \)

Step 5: **Security Foundation  
The security of RSA relies on the difficulty of factoring large numbers; thus, choosing sufficiently large prime numbers for \( p \) and \( q \) is crucial for security.

## Program:
```
#include <stdio.h>

// GCD function
int gcd(int a, int b)
{
    while (b != 0)
    {
        int t = b;
        b = a % b;
        a = t;
    }
    return a;
}

// Modular exponentiation
int mod_exp(int base, int exp, int mod)
{
    int result = 1;
    while (exp > 0)
    {
        result = (result * base) % mod;
        exp--;
    }
    return result;
}

// Modular inverse
int mod_inverse(int e, int phi)
{
    for (int d = 1; d < phi; d++)
    {
        if ((e * d) % phi == 1)
            return d;
    }
    return -1;
}

int main()
{
    int p, q, n, phi, e, d;
    int message, encrypted_message, decrypted_message;

    printf("Enter a prime number (p): ");
    scanf("%d", &p);

    printf("Enter another prime number (q): ");
    scanf("%d", &q);

    n = p * q;
    phi = (p - 1) * (q - 1);

    do
    {
        printf("Enter a value for public key exponent (e) such that 1 < e < %d: ", phi);
        scanf("%d", &e);
    } while (gcd(e, phi) != 1);

    d = mod_inverse(e, phi);

    printf("Public key: (n = %d, e = %d)\n", n, e);
    printf("Private key: (n = %d, d = %d)\n", n, d);

    printf("Enter the message to encrypt (as an integer): ");
    scanf("%d", &message);

    encrypted_message = mod_exp(message, e, n);
    printf("Encrypted message: %d\n", encrypted_message);

    decrypted_message = mod_exp(encrypted_message, d, n);
    printf("Decrypted message: %d\n", decrypted_message);

    return 0;
}

```

## Output:

<img width="940" height="493" alt="image" src="https://github.com/user-attachments/assets/ed152b38-7afa-4402-8eac-93cda4a64475" />




## Result:
 The program is executed successfully.
