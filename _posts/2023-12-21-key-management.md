---
layout: post
title: Key Management
excerpt_image: ../../../../assets/images/key-management.jpg 
categories: Web3
tags: [web3, advanced]
---

<script type="text/javascript"
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS_CHTML">
</script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath: [['$','$'], ['\\(','\\)']],
      processEscapes: true},
      jax: ["input/TeX","input/MathML","input/AsciiMath","output/CommonHTML"],
      extensions: ["tex2jax.js","mml2jax.js","asciimath2jax.js","MathMenu.js","MathZoom.js","AssistiveMML.js", "[Contrib]/a11y/accessibility-menu.js"],
      TeX: {
      extensions: ["AMSmath.js","AMSsymbols.js","noErrors.js","noUndefined.js"],
      equationNumbers: {
      autoNumber: "AMS"
      }
    }
  });
</script>


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

$$
y^2 = x^3 + 7
$$

In this equation, x and y are the coordinates of a point on the curve. The curve is defined over the field of integers modulo a prime number `p`, where:

$$
p = 2^{256} - 2^{32} - 977
$$

The result of the multiplication of the curve's generator point and the private key is a point on the curve, which represents the public key. This point is then compressed into a 33-byte hexadecimal string that starts with "0x02" or "0x03" depending on whether the Y-coordinate of the point is even or odd. The compressed form of the public key can be used in Ethereum transactions for verification purposes.

### Address

In Ethereum, an address is a 40 hexadecimal characters (160 bits) string that represents a unique identity on the network. The address is derived from the corresponding public key of an account using Keccak-256 hash function and then truncated to create a 160-bit address, represented as a 40 hexadecimal characters. The first 2 characters of the address represent the network identifier, while the remaining 38 characters represent the unique identifier of the account.


## Multi-Party Computation

In short, Multi-party computation(MPC) refers to cryptographic technique that enables different parties to joinly perform computation on their individual inputs without actually revealing their inputs to each other. One of the famous example is Yao's Millionaires' Problem[1] which allows two parties to determine which of them has more wealth without revealing any snesitive information about their actual wealth to each other or anyone else.

MPC can be used in many domains. But here we will focus on the usage on blockchain key management - multi-party threshold ECDSA.

There are many open-source algorithms implementing the threshold signature schemes. For examples:

| Protocol | Repo                                           | Tag    |
| -------- | ---------------------------------------------- | ------ |
| DMZ+21   | https://github.com/LatticeX-Foundation/opentss | rust   |
| GG18/20  | https://github.com/ZenGo-X/multi-party-ecdsa   | rust   |
| GG18     | https://github.com/bnb-chain/tss-lib           | golang |
| GG20     | https://gitlab.com/thorchain/tss/go-tss        | golang |


To understand how multi-party threshold ECDSA works by taking an example on GG18.

### Basic arithmetic concepts

#### Modular arithmetic

Give two integers a, b, if take a natural number (p) from a, b and the remainder are the same, then we say $a \equiv b (mod p)$

#### Primitive root modulo n [2]

It is mainly used to convert manipulation to addition.

#### Diffie-Hellman key exchange

TODO: add this part later


#### Lagrange polynomial

TODO: add this part later

### Threshold signature sheme

Protocol consists two phases: sharing phase and reconstruction phase.

In the sharing phase, each player will broadcast their points. Other players uses these points to calculate the weight and value which can be used to reconstruct the private key in the next phase.

3-to-4 shares

Given a private key $u=140$, split it randomly into 4 shares $(10, 20, 50, 60)$ which $140 = 10 + 20 + 50 + 60$ and store it into 4 different db that handled by 4 servers.


Each server keeps one key share and a polynomial function $F_i = a_ix^2+b_ix+c_i \  ( a_i, b_i \in N, c_i \in \{10, 20, 50, 60\}, i \in \{1, 2, 3, 4 \})$


Take an example:

Server 1 stores polynomial function $F_1(x)= x^2+2x+10$, key share $u_1 = 10$

Server 2 stores polynomial function $F_2(x)= x^2+4x+20$, key share $u_2 = 20$

Server 3 stores polynomial function $F_3(x)= x^2+5x+50$, key share $u_3 = 50$

Server 4 stores polynomial function $F_4(x)= x^2+10x+60$, key share $u_4 = 60$




Then,

Randomly choose 4 different x. eg. $x_1=1$, $x_2 = 2$, $x_3 = 3$, $x_4 = 4$.

Calculate  from each server

From server 1, we get 4 points, $F_1(1) = 13$, $F_1(2) = 18$, $F_1(3) = 25$, $F_1(4) = 34$

Similarly, we get 4 points from server 2, 3 and 4.


Then save

 $y_1 = F_1(1)+F_2(1)+F_3(1)+F_4(1) = 165$ to server 1, $198$ to server 2, $239$ to server 3, $288$ to server 4.




In the private key reconstruction section, let's use server 1, server 2 and server 3 only.

Apply Lagrange interpolation formula in each server,

Server 1, $L_1(x) =\frac{ (x - 2)(x - 3)}{ (1- 2)(1-3)}$, and $L_1(0) = 3$, we get $u_1 = L_1(0) * y_1 = 165 * 3$

Server 2, $L_2(x) =\frac{ (x - 1)(x - 3)}{ (2- 1)(2-3)}$, and $L_2(0) = -3$, we get $u_3 = L_3(0) * y_3 = 239 * 1$

Server 3, $L_3(x) =\frac{ (x - 1)(x - 2)}{ (3- 1)(3-2)}$, and $L_3(0) = 1$, we get $u_3 = L_3(0) * y_3 = 239 * 1$

private key 
$$
u=L_1(0) * y_1 + L_2(0) * y_2+ L_2(0) * y_2 = 3*165+(-3)*198+1*239=140
$$


In the DSA signing process,$y_{public key} = g^u$, u is the private key. since $g^u = g^{u_1+u_2+u_3} = g^{u_1} * g^{u_2} * g^{u_3}$, so it could be signed by each server and join then together in the end and will get the same result as using the private key to sign.

If user forget one key share, or the key pair leaks, we can repeat the process above to select a different polynomial function set for each server.


## References

* [1] [Yao's Millionaires' Problem](https://en.wikipedia.org/wiki/Yao%27s_Millionaires%27_problem)
* [2] [Primitive root](https://brilliant.org/wiki/primitive-roots/)