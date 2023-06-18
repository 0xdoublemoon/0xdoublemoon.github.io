---
layout: default
title: Key Management
parent: Web3
nav_order: 1
---

# Key Management

## Basic Concepts

* private key
* public key
* address
  

### Private Key

In Ethereum, private key is a random 256-bit (64 hexadecimal characters) secure number that provides the owner access to its associated account. A private key is used for signing transactions, which is a cryptographic process of verifying the transaction. With a private key, the owner can initiate transactions, send and receive Ether, and interact with smart contracts on the Ethereum network.

A private key example (please don't use this one):

```
0101001011110110000110001001001010110010000000101110111011010011000101011001010000001101011011001000000010000001100101101011001101010101011001111000011010111010110100011010111111010110111001001000100010010010101111111100001101110101101100100100011011110000 
```

### Public Key

A public key is derived from the corresponding private key using a *mathematical algorithm*. The private key is used to generate a digital signature for a transaction, while the public key is used to verify the transaction signature. The public key is derived from the private key using a mathematical process that cannot be reversed, which ensures that a private key cannot be derived from a public key.

A public key is composed of two parts: an X-coordinate and a Y-coordinate, both of which are represented by 64 hexadecimal characters (256 bits). 

#### Elliptic Curve Cryptography 
The mathematical algorithm used to derive a public key from a private key in Ethereum is called Elliptic Curve Cryptography (ECC).

In the case of Ethereum, the elliptic curve used is called secp256k1. The secp256k1 curve is defined by the following equation:

```
y^2 = x^3 + 7
```

In this equation, x and y are the coordinates of a point on the curve. The curve is defined over the field of integers modulo a prime number `p`, where:

```
p = 2^256 - 2^32 - 977
```

The result of the multiplication of the curve's generator point and the private key is a point on the curve, which represents the public key. This point is then compressed into a 33-byte hexadecimal string that starts with "0x02" or "0x03" depending on whether the Y-coordinate of the point is even or odd. The compressed form of the public key can be used in Ethereum transactions for verification purposes.

### Address

In Ethereum, an address is a 40 hexadecimal characters (160 bits) string that represents a unique identity on the network. The address is derived from the corresponding public key of an account using Keccak-256 hash function and then truncated to create a 160-bit address, represented as a 40 hexadecimal characters. The first 2 characters of the address represent the network identifier, while the remaining 38 characters represent the unique identifier of the account.


## Multi-Party Computation

Continue ...