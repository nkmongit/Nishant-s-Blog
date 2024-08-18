---
date created: Saturday, August 10th 2024, 6:41:28 pm
date modified: Saturday, August 17th 2024, 5:44:03 pm
tags:
  - 100xdevs
  - web3
  - cryptography
  - moc/web3
  - encryption
  - decryption
  - sha-256
---
# Banks vs Blockchains

### How banks do Auth

In traditional banks, you have a `username` and `password` that are enough for you to

1. Look at your funds
2. Transfer funds
3. Look at your existing transactions

![[keypair1.png]]

### How Blockchains do Auth?

If you ever want to create an `account` on a blockchain, you need to generate a `public-private` key-pair.
#### Public Private Key-pair

A public-private key pair is a set of two keys used in `asymmetric cryptography`. These two keys have the following characteristics:

**Public Key**: The public key is a string that can be shared openly.

![[keypair2.png]]

For example - [https://etherscan.io/address/0xD9a657ACB3960DB92AaaA32942019bD3c473FCCB](https://etherscan.io/address/0xD9a657ACB3960DB92AaaA32942019bD3c473FCCB)

**Private key:** The private key is a secret string that must be kept confidential.

![[keypair3.png]]

# Bits and Bytes

#### **What is a Bit?**

A bit is the smallest unit of data in a computer and can have one of two values: 0 or 1.
Think of a bit like a light switch that can be either off (0) or on (1).

#### What is a byte?

A byte is a group of `8` bits. It’s the standard unit of data used to represent a single character in memory. Since each bit can be either 0 or 1, a byte can have 2^8 (256) possible values, ranging from 0 to 255

#### Assignment
What is the `11001010` converted to a `decimals` ?

Answer
- **2^7:** 1×27=1×128=128
- **2^6:** 1×26=1×64=64
- **2^5:** 0×25=0×32=0
- **2^4:** 0×24=0×16=0
- **2^3:** 1×23=1×8=8
- **2^2:** 0×22=0×4=0
- **2^1:** 1×21=1×2=2
- **2^0:** 0×20=0×1=0 = 202

#### Representing bits and bytes in JS

- Bit
```javascript
const x = 0;
console.log(x);
```

- Byte
```javascript
const x = 202
console.log(x);
```

- Array of bytes
```javascript
const bytes = [202, 244, 1, 23]
console.log(bytes);
```

#### UInt8Array
A better way to represent an array of bytes is to use a `UInt8Array` in JS

```javascript
let bytes = new Uint8Array([0, 255, 127, 128]);
console.log(bytes)
```

Why use `UInt8Array` over `native arrays` ?

- They use less space. Every number takes 64 bits (8 bytes). But every value in a `UInt8Array` takes 1 byte.
- UInt8Array Enforces constraints - It makes sure every element doesn’t exceed 255.

#### Assignment -

What do you think happens to the first element here? Does it throw an error?
```javascript
let uint8Arr = new Uint8Array([0, 255, 127, 128]);
uint8Arr[1] = 300;
```

private keys => array of bytes (32 bytes)
public keys => 

# Encoding

Bytes are cool but highly unreadable. Imagine telling someone
```javascript
Hey, my name is 00101011101010101020
```
It’s easier to `encode` data so it is more `human readable` . 
Some common encoding include:
1. ASCII
2. Hex
3. Base64
4. Base58

### ASCII

<font color="#c0504d">`1 character = 7 bits`</font>

Every byte corresponds to a `text` on the `computer` . 
Here is a complete list - [https://www.w3schools.com/charsets/ref_html_ascii.asp#:~:text=The ASCII Character Set&text=ASCII is a 7-bit,are all based on ASCII](https://www.w3schools.com/charsets/ref_html_ascii.asp#:~:text=The%20ASCII%20Character%20Set&text=ASCII%20is%20a%207%2Dbit,are%20all%20based%20on%20ASCII).

  
**Bytes to ASCII**

```javascript
function bytesToAscii(byteArray) {
  return byteArray.map(byte => String.fromCharCode(byte)).join('');
}

// Example usage:
const bytes = [72, 101, 108, 108, 111]; // Corresponds to "Hello"
const asciiString = bytesToAscii(bytes);
console.log(asciiString); // Output: "Hello"
```

**ASCII to bytes**

```javascript
function asciiToBytes(asciiString) {
  const byteArray = [];
  for (let i = 0; i < asciiString.length; i++) {
    byteArray.push(asciiString.charCodeAt(i));
  }
  return byteArray;
}

// Example usage:
const ascii = "Hello";
const byteArray = asciiToBytes(ascii);
console.log(byteArray); // Output: [72, 101, 108, 108, 111]
```

**UInt8Array to ASCII**

```javascript
function bytesToAscii(byteArray) {
  return new TextDecoder().decode(byteArray);
}

// Example usage:
const bytes = new Uint8Array([72, 101, 108, 108, 111]); // Corresponds to "Hello"
const asciiString = bytesToAscii(bytes);
console.log(asciiString); // Output: "Hello"
```

**ASCII to UInt8Array**

```javascript
function asciiToBytes(asciiString) {
  return new Uint8Array([...asciiString].map(char => char.charCodeAt(0)));
}

// Example usage:
const ascii = "Hello";
const byteArray = asciiToBytes(ascii);
console.log(byteArray); // Output: Uint8Array(5) [72, 101, 108, 108, 111]
```

![[ascii1.png]]

### Hex

`1 character = 4 bits`

A single hex character can be any of the 16 possible values: `0-9` and `A-F`.

**Array to Hex**

```javascript
function arrayToHex(byteArray) {
  let hexString = '';
  for (let i = 0; i < byteArray.length; i++) {
    hexString += byteArray[i].toString(16).padStart(2, '0');
  }
  return hexString;
}

// Example usage:
const byteArray = new Uint8Array([72, 101, 108, 108, 111]); // Corresponds to "Hello"
const hexString = arrayToHex(byteArray);
console.log(hexString); // Output: "48656c6c6f"
```

**Hex to Array**

```javascript
function hexToArray(hexString) {
  const byteArray = new Uint8Array(hexString.length / 2);
  for (let i = 0; i < byteArray.length; i++) {
    byteArray[i] = parseInt(hexString.substr(i * 2, 2), 16);
  }
  return byteArray;
}

// Example usage:
const hex = "48656c6c6f";
const byteArrayFromHex = hexToArray(hex);
console.log(byteArrayFromHex); // Output: Uint8Array(5) [72, 101, 108, 108, 111]
```

Ref - [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt)

The `padStart(2, '0')` method is used to ensure that each byte in the `byteArray` is represented as a two-character hexadecimal string.

![[hex1.png]]

### Base64
`1 character = 6 bits`

Base64 encoding uses 64 different characters (`A-Z`, `a-z`, `0-9`, `+`, `/`), which means each character can represent one of 64 possible values.
[Base64 Encoding](https://www.base64encode.org/)

Encode
```javascript
const uint8Array = new Uint8Array([72, 101, 108, 108, 111]);
const base64Encoded = Buffer.from(uint8Array).toString("base64");
console.log(base64Encoded);
```


### Base58

It is similar to **Base64** but uses a different set of characters to avoid visually similar characters and to make the encoded output more user-friendly

**Base58** uses 58 different characters:
- Uppercase letters: `A-Z` (excluding `I` and `O`)
- Lowercase letters: `a-z` (excluding `l`)
-   
    Numbers: `1-9` (excluding `0`)

**Encode**

```javascript
const bs58 = require('bs58');

function uint8ArrayToBase58(uint8Array) {
  return bs58.encode(uint8Array);
}

// Example usage:
const byteArray = new Uint8Array([72, 101, 108, 108, 111]); // Corresponds to "Hello"
const base58String = uint8ArrayToBase58(byteArray);
console.log(base58String); // Output: Base58 encoded string
```

**Decode**

```javascript
const bs58 = require('bs58');

function base58ToUint8Array(base58String) {
  return bs58.decode(base58String);
}

// Example usage:
const base58 = base58String; // Use the previously encoded Base58 string
const byteArrayFromBase58 = base58ToUint8Array(base58);
console.log(byteArrayFromBase58); // Output: Uint8Array(5) [72, 101, 108, 108, 111]
```


# Hashing vs Encryption

### Hashing
Hashing is a process of converting data (like a file or a message) into a fixed-size string of characters, which typically appears random.

![[hash1.png]]

Common hashing algorithms - **SHA-256, MD5**

### Encryption
Encryption is the process of converting plaintext data into an unreadable format, called ciphertext, using a specific algorithm and a key. The data can be decrypted back to its original form only with the appropriate key.

**Key Characteristics:**
- **Reversible**: With the correct key, the cipher-text can be decrypted back to plain-text.
- **Key-dependent**: The security of encryption relies on the secrecy of the key.
- **Two main types**:
- **Symmetric encryption**: The same key is used for both encryption and decryption.
- **Asymmetric encryption**: Different keys are used for encryption (public key) and decryption (private key).

### Symmetric Encryption

![[symmetric.png]]

![[signkey.png]]

**Code**

```javascript
const crypto = require('crypto');

// Generate a random encryption key
const key = crypto.randomBytes(32); // 32 bytes = 256 bits
const iv = crypto.randomBytes(16); // Initialization vector (IV)

// Function to encrypt text
function encrypt(text) {
    const cipher = crypto.createCipheriv('aes-256-cbc', key, iv);
    let encrypted = cipher.update(text, 'utf8', 'hex');
    encrypted += cipher.final('hex');
    return encrypted;
}

// Function to decrypt text
function decrypt(encryptedText) {
    const decipher = crypto.createDecipheriv('aes-256-cbc', key, iv);
    let decrypted = decipher.update(encryptedText, 'hex', 'utf8');
    decrypted += decipher.final('utf8');
    return decrypted;
}

// Example usage
const textToEncrypt = 'Hello, World!';
const encryptedText = encrypt(textToEncrypt);
const decryptedText = decrypt(encryptedText);

console.log('Original Text:', textToEncrypt);
console.log('Encrypted Text:', encryptedText);
console.log('Decrypted Text:', decryptedText);
```

### Asymmetric Encryption

![[asymetric.png]]



# Asymmetric Encryption

Asymmetric encryption, also known as public-key cryptography, is a type of encryption that uses a pair of keys: a public key and a private key. The keys are mathematically related, but it is computationally infeasible to derive the `private key` from the `public key`.

**Public Key**: The public key is a string that can be shared openly

**Private Key**: The private key is a secret cryptographic code that must be kept confidential. It is used to de-crypt data encrypted with the corresponding public key or to create digital signatures.

![[asymc.png]]

#### **Common Asymmetric Encryption Algorithms:**

1. **RSA** - Rivest–Shamir–Adleman
		- Used very big two prime numbers and multiply them we get a very big string, from that string it's hard to find those two prime numbers.
1. **ECC** - Elliptic Curve Cryptography (ECDSA) - ETH and BTC
2. **EdDSA -** Edwards-curve Digital Signature Algorithm  - SOL

![[ellipticcurve.png]]

**How eliptic curves work** - [https://www.youtube.com/watch?v=NF1pwjL9-DE&](https://www.youtube.com/watch?v=NF1pwjL9-DE&)

#### Common Eleptic Curves
1. secp256k1 - BTC and ETH
2. ed25519 - SOL

**Few use-cases of public key cryptography -**
1. SSL/TLS certificates
2. SSH keys to connect to servers/push to github
3. Blockchains and cryptocurrencies
# Creating a public/private key-pair

Let’s look at various ways of creating public/private key-pairs, signing messages and verifying them

![[generatekeypair.png]]

#### **EdDSA - Edwards-curve Digital Signature Algorithm  - ED25519**

**Using `@noble/ed25519`**

```javascript
import * as ed from "@noble/ed25519";

async function main() {
  // Generate a secure random private key
  const privKey = ed.utils.randomPrivateKey();

  // Convert the message "hello world" to a Uint8Array
  const message = new TextEncoder().encode("hello world");

  // Generate the public key from the private key
  const pubKey = await ed.getPublicKeyAsync(privKey);

  // Sign the message
  const signature = await ed.signAsync(message, privKey);

  // Verify the signature
  const isValid = await ed.verifyAsync(signature, message, pubKey);

  // Output the result
  console.log(isValid); // Should print `true` if the signature is valid
}

main();
```

**Using `@solana/web3.js`**

```javascript
import { Keypair } from "@solana/web3.js";
import nacl from "tweetnacl";

// Generate a new keypair
const keypair = Keypair.generate();

// Extract the public and private keys
const publicKey = keypair.publicKey.toString();
const secretKey = keypair.secretKey;

// Display the keys
console.log("Public Key:", publicKey);
console.log("Private Key (Secret Key):", secretKey);

// Convert the message "hello world" to a Uint8Array
const message = new TextEncoder().encode("hello world");

const signature = nacl.sign.detached(message, secretKey);
const result = nacl.sign.detached.verify(
  message,
  signature,
  keypair.publicKey.toBytes(),
);

console.log(result);
```

#### **ECDSA (Elliptic Curve Digital Signature Algorithm) - secp256k1**

**Using `@noble/secp256k1`**

```javascript
import * as secp from "@noble/secp256k1";

async function main() {
  const privKey = secp.utils.randomPrivateKey(); // Secure random private key
  // sha256 of 'hello world'
  const msgHash =
    "b94d27b9934d3e08a52e52d7da7dabfac484efe37a5380ee9088f7ace2efcde9";
  const pubKey = secp.getPublicKey(privKey);
  const signature = await secp.signAsync(msgHash, privKey); // Sync methods below
  const isValid = secp.verify(signature, msgHash, pubKey);
  console.log(isValid);
}

main();
```

**Using `ethers`**

```javascript
import { ethers } from "ethers";

// Generate a random wallet
const wallet = ethers.Wallet.createRandom();

// Extract the public and private keys
const publicKey = wallet.address;
const privateKey = wallet.privateKey;

console.log("Public Key (Address):", publicKey);
console.log("Private Key:", privateKey);

// Message to sign
const message = "hello world";

// Sign the message using the wallet's private key
const signature = await wallet.signMessage(message);
console.log("Signature:", signature);

// Verify the signature
const recoveredAddress = ethers.verifyMessage(message, signature);

console.log("Recovered Address:", recoveredAddress);
console.log("Signature is valid:", recoveredAddress === publicKey);
```