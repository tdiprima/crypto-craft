# Node.js Cryptography Examples

Hands-on reference implementations of symmetric encryption, password hashing, file encryption, and HMAC authentication using Node.js's built-in `crypto` module — no third-party dependencies required.

## Cryptography Is Hard to Get Right

Developers who need to encrypt data or verify integrity often reach for third-party libraries without understanding what's happening underneath — or they roll their own implementations using outdated approaches (MD5, SHA1 for passwords, ECB mode, static IVs). The result is code that looks secure but isn't.

## Learning by Working Example

This project demonstrates correct, production-aware usage of the Node.js `crypto` module across the most common real-world scenarios: AES-192/256 symmetric encryption and decryption, password-derived key generation with `scrypt`, HMAC-SHA256 message authentication, and stream-based file encryption. Each file is a focused, runnable example with inline comments explaining the why behind each step.

It also includes a reusable utility module (`cryptoUtils.js`) with async encrypt/decrypt functions and a test script that verifies round-trip correctness.

## Example: Encrypt and Decrypt a String

```js
const { encryptData, decryptData } = require('./src/cryptoUtils');

const password = 'supersecret';
const original = 'Hello, World!';

const encrypted = await encryptData(original, password);
// => 'a3f8c2...' (hex-encoded AES-192-CBC ciphertext)

const decrypted = await decryptData(encrypted, password);
// => 'Hello, World!'
```

Key derivation uses `crypto.scrypt` — a memory-hard function designed to resist brute-force attacks, appropriate for password-based encryption.

## Usage

**Prerequisites:** Node.js 16+

```bash
# Encrypt and decrypt a string (reusable utility)
node src/testCryptoUtils.js

# AES-192-CBC encryption
node src/encryptWithAES192.js

# AES-192-CBC decryption
node src/decryptWithAES192.js

# Decipher a hardcoded encrypted string
node src/decipher-encrypted-text.js

# AES-256-CTR password encryption/decryption
node src/encryptAndDecryptPasswordAES256.js

# Stream-based AES-256-CTR file encryption
node src/encryptFileWithAES256.js

# HMAC-SHA256 message authentication
node src/generateHmacSha256.js
```

For context on when to use AES vs. SHA, see [`docs/differenceBetweenAESandSHA.md`](docs/differenceBetweenAESandSHA.md).
