# Challenge 01

#### Challenge Structure
- In this domain we were required to download the challenge files from the provided drive link.
- The directory contains 5 challenge files.
- This is the first one.


## Challenge Overview
- This challenge contains 2 files namely: `chal.py` and `ct`.
- `chal.py` contains the following code:
    ```py
    flag = b"flaggg{????????????????????????????????????????}"
    # len(flag) = 48
    key  = b'djpakoda'
    # len(key) = 8
    ct = bytes(x ^ y for x, y in zip(flag, cycle(key)))

    with open("ct", "wb") as ct_file:
        ct_file.write(ct)
    ```
- **Program Understanding**
    - Everything is dealt with converting them into raw bytes.
    - Variables `flag` and `key` are self descriptive.
    - We repeat the contents of the `key` to match the length of the contents of the `flag` variable.
    - We then `XOR` each byte of `flag` with each byte of `key` to generate the *encrypted* message and write it to the `ct` file.
    - Since the file contains raw bytes, we can't directly `cat` out the contents of the `ct` file.
- **Program approach**
    - Since `XOR` operation is *commutative*, we can `XOR` the encrypted message with the key again to get the decrypted message which will be our `flag`.
    - We use the same method in the program to solve the challenge.
- **Solution**
    - Read the bytes from the `ct` file.
    - `XOR` it with the `key` cycled to match its length.
    - Print the output.

**The solution code:**
```py
from itertools import cycle

key = b'djpakoda'

with open("ct", "rb") as ct_file:
    content = ct_file.read()

decrypt = bytes(x ^ y for x, y in zip(content, cycle(key)))
print(decrypt)
```

## Solve
**Flag:** `flaggg{w0w_g0od_j0b_V3ry_gr34t_amazing_AW35OMEE}`


## New Learnings
- The encryption function.
- The decryption function.
- Basics of Cryptography.
- Symmetric Encryption.
- Advanced Encryption Standard (AES) properties.
    - Confusion
        - The key is generally small and repeated to match the decrypted message length by repeating itself over and over.
        - Each bit of the cipher text depends on several parts of the key, obscuring the connections between the two.
    - Diffusion
        - A change in a single bit of plaintext produces a change in about half the bits of ciphertext.
- AES encrypts only on bytes multiple of 16.
    - Key size: 128/192/256 bits.
    - Block size: 128 bits.


## Resources
- [Cryptography: Introduction by pwn.college](https://www.youtube.com/watch?v=YBdzIxeseuE&list=PL-ymxv0nOtqpBYQKnbivatYlfQ3Ygf63_&index=1)
- [Cryptography: Symmetric Encryption by pwn.college](https://www.youtube.com/watch?v=CJrCzOR2qhk&list=PL-ymxv0nOtqpBYQKnbivatYlfQ3Ygf63_&index=2)