# KHAN Encryption Algorithm

**Author:** Ayaz Khan  
**Date:** 05/27/2024

## Overview
The Keyed Hashing and Asymmetric Nonce (KHAN) encryption algorithm is a novel encryption system based on cyclic primes and unique movement patterns. This algorithm ensures that each character in the plaintext is mapped to a unique movement in the cyclic sequence, providing robust security through its unique mathematical foundations.

## Features
- **Unique Movement Patterns:** Each character in the plaintext is mapped to a unique movement in the cyclic sequence.
- **Cyclic Primes:** Utilizes cyclic prime numbers and their sequences to generate encryption keys.
- **Superposition Movements:** Handles equal clockwise and anticlockwise movements efficiently.
- **Overall Net Movement of Zero:** Ensures that the net overall movement for each pattern sequence results in zero.
- **Security:** Designed to be resistant to common brute-force and frequency analysis attacks.

## Mathematical Description

Let \( p \) be a cyclic prime number, and let \( S \) be the first \( p-1 \) digits of its cyclic sequence.

For any \( n \) and \( k \) such that \( 1 \leq k \leq n \), let:

\[ S_k = \text{substring of } S \text{ starting at } k \text{ and length } \lfloor \log_{10}(p) \rfloor \]

### Movements
- **Clockwise Movement:**
  \[ \text{clockwise}_k = (S_k - S_{k+1}) \mod (p-1) \]
- **Anticlockwise Movement:**
  \[ \text{anticlockwise}_k = (S_{k+1} - S_k) \mod (p-1) \]
- **Minimal Movement:**
  \[ \text{movement}_k = \min(\text{clockwise}_k, \text{anticlockwise}_k) \]

### Superposition Movements
A superposition movement occurs when the minimal movement is equal in both directions. The magnitude of the superposition movement is:

\[ \text{superposition} = \frac{p-1}{2} \]

### Net Overall Movement
The algorithm ensures that the overall net movement for each pattern sequence results in zero, thereby maintaining the integrity and consistency of the encryption:

\[ \sum_{k=1}^{n} \text{movement}_k = 0 \]

## Usage

### Installation

First, install the necessary dependencies using pip:

```bash
pip install pycryptodome
```

### Example Comparison Code
```python
import time
import random
import string
from Crypto.PublicKey import RSA
from Crypto.Cipher import PKCS1_OAEP
from Crypto.Cipher import AES
from Crypto.Util.Padding import pad, unpad

# Define the KHAN encryption and decryption functions here (refer to your provided code)

# Function to generate random plaintext of a given length
def generate_plaintext(length):
    return ''.join(random.choice(string.ascii_letters + string.digits) for _ in range(length))

# Function to measure encryption and decryption time for Khan encryption
def measure_khan_encryption(khan_encrypt, khan_decrypt, plaintext):
    start_time = time.time()
    ciphertext, char_to_movement, movement_to_char, z_value, superposition_sequence = khan_encrypt(plaintext)
    encryption_time = time.time() - start_time

    start_time = time.time()
    decrypted_text = khan_decrypt(ciphertext, char_to_movement, movement_to_char, z_value, superposition_sequence)
    decryption_time = time.time() - start_time

    return encryption_time, decryption_time, decrypted_text

# Function to measure encryption and decryption time for RSA
def measure_rsa_encryption(plaintext):
    key = RSA.generate(2048)
    cipher_rsa = PKCS1_OAEP.new(key)
    
    start_time = time.time()
    ciphertext = cipher_rsa.encrypt(plaintext.encode())
    encryption_time = time.time() - start_time

    start_time = time.time()
    decrypted_text = cipher_rsa.decrypt(ciphertext).decode()
    decryption_time = time.time() - start_time

    return encryption_time, decryption_time, decrypted_text

# Function to measure encryption and decryption time for AES
def measure_aes_encryption(plaintext):
    key = ''.join(random.choice(string.ascii_letters + string.digits) for _ in range(16)).encode()
    cipher_aes = AES.new(key, AES.MODE_CBC)
    iv = cipher_aes.iv

    start_time = time.time()
    ciphertext = cipher_aes.encrypt(pad(plaintext.encode(), AES.block_size))
    encryption_time = time.time() - start_time

    start_time = time.time()
    cipher_aes = AES.new(key, AES.MODE_CBC, iv)
    decrypted_text = unpad(cipher_aes.decrypt(ciphertext), AES.block_size).decode()
    decryption_time = time.time() -......
# Placeholder functions for Khan encryption and decryption

```python
def khan_encrypt(plaintext):
    # Implement your Khan encryption algorithm here
    return plaintext, {}, {}, 0, []  # Placeholder

def khan_decrypt(ciphertext, char_to_movement, movement_to_char, z_value, superposition_sequence):
    # Implement your Khan decryption algorithm here
    return ciphertext  # Placeholder
