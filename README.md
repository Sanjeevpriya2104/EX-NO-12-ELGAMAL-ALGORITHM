# EX-NO-12-ELGAMAL-ALGORITHM

## AIM:
To Implement ELGAMAL ALGORITHM

## ALGORITHM:

1. ElGamal Algorithm is a public-key cryptosystem based on the Diffie-Hellman key exchange and relies on the difficulty of solving the discrete logarithm problem.

2. Initialization:
   - Select a large prime \( p \) and a primitive root \( g \) modulo \( p \) (these are public values).
   - The receiver chooses a private key \( x \) (a random integer), and computes the corresponding public key \( y = g^x \mod p \).

3. Key Generation:
   - The public key is \( (p, g, y) \), and the private key is \( x \).

4. Encryption:
   - The sender picks a random integer \( k \), computes \( c_1 = g^k \mod p \), and \( c_2 = m \times y^k \mod p \), where \( m \) is the message.
   - The ciphertext is the pair \( (c_1, c_2) \).

5. Decryption:
   - The receiver computes \( s = c_1^x \mod p \), and then calculates the plaintext message \( m = c_2 \times s^{-1} \mod p \), where \( s^{-1} \) is the modular inverse of \( s \).

6. Security: The security of the ElGamal algorithm relies on the difficulty of solving the discrete logarithm problem in a large prime field, making it secure for encryption.

## Program:
```
#include <stdio.h>

long long modexp(long long base, long long exp, long long mod)
{
    long long result = 1;
    base %= mod;

    while (exp > 0)
    {
        if (exp % 2 == 1)
            result = (result * base) % mod;

        base = (base * base) % mod;
        exp /= 2;
    }
    return result;
}

long long modInverse(long long a, long long m)
{
    long long m0 = m, t, q;
    long long x0 = 0, x1 = 1;

    while (a > 1)
    {
        q = a / m;
        t = m;
        m = a % m;
        a = t;
        t = x0;
        x0 = x1 - q * x0;
        x1 = t;
    }

    if (x1 < 0)
        x1 += m0;

    return x1;
}

int main()
{
    long long p, g, bob_private_key, message, k;

    printf("Enter a prime number (p): ");
    scanf("%lld", &p);

    printf("Enter a primitive root modulo p (g): ");
    scanf("%lld", &g);

    printf("Prathyus's private key (x): ");
    scanf("%lld", &bob_private_key);

    long long bob_public_key = modexp(g, bob_private_key, p);
    printf("sanju's public key (y): %lld\n", bob_public_key);

    printf("sanjeevpriya, enter the message (M) you want to send: ");
    scanf("%lld", &message);

    printf("sanjeevpriya's private key (k): ");
    scanf("%lld", &k);

    long long c1 = modexp(g, k, p);
    long long yk = modexp(bob_public_key, k, p);
    long long c2 = (message * yk) % p;

    printf("sanjeevpriya sends encrypted message (c1, c2): (%lld, %lld)\n", c1, c2);

    long long s = modexp(c1, bob_private_key, p);
    long long s_inv = modInverse(s, p);

    long long decrypted_message = (c2 * s_inv) % p;

    printf("sanju decrypts the message: %lld\n", decrypted_message);

    return 0;
}
```

## Output:
<img width="1743" height="879" alt="image" src="https://github.com/user-attachments/assets/b7410a8f-db92-499b-9482-1aae132ee946" />


## Result:
The program is executed successfully.
