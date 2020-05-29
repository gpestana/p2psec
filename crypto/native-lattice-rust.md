---
title: Native Lattice Crypto in Rust
description: research notes pm implementing a native lattice crypto crate in Rust.
tags: crypto, rust
---

# Native Lattice Crypto in Rust

**Scope**: research and specs for implementing a native lattice crypto crate in Rust.

**Why?**
- Lattice-based cryto schemes are (so far) post-quantum
- Size of asymmetric keys are small compared to RSA and elliptic curve-based schemes;
- Encryption/decryption times are faster than RSA and ECDH assumptions;
- There are practical fully homomorphic schemes based on lattice crypto; 
- No native implementation of lattice-based crypto schemes in Rust;

- [ ] Check [lattigo](https://github.com/ldsec/lattigo) golang package.
- [ ] Spec traits and logic for key generation 
- [ ] Spec traits and logic for encryption/decryption of BFV;
- [ ] Spec traits and plans for implementing a signature protocol using lattice crypto;
- [ ] Spec traits and plans for implementing homomorphic encryption scheme (e.g. BFV) using LWE/lattice crypto;
- [ ] Document all along the way;


## Research notes of lattigo

- [lattigo](https://github.com/ldsec/lattigo) golang package;

`params` for bfv includes:
- `T`
- `LogModuli` stores the NTT primes of the RNS representation
    - `LogQi` Ciphertext prime moduli
    - `LogPi` Keys additional prime moduli
    - `LogQiMul` Ciphertext secondary prime moduli
- `Sigma`

In lattice crypto, NTT -- Number Theory Transform -- boosts computation times, specially on key generation and encryption/decryption.

### lattigo.BFV

A [polynomial](https://github.com/ldsec/lattigo/blob/bb095f1d82cd5c532171b138cd0ad83ecd785103/ring/ring_object.go#L11) is represented in the  (Chinese Remainer Theorem) form, as a matrix of `uint64`. Each entry in the matrix represents a polynomial coefficient. 

1. **Secret generation Key**

A secret key is a large polynomial (`*ring.Poly`) with a given distribution. The package generates the polynomial using NTT and representing it in the Montgomery form, more specifically as a "montgomery matrix ternary". The default distribution for the ternary matrix is `1/3`.

```
sk = [[a_0, ..., a_n], [b_0, ..., b_n], [c_0, ..., c_n]]

// where [X_0, ..., X_n] is a vector representing the polynomial coefficients in the Montgomery form
```

A secret key with 0 values is generated in the follwoing way:

```
func NewSecretKey(params *Parameters) *SecretKey {
    //...
    sk.sk = ring.NewPoly(uint64(1<<params.LogN), uint64(len(params.LogQi)+len(params.LogPi)))
}
```

Which shows that the secret key is a polynomial in the Montgomery form, represented by a matrix of vectors. The size of the matrix is defined by the `nbModuli` (more specifically, by `2^LogN = N`) of the initialization parameters, while the size of the coefficient vector is defined by `N` (more specifically by `|logQui| + |logPi|`), of the initialization params.

2. **Public generation Key**

A public key is represented by two ring polynomials (`[2]*ring.Poly`). 


3. CRT - Chinese Remaider Theorem

[Coursera - CRT Concepts, Integer-to-CRT Conversions
](https://www.coursera.org/lecture/mathematical-foundations-cryptography/crt-concepts-integer-to-crt-conversions-SZEq9)


The polynomial coefficients are represented in CRT. The CRT is a way to represent large integrers. 

Different integer/number representations highlight different aspects of the number, and hide other aspects. Each representation has its advantages and many should be considered.

*it seems that one can represent a large number with CRT with very few data.*

CRT is the representation of the residues of the moduli of an integer. The number of possible representations in CRT is defined by the module `N`. Note that the CRT moduli must be pairwise coprime, i.e the moduli and their divisors should not be the same or overlap.

With the CRT representation, it is easy to learn which moduli N a number represented is divisible by. The reasoning being that the representation for that moduli is 0.

In summary, CRT representation allow us to represent integers as coefficients (i.e which are moduli remainders). For example, `(2, 7, 19) mod(4, 9, 25)`. The `(2, 7, 19)` is the representation of the integer under the moduli `(4, 9, 25)`. The moduli are pairwise coprime and can represent all integers betwee 0 and `4*9*25`.

**Questions**
- [x] Q: why are secret keys represented in the Montgomery form? 

From [Montgomery Arithmetic from a Software Perspective*](https://eprint.iacr.org/2017/1057.pdf): "Modular multiplication is a fundamental arithmetic operation, for instance when computing in a finite field or a finite ring, and forms one of the basic operations underlying almost all currently deployed public-key cryptographic protocols. The efficient computation of modular multiplication is an important research area since optimizations, even ones resulting in a constant-factor speedup, have a direct impact on our day-to-day information security life."

So Montomery representation is "a representation of residue classes so as to speed modular multiplication without affecting the modular addition and subtraction algorithms."

## Montgomery Arithmetic for engineers

### Introduction

- [ ] Rust crate that implements Montogomery arithmetic for cryptography, abstracted and with security features such as constant time? 

Montogomery arithmetic allows for *efficient computation of modular multiplication*. Modular multiplication is represented as $C = AB\,mod\, N$.

There are different ways to calculate the modular multiplication in software:

1) **Definitional approach for modular multiplication:**

The definitional approach consists of i) first calculate $P = AB$ and then ii) $P = NQ + C$, where $Q$ and $C$ are positive integers smaller than the modulus $N$.

This method has a computational complexity of $O(n^2)$ for multiplications and $O(n)$ for divisions.

Since multiplications are expensive on computers (due to low-level binary representation), can we compute the modular multiplication without divisions?

2) **Barret multiplication**

Since most low level data representation is binary, all arithmetic over that data is represented as modulo $2^w$ and divisions or multiplications by 2 can be easily performed by shifting word bits.

The Barret multiplication uses those "cheap" word multiplications and divisions and lists of pre-computed values for the modulo used. This method does not use any division instruction and requires only $O(n^2)$ multiplication instructions.

3) **Montgomery multiplication**

Montgomery multiplication is preferred in cryptography for most cases -- there are some cases when the modulus has a special "form" and subsequently allows for a more efficient representation. In addition, Montgomery multiplication prevents against some types of cryptographic attacks (e.g. differential power analysis attacks).

### Montgomery multiplication


## NTT primer - notes

Number theory transform (NTT).

### References
[Speeding up the Number Theoretic Transform for Faster Ideal Lattice-Based Cryptography (paper)](https://eprint.iacr.org/2016/504.pdf)
[NTT notes](http://www.apfloat.org/ntt.html)
[FTT class](https://www.cs.cmu.edu/afs/cs/academic/class/15451-s10/www/lectures/lect0423.txt)

