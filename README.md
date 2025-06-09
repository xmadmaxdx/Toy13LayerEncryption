# A Toy 13-Layer Encryption System Using Classical, Stream, and Permutation Ciphers

## Overview

This repository contains the source code, implementation logic for the research project titled:

> **"A Toy 13-Layer Encryption System Using Classical, Stream, and Permutation Ciphers"**

This work explores the construction of a multi-layered encryption system composed of thirteen distinct cryptographic transformations. Each layer is designed to obscure, randomize, permute, and cryptographically protect plaintext through a cascade of classical and modern techniques. The resulting system serves as a demonstrative prototype for hybrid cryptographic architecture, unifying simplicity and theoretical security principles.

## Repository Structure

- `13_Layer_Encryption_System.ipynb` — Core Jupyter notebook containing all encryption and decryption routines, step-by-step layer logic, and interface testing.
- `README.md` — This documentation file.
- `LICENSE` — License terms.

## Encryption Pipeline Overview

The system applies the following **13 transformation layers** sequentially:

1. **Unicode Normalization (NFKD)**  
   Converts text to its canonical decomposed form, aiding in uniform processing across language inputs.

2. **Word-wise Reverse**  
   Reverses the characters of each word independently, preserving natural spacing.

3. **Autokey Vigenère Cipher**  
   Implements a polyalphabetic Caesar cipher using the plaintext to extend the key.

4. **ChaCha20 XOR Cipher**  
   XORs the byte stream with keystream generated from the ChaCha20 algorithm.

5. **Feistel Network**  
   Executes multiple rounds of a symmetric Feistel cipher using round-specific dynamic keys.

6. **Byte Permutation**  
   Rearranges the byte order deterministically using a PRNG seeded from key material.

7. **Bitwise Rotation**  
   Applies circular bit shifts per byte based on a key-derived rotation table.

8. **SHA-512 Keystream XOR**  
   Generates a pseudo-random keystream via SHA-512 hashing, which is XORed with the data.

9. **Modular Exponentiation**  
   Each byte is transformed through modular exponentiation using random primes.

10. **XOR-Salt Mixing**  
    Introduces entropy through elliptic-curve-derived salts, mixed via XOR.

11. **Key-Derived S-Box Substitution**  
    Replaces each byte via a substitution box deterministically generated from the master key.

12. **16-Byte Block Shuffle**  
    Blocks are scrambled in their 16-byte groupings using a fixed schedule.

13. **Nibble-Swap**  
    Final obfuscation by swapping the high and low 4-bit nibbles of each byte.

Each layer contributes a unique cryptographic or obfuscatory transformation, and together they aim to simulate the behavior of a layered defense model in secure communication protocols.



## Compact Encoding & Decoding

Binary output from the encryption pipeline is compacted into a **Base62-encoded string** using the `super_compact_all()` routine. This facilitates secure, alphanumeric serialization for transmission or storage.

### Example — Compact Encoding

```python
compact_str = super_compact_all(salt, ciphertext)
```

### Example — Compact Decoding

```python
salt, ciphertext = super_expand_all(compact_str)
```

This compact format maintains cryptographic fidelity while enabling simplified CLI interaction.

## Command-Line Interface

An interactive command-line interface (CLI) is provided for encoding and decoding purposes.

```python
if __name__ == "__main__":
    # CLI entry point
```

### Usage

- Type `'e'` to encrypt a plaintext message.
- Type `'d'` to decrypt a compact Base62 string.
- Type `'q'` to quit the interface.

Internally, the CLI handles secure key and nonce generation, exception handling, and encoding/decoding workflows using the defined transformation stack.

## Example CLI Session

```plaintext
Type 'e' to encode, 'd' to decode, or 'q' to quit.

Your choice (e/d/q): e
Enter plaintext:
Hello world

Super-Compact (one-field): s6iuA2tFCEQXV2gVwu1ODgqvbDdnkJfSrnWSL1XjCQJ
```

```plaintext
Your choice (e/d/q): d
Paste Super-Compact string:
s6iuA2tFCEQXV2gVwu1ODgqvbDdnkJfSrnWSL1XjCQJ

Plaintext:
Hello world
```



## Security Disclaimer

This encryption system is intended for **educational and demonstrational purposes only**. It is not recommended for deployment in any real-world secure communication context. While the layering is designed with cryptographic principles in mind, this system has not undergone formal cryptanalysis or peer review.

## Requirements

- Python 3.8+
- PyCryptodome (`pip install pycryptodome`)

## Citation

Please note that this project is currently **unpublished** and undergoing continued development. Formal publication is pending.


## License

This repository is licensed under the **GNU General Public License v3.0 (GPL-3.0)**.  
You are free to use, modify, and distribute this work under the terms of the GPL-3.0 license.

For full details, please refer to the [`LICENSE`](LICENSE) file included in this repository.


## Author

**Simanta Das**  
Independent Researcher  
