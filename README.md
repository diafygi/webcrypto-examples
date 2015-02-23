# Web Cryptography API Examples

Live Table: https://diafygi.github.io/webcrypto-examples

I couldn't find anywhere that had clear examples of WebCrytoAPI, so I
wrote examples and made a live table with them. Pull requests welcome!

1. [RSASSA-PKCS1-v1_5](#rsassa-pkcs1-v1_5)
    * [generateKey](#generatekey)
    * [importKey](#importkey)
    * [exportKey](#exportkey)
    * [sign](#sign)
    * [verify](#verify)
2. [RSA-PSS](#rsa-pss)
    * [generateKey](#generatekey-1)
    * [importKey](#importkey-1)
    * [exportKey](#exportkey-1)
    * [sign](#sign-1)
    * [verify](#verify-1)
3. [RSA-OAEP](#rsa-oaep)
    * [generateKey](#generatekey-2)
    * [importKey](#importkey-2)
    * [exportKey](#exportkey-2)
    * [encrypt](#encrypt)
    * [decrypt](#decrypt)
4. [ECDSA](#ecdsa)
    * [generateKey](#generatekey-3)
    * [importKey](#importkey-3)
    * [exportKey](#exportkey-3)
    * [sign](#sign-2)
    * [verify](#verify-2)
5. [ECDH](#ecdh)
    * [generateKey](#generatekey-4)
    * [importKey](#importkey-4)
    * [exportKey](#exportkey-4)
    * [deriveBits](#derivebits)
    * [deriveKey](#derivekey)
6. [AES-CTR](#aes-ctr)
    * [generateKey](#generatekey-5)
    * [importKey](#importkey-5)
    * [exportKey](#exportkey-5)
    * [encrypt](#encrypt-1)
    * [decrypt](#decrypt-1)
7. [AES-CBC](#aes-cbc)
    * [generateKey](#generatekey-6)
    * [importKey](#importkey-6)
    * [exportKey](#exportkey-6)
    * [encrypt](#encrypt-2)
    * [decrypt](#decrypt-2)
8. [AES-CMAC](#aes-cmac)
    * [generateKey](#generatekey-7)
    * [importKey](#importkey-7)
    * [exportKey](#exportkey-7)
    * [sign](#sign-3)
    * [verify](#verify-3)
9. [AES-GCM](#aes-gcm)
    * [generateKey](#generatekey-8)
    * [importKey](#importkey-8)
    * [exportKey](#exportkey-8)
    * [encrypt](#encrypt-3)
    * [decrypt](#decrypt-3)
10. [AES-CFB](#aes-cfb)
    * [generateKey](#generatekey-9)
    * [importKey](#importkey-9)
    * [exportKey](#exportkey-9)
    * [encrypt](#encrypt-4)
    * [decrypt](#decrypt-4)
11. [AES-KW](#aes-kw)
    * [generateKey](#generatekey-10)
    * [importKey](#importkey-10)
    * [exportKey](#exportkey-10)
12. [HMAC](#hmac)
    * [generateKey](#generatekey-11)
    * [importKey](#importkey-11)
    * [exportKey](#exportkey-11)
    * [sign](#sign-4)
    * [verify](#verify-4)
13. [DH](#dh)
    * [generateKey](#generatekey-12)
    * [importKey](#importkey-12)
    * [exportKey](#exportkey-12)
    * [deriveBits](#derivebits-1)
    * [deriveKey](#derivekey-1)
14. [SHA-1](#sha-1)
    * [digest](#digest)
15. [SHA-256](#sha-256)
    * [digest](#digest-1)
16. [SHA-384](#sha-384)
    * [digest](#digest-2)
17. [SHA-512](#sha-512)
    * [digest](#digest-3)
18. [CONCAT](#concat)
    * [importKey](#importkey-13)
    * [deriveBits](#derivebits-2)
    * [deriveKey](#derivekey-2)
19. [HKDF-CTR](#hkdf-ctr)
    * [importKey](#importkey-14)
    * [deriveBits](#derivebits-3)
    * [deriveKey](#derivekey-3)
20. [PBKDF2](#pbkdf2)
    * [generateKey](#generatekey-13)
    * [importKey](#importkey-15)
    * [deriveBits](#derivebits-4)
    * [deriveKey](#derivekey-4)

##RSASSA-PKCS1-v1_5
###generateKey
```javascript
window.crypto.subtle.generateKey(
    {
        name: "RSASSA-PKCS1-v1_5",
        modulusLength: 2048, //can be 1024, 2048, or 4096
        publicExponent: new Uint8Array([0x01, 0x00, 0x01]),
        hash: {name: "SHA-256"}, //can be "SHA-1", "SHA-256", "SHA-384", or "SHA-512"
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["sign", "verify"] //can be any combination of "sign" and "verify"
)
.then(function(key){
    //returns a keypair object
    console.log(key);
    console.log(key.publicKey);
    console.log(key.privateKey);
})
.catch(function(err){
    console.error(err);
});
```
###importKey
```javascript
window.crypto.subtle.importKey(
    "jwk", //can be "jwk", "spki", or "pkcs8"
    {   //this is an example jwk key, other key types are Uint8Array objects
        kty: "RSA",
        e: "AQAB",
        n: "vGO3eU16ag9zRkJ4AK8ZUZrjbtp5xWK0LyFMNT8933evJoHeczexMUzSiXaLrEFSyQZortk81zJH3y41MBO_UFDO_X0crAquNrkjZDrf9Scc5-MdxlWU2Jl7Gc4Z18AC9aNibWVmXhgvHYkEoFdLCFG-2Sq-qIyW4KFkjan05IE",
        alg: "RS256",
        ext: true,
    },
    {   //these are the algorithm options
        name: "RSASSA-PKCS1-v1_5",
        hash: {name: "SHA-256"}, //can be "SHA-1", "SHA-256", "SHA-384", or "SHA-512"
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["verify"] //"verify" for public key import, "sign" for private key imports
)
.then(function(publicKey){
    //returns a publicKey (or privateKey if you are importing a private key)
    console.log(publicKey);
})
.catch(function(err){
    console.error(err);
});
```
###exportKey
```javascript
window.crypto.subtle.exportKey(
    "jwk", //can be "jwk", "spki", or "pkcs8"
    publicKey //can be a publicKey or privateKey, as long as extractable was true
)
.then(function(keydata){
    //returns the exported key data
    console.log(keydata);
})
.catch(function(err){
    console.error(err);
});
```
###sign
```javascript
window.crypto.subtle.sign(
    {
        name: "RSASSA-PKCS1-v1_5",
    },
    privateKey, //from generateKey or importKey above
    data //ArrayBuffer of data you want to sign
)
.then(function(signature){
    //returns an ArrayBuffer containing the signature
    console.log(new Uint8Array(signature));
})
.catch(function(err){
    console.error(err);
});
```
###verify
```javascript
window.crypto.subtle.verify(
    {
        name: "RSASSA-PKCS1-v1_5",
    },
    publicKey, //from generateKey or importKey above
    signature, //ArrayBuffer of the signature
    data //ArrayBuffer of the data
)
.then(function(isvalid){
    //returns a boolean on whether the signature is true or not
    console.log(isvalid);
})
.catch(function(err){
    console.error(err);
});
```

##RSA-PSS
###generateKey
```javascript
window.crypto.subtle.generateKey(
    {
        name: "RSA-PSS",
        modulusLength: 2048, //can be 1024, 2048, or 4096
        publicExponent: new Uint8Array([0x01, 0x00, 0x01]),
        hash: {name: "SHA-256"}, //can be "SHA-1", "SHA-256", "SHA-384", or "SHA-512"
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["sign", "verify"] //can be any combination of "sign" and "verify"
)
.then(function(key){
    //returns a keypair object
    console.log(key);
    console.log(key.publicKey);
    console.log(key.privateKey);
})
.catch(function(err){
    console.error(err);
});
```
###importKey
```javascript
window.crypto.subtle.importKey(
    "jwk", //can be "jwk", "spki", or "pkcs8"
    {   //this is an example jwk key, other key types are Uint8Array objects
        kty: "RSA",
        e: "AQAB",
        n: "vGO3eU16ag9zRkJ4AK8ZUZrjbtp5xWK0LyFMNT8933evJoHeczexMUzSiXaLrEFSyQZortk81zJH3y41MBO_UFDO_X0crAquNrkjZDrf9Scc5-MdxlWU2Jl7Gc4Z18AC9aNibWVmXhgvHYkEoFdLCFG-2Sq-qIyW4KFkjan05IE",
        alg: "PS256",
        ext: true,
    },
    {   //these are the algorithm options
        name: "RSA-PSS",
        hash: {name: "SHA-256"}, //can be "SHA-1", "SHA-256", "SHA-384", or "SHA-512"
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["verify"] //"verify" for public key import, "sign" for private key imports
)
.then(function(publicKey){
    //returns a publicKey (or privateKey if you are importing a private key)
    console.log(publicKey);
})
.catch(function(err){
    console.error(err);
});
```
###exportKey
```javascript
window.crypto.subtle.exportKey(
    "jwk", //can be "jwk", "spki", or "pkcs8"
    publicKey //can be a publicKey or privateKey, as long as extractable was true
)
.then(function(keydata){
    //returns the exported key data
    console.log(keydata);
})
.catch(function(err){
    console.error(err);
});
```
###sign
```javascript
window.crypto.subtle.sign(
    {
        name: "RSA-PSS",
        saltLength: 128, //the length of the salt
    },
    privateKey, //from generateKey or importKey above
    data //ArrayBuffer of data you want to sign
)
.then(function(signature){
    //returns an ArrayBuffer containing the signature
    console.log(new Uint8Array(signature));
})
.catch(function(err){
    console.error(err);
});
```
###verify
```javascript
window.crypto.subtle.verify(
    {
        name: "RSA-PSS",
        saltLength: 128, //the length of the salt
    },
    publicKey, //from generateKey or importKey above
    signature, //ArrayBuffer of the signature
    data //ArrayBuffer of the data
)
.then(function(isvalid){
    //returns a boolean on whether the signature is true or not
    console.log(isvalid);
})
.catch(function(err){
    console.error(err);
});
```

##RSA-OAEP
###generateKey
```javascript
window.crypto.subtle.generateKey(
    {
        name: "RSA-OAEP",
        modulusLength: 2048, //can be 1024, 2048, or 4096
        publicExponent: new Uint8Array([0x01, 0x00, 0x01]),
        hash: {name: "SHA-256"}, //can be "SHA-1", "SHA-256", "SHA-384", or "SHA-512"
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["encrypt", "decrypt"] //can be any combination of "encrypt" and "decrypt"
)
.then(function(key){
    //returns a keypair object
    console.log(key);
    console.log(key.publicKey);
    console.log(key.privateKey);
})
.catch(function(err){
    console.error(err);
});
```
###importKey
```javascript
window.crypto.subtle.importKey(
    "jwk", //can be "jwk", "spki", or "pkcs8"
    {   //this is an example jwk key, other key types are Uint8Array objects
        kty: "RSA",
        e: "AQAB",
        n: "vGO3eU16ag9zRkJ4AK8ZUZrjbtp5xWK0LyFMNT8933evJoHeczexMUzSiXaLrEFSyQZortk81zJH3y41MBO_UFDO_X0crAquNrkjZDrf9Scc5-MdxlWU2Jl7Gc4Z18AC9aNibWVmXhgvHYkEoFdLCFG-2Sq-qIyW4KFkjan05IE",
        alg: "RSA-OAEP-256",
        ext: true,
    },
    {   //these are the algorithm options
        name: "RSA-OAEP",
        hash: {name: "SHA-256"}, //can be "SHA-1", "SHA-256", "SHA-384", or "SHA-512"
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["encrypt"] //"encrypt" for public key import, "decrypt" for private key imports
)
.then(function(publicKey){
    //returns a publicKey (or privateKey if you are importing a private key)
    console.log(publicKey);
})
.catch(function(err){
    console.error(err);
});
```
###exportKey
```javascript
window.crypto.subtle.exportKey(
    "jwk", //can be "jwk", "spki", or "pkcs8"
    publicKey //can be a publicKey or privateKey, as long as extractable was true
)
.then(function(keydata){
    //returns the exported key data
    console.log(keydata);
})
.catch(function(err){
    console.error(err);
});
```
###encrypt
```javascript
window.crypto.subtle.encrypt(
    {
        name: "RSA-OAEP",
        //label: Uint8Array([...]) //optional
    },
    publicKey, //from generateKey or importKey above
    data //ArrayBuffer of data you want to encrypt
)
.then(function(encrypted){
    //returns an ArrayBuffer containing the encrypted data
    console.log(new Uint8Array(encrypted));
})
.catch(function(err){
    console.error(err);
});
```
###decrypt
```javascript
window.crypto.subtle.decrypt(
    {
        name: "RSA-OAEP",
        //label: Uint8Array([...]) //optional
    },
    privateKey, //from generateKey or importKey above
    data //ArrayBuffer of the data
)
.then(function(decrypted){
    //returns an ArrayBuffer containing the decrypted data
    console.log(new Uint8Array(decrypted));
})
.catch(function(err){
    console.error(err);
});
```

##ECDSA
###generateKey
```javascript
window.crypto.subtle.generateKey(
    {
        name: "ECDSA",
        namedCurve: "P-256", //can be "P-256", "P-384", or "P-521"
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["sign", "verify"] //can be any combination of "sign" and "verify"
)
.then(function(key){
    //returns a keypair object
    console.log(key);
    console.log(key.publicKey);
    console.log(key.privateKey);
})
.catch(function(err){
    console.error(err);
});
```
###importKey
```javascript
window.crypto.subtle.importKey(
    "jwk", //can be "jwk", "spki", or "pkcs8"
    {   //this is an example jwk key, other key types are Uint8Array objects
        kty: "EC",
        crv: "P-256",
        x: "zCQ5BPHPCLZYgdpo1n-x_90P2Ij52d53YVwTh3ZdiMo",
        y: "pDfQTUx0-OiZc5ZuKMcA7v2Q7ZPKsQwzB58bft0JTko",
        ext: true,
    },
    {   //these are the algorithm options
        name: "ECDSA",
        namedCurve: "P-256", //can be "P-256", "P-384", or "P-521"
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["verify"] //"verify" for public key import, "sign" for private key imports
)
.then(function(publicKey){
    //returns a publicKey (or privateKey if you are importing a private key)
    console.log(publicKey);
})
.catch(function(err){
    console.error(err);
});
```
###exportKey
```javascript
window.crypto.subtle.exportKey(
    "jwk", //can be "jwk", "spki", or "pkcs8"
    publicKey //can be a publicKey or privateKey, as long as extractable was true
)
.then(function(keydata){
    //returns the exported key data
    console.log(keydata);
})
.catch(function(err){
    console.error(err);
});
```
###sign
```javascript
window.crypto.subtle.sign(
    {
        name: "ECDSA",
        hash: {name: "SHA-256"}, //can be "SHA-1", "SHA-256", "SHA-384", or "SHA-512"
    },
    privateKey, //from generateKey or importKey above
    data //ArrayBuffer of data you want to sign
)
.then(function(signature){
    //returns an ArrayBuffer containing the signature
    console.log(new Uint8Array(signature));
})
.catch(function(err){
    console.error(err);
});
```
###verify
```javascript
window.crypto.subtle.verify(
    {
        name: "ECDSA",
        hash: {name: "SHA-256"}, //can be "SHA-1", "SHA-256", "SHA-384", or "SHA-512"
    },
    publicKey, //from generateKey or importKey above
    signature, //ArrayBuffer of the signature
    data //ArrayBuffer of the data
)
.then(function(isvalid){
    //returns a boolean on whether the signature is true or not
    console.log(isvalid);
})
.catch(function(err){
    console.error(err);
});
```

##ECDH
###generateKey
```javascript
window.crypto.subtle.generateKey(
    {
        name: "ECDH",
        namedCurve: "P-256", //can be "P-256", "P-384", or "P-521"
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["deriveKey", "deriveBits"] //can be any combination of "deriveKey" and "deriveBits"
)
.then(function(key){
    //returns a keypair object
    console.log(key);
    console.log(key.publicKey);
    console.log(key.privateKey);
})
.catch(function(err){
    console.error(err);
});
```
###importKey
```javascript
window.crypto.subtle.importKey(
    "jwk", //can be "jwk", "spki", "pkcs8", or "raw"
    {   //this is an example jwk key, other key types are Uint8Array objects
        kty: "EC",
        crv: "P-256",
        x: "zCQ5BPHPCLZYgdpo1n-x_90P2Ij52d53YVwTh3ZdiMo",
        y: "pDfQTUx0-OiZc5ZuKMcA7v2Q7ZPKsQwzB58bft0JTko",
        ext: true,
    },
    {   //these are the algorithm options
        name: "ECDH",
        namedCurve: "P-256", //can be "P-256", "P-384", or "P-521"
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["deriveKey", "deriveBits"] //can be any combination of "deriveKey" and "deriveBits"
)
.then(function(publicKey){
    //returns a publicKey (private keys cannot be imported)
    console.log(publicKey);
})
.catch(function(err){
    console.error(err);
});
```
###exportKey
```javascript
window.crypto.subtle.exportKey(
    "jwk", //can be "jwk", "spki", "pkcs8", or "raw"
    publicKey //public key (private keys cannot be exported)
)
.then(function(keydata){
    //returns the exported public key data
    console.log(keydata);
})
.catch(function(err){
    console.error(err);
});
```
###deriveKey
```javascript
window.crypto.subtle.deriveKey(
    {
        name: "ECDH",
        namedCurve: "P-256", //can be "P-256", "P-384", or "P-521"
        public: publicKey, //an ECDH public key from generateKey or importKey
    },
    privateKey, //your ECDH private key from generateKey or importKey
    { //the key type you want to create based on the derived bits
        name: "AES-CTR", //can be any AES algorithm ("AES-CTR", "AES-CBC", "AES-CMAC", "AES-GCM", "AES-CFB", "AES-KW", "ECDH", "DH", or "HMAC")
        //the generateKey parameters for that type of algorithm
        length: 256, //can be  128, 192, or 256
    },
    false, //whether the derived key is extractable (i.e. can be used in exportKey)
    ["encrypt", "decrypt"] //limited to the options in that algorithm's importKey
)
.then(function(keydata){
    //returns the exported key data
    console.log(keydata);
})
.catch(function(err){
    console.error(err);
});
```
###deriveBits
```javascript
window.crypto.subtle.deriveBits(
    {
        name: "ECDH",
        namedCurve: "P-256", //can be "P-256", "P-384", or "P-521"
        public: publicKey, //an ECDH public key from generateKey or importKey
    },
    privateKey, //your ECDH private key from generateKey or importKey
    256 //the number of bits you want to derive
)
.then(function(bits){
    //returns the derived bits as an ArrayBuffer
    console.log(new Uint8Array(bits));
})
.catch(function(err){
    console.error(err);
});
```

##AES-CTR
###generateKey
```javascript
window.crypto.subtle.generateKey(
    {
        name: "AES-CTR",
        length: 256, //can be  128, 192, or 256
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["encrypt", "decrypt"] //can be any combination of "encrypt" and "decrypt"
)
.then(function(key){
    //returns a key object
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
###importKey
```javascript
window.crypto.subtle.importKey(
    "jwk", //can be "jwk" or "raw"
    {   //this is an example jwk key, "raw" would be an ArrayBuffer
        kty: "oct",
        k: "Y0zt37HgOx-BY7SQjYVmrqhPkO44Ii2Jcb9yydUDPfE",
        alg: "A256CTR",
        ext: true,
    },
    {   //this is the algorithm options
        name: "AES-CTR",
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["encrypt", "decrypt"] //can be any combination of "encrypt" and "decrypt"
)
.then(function(key){
    //returns the symmetric key
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
###exportKey
```javascript
window.crypto.subtle.exportKey(
    "jwk", //can be "jwk" or "raw"
    key //extractable must be true
)
.then(function(keydata){
    //returns the exported key data
    console.log(keydata);
})
.catch(function(err){
    console.error(err);
});
```
###encrypt
```javascript
window.crypto.subtle.encrypt(
    {
        name: "AES-CTR",
        counter: window.crypto.getRandomValues(new Uint8Array(16)),
        length: 128, //NOTE: NOT SURE WHAT THIS SHOULD BE! PLEASE PULL REQUEST!
    },
    key, //from generateKey or importKey above
    data //ArrayBuffer of data you want to encrypt
)
.then(function(encrypted){
    //returns an ArrayBuffer containing the encrypted data
    console.log(new Uint8Array(encrypted));
})
.catch(function(err){
    console.error(err);
});
```
###decrypt
```javascript
window.crypto.subtle.decrypt(
    {
        name: "AES-CTR",
        counter: window.crypto.getRandomValues(new Uint8Array(16)),
        length: 128, //NOTE: NOT SURE WHAT THIS SHOULD BE! PLEASE PULL REQUEST!
    },
    key, //from generateKey or importKey above
    data //ArrayBuffer of the data
)
.then(function(decrypted){
    //returns an ArrayBuffer containing the decrypted data
    console.log(new Uint8Array(decrypted));
})
.catch(function(err){
    console.error(err);
});
```

##AES-CBC
###generateKey
```javascript
window.crypto.subtle.generateKey(
    {
        name: "AES-CBC",
        length: 256, //can be  128, 192, or 256
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["encrypt", "decrypt"] //can be any combination of "encrypt" and "decrypt"
)
.then(function(key){
    //returns a key object
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
###importKey
```javascript
window.crypto.subtle.importKey(
    "jwk", //can be "jwk" or "raw"
    {   //this is an example jwk key, "raw" would be an ArrayBuffer
        kty: "oct",
        k: "Y0zt37HgOx-BY7SQjYVmrqhPkO44Ii2Jcb9yydUDPfE",
        alg: "A256CBC",
        ext: true,
    },
    {   //this is the algorithm options
        name: "AES-CBC",
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["encrypt", "decrypt"] //can be any combination of "encrypt" and "decrypt"
)
.then(function(key){
    //returns the symmetric key
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
###exportKey
```javascript
window.crypto.subtle.exportKey(
    "jwk", //can be "jwk" or "raw"
    key //extractable must be true
)
.then(function(keydata){
    //returns the exported key data
    console.log(keydata);
})
.catch(function(err){
    console.error(err);
});
```
###encrypt
```javascript
window.crypto.subtle.encrypt(
    {
        name: "AES-CBC",
        //Don't re-use initialization vectors!
        //Always generate a new iv every time your encrypt!
        iv: window.crypto.getRandomValues(new Uint8Array(16)),
    },
    key, //from generateKey or importKey above
    data //ArrayBuffer of data you want to encrypt
)
.then(function(encrypted){
    //returns an ArrayBuffer containing the encrypted data
    console.log(new Uint8Array(encrypted));
})
.catch(function(err){
    console.error(err);
});
```
###decrypt
```javascript
window.crypto.subtle.decrypt(
    {
        name: "AES-CBC",
        iv: ArrayBuffer(16), //The initialization vector you used to encrypt
    },
    key, //from generateKey or importKey above
    data //ArrayBuffer of the data
)
.then(function(decrypted){
    //returns an ArrayBuffer containing the decrypted data
    console.log(new Uint8Array(decrypted));
})
.catch(function(err){
    console.error(err);
});
```

##AES-CMAC
###generateKey
```javascript
window.crypto.subtle.generateKey(
    {
        name: "AES-CMAC",
        length: 256, //can be  128, 192, or 256
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["sign", "verify"] //can be any combination of "sign" and "verify"
)
.then(function(key){
    //returns a key object
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
###importKey
```javascript
window.crypto.subtle.importKey(
    "jwk", //can be "jwk" or "raw"
    {   //this is an example jwk key, "raw" would be an ArrayBuffer
        kty: "oct",
        k: "Y0zt37HgOx-BY7SQjYVmrqhPkO44Ii2Jcb9yydUDPfE",
        alg: "A256CMAC",
        ext: true,
    },
    {   //this is the algorithm options
        name: "AES-CMAC",
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["sign", "verify"] //can be any combination of "sign" and "verify"
)
.then(function(key){
    //returns the symmetric key
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
###exportKey
```javascript
window.crypto.subtle.exportKey(
    "jwk", //can be "jwk" or "raw"
    key //extractable must be true
)
.then(function(keydata){
    //returns the exported key data
    console.log(keydata);
})
.catch(function(err){
    console.error(err);
});
```
###sign
```javascript
window.crypto.subtle.sign(
    {
        name: "AES-CMAC",
        length: 256, //bit length of the MAC
    },
    key, //from generateKey or importKey above
    data //ArrayBuffer of data you want to sign
)
.then(function(signature){
    //returns an ArrayBuffer containing the signature
    console.log(new Uint8Array(signature));
})
.catch(function(err){
    console.error(err);
});
```
###verify
```javascript
window.crypto.subtle.verify(
    {
        name: "AES-CMAC",
        length: 256, //bit length of the MAC
    },
    key, //from generateKey or importKey above
    signature, //ArrayBuffer of the signature
    data //ArrayBuffer of the data
)
.then(function(isvalid){
    //returns a boolean on whether the signature is true or not
    console.log(isvalid);
})
.catch(function(err){
    console.error(err);
});
```

##AES-GCM
###generateKey
```javascript
window.crypto.subtle.generateKey(
    {
        name: "AES-GCM",
        length: 256, //can be  128, 192, or 256
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["encrypt", "decrypt"] //can be any combination of "encrypt" and "decrypt"
)
.then(function(key){
    //returns a key object
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
###importKey
```javascript
window.crypto.subtle.importKey(
    "jwk", //can be "jwk" or "raw"
    {   //this is an example jwk key, "raw" would be an ArrayBuffer
        kty: "oct",
        k: "Y0zt37HgOx-BY7SQjYVmrqhPkO44Ii2Jcb9yydUDPfE",
        alg: "A256GCM",
        ext: true,
    },
    {   //this is the algorithm options
        name: "AES-GCM",
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["encrypt", "decrypt"] //can be any combination of "encrypt" and "decrypt"
)
.then(function(key){
    //returns the symmetric key
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
###exportKey
```javascript
window.crypto.subtle.exportKey(
    "jwk", //can be "jwk" or "raw"
    key //extractable must be true
)
.then(function(keydata){
    //returns the exported key data
    console.log(keydata);
})
.catch(function(err){
    console.error(err);
});
```
###encrypt
```javascript
window.crypto.subtle.encrypt(
    {
        name: "AES-GCM",

        //Don't re-use initialization vectors!
        //Always generate a new iv every time your encrypt!
        iv: window.crypto.getRandomValues(new Uint8Array(16)),

        //Additional authentication data (unsure what proper use for this is)
        additionalData: window.crypto.getRandomValues(new Uint8Array(256)),
        tagLength: 128,
        };
    },
    key, //from generateKey or importKey above
    data //ArrayBuffer of data you want to encrypt
)
.then(function(encrypted){
    //returns an ArrayBuffer containing the encrypted data
    console.log(new Uint8Array(encrypted));
})
.catch(function(err){
    console.error(err);
});
```
###decrypt
```javascript
window.crypto.subtle.decrypt(
    {
        name: "AES-GCM",
        iv: ArrayBuffer(16), //The initialization vector you used to encrypt
        additionalData: ArrayBuffer, //The addtionalData you used to encrypt
        tagLength: 128, //The tagLength you used to encrypt
    },
    key, //from generateKey or importKey above
    data //ArrayBuffer of the data
)
.then(function(decrypted){
    //returns an ArrayBuffer containing the decrypted data
    console.log(new Uint8Array(decrypted));
})
.catch(function(err){
    console.error(err);
});
```

##AES-CFB
###generateKey
```javascript
window.crypto.subtle.generateKey(
    {
        name: "AES-CFB-8",
        length: 256, //can be  128, 192, or 256
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["encrypt", "decrypt"] //can be any combination of "encrypt" and "decrypt"
)
.then(function(key){
    //returns a key object
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
###importKey
```javascript
window.crypto.subtle.importKey(
    "jwk", //can be "jwk" or "raw"
    {   //this is an example jwk key, "raw" would be an ArrayBuffer
        kty: "oct",
        k: "Y0zt37HgOx-BY7SQjYVmrqhPkO44Ii2Jcb9yydUDPfE",
        alg: "A256CFB8",
        ext: true,
    },
    {   //this is the algorithm options
        name: "AES-CFB-8",
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["encrypt", "decrypt"] //can be any combination of "encrypt" and "decrypt"
)
.then(function(key){
    //returns the symmetric key
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
###exportKey
```javascript
window.crypto.subtle.exportKey(
    "jwk", //can be "jwk" or "raw"
    key //extractable must be true
)
.then(function(keydata){
    //returns the exported key data
    console.log(keydata);
})
.catch(function(err){
    console.error(err);
});
```
###encrypt
```javascript
window.crypto.subtle.encrypt(
    {
        name: "AES-CFB-8",
        //Don't re-use initialization vectors!
        //Always generate a new iv every time your encrypt!
        iv: window.crypto.getRandomValues(new Uint8Array(16)),
    },
    key, //from generateKey or importKey above
    data //ArrayBuffer of data you want to encrypt
)
.then(function(encrypted){
    //returns an ArrayBuffer containing the encrypted data
    console.log(new Uint8Array(encrypted));
})
.catch(function(err){
    console.error(err);
});
```
###decrypt
```javascript
window.crypto.subtle.decrypt(
    {
        name: "AES-CFB-8",
        iv: ArrayBuffer(16), //The initialization vector you used to encrypt
    },
    key, //from generateKey or importKey above
    data //ArrayBuffer of the data
)
.then(function(decrypted){
    //returns an ArrayBuffer containing the decrypted data
    console.log(new Uint8Array(decrypted));
})
.catch(function(err){
    console.error(err);
});
```

##AES-KW
###generateKey
```javascript
window.crypto.subtle.generateKey(
    {
        name: "AES-KW",
        length: 256, //can be  128, 192, or 256
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["wrapKey", "unwrapKey"] //can be any combination of "wrapKey" and "unwrapKey"
)
.then(function(key){
    //returns a key object
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
###importKey
```javascript
window.crypto.subtle.importKey(
    "jwk", //can be "jwk" or "raw"
    {   //this is an example jwk key, "raw" would be an ArrayBuffer
        kty: "oct",
        k: "Y0zt37HgOx-BY7SQjYVmrqhPkO44Ii2Jcb9yydUDPfE",
        alg: "A256KW",
        ext: true,
    },
    {   //this is the algorithm options
        name: "AES-KW",
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["wrapKey", "unwrapKey"] //can be any combination of "wrapKey" and "unwrapKey"
)
.then(function(key){
    //returns the symmetric key
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
###exportKey
```javascript
window.crypto.subtle.exportKey(
    "jwk", //can be "jwk" or "raw"
    key //extractable must be true
)
.then(function(keydata){
    //returns the exported key data
    console.log(keydata);
})
.catch(function(err){
    console.error(err);
});
```

##HMAC
###generateKey
```javascript
window.crypto.subtle.generateKey(
    {
        name: "HMAC",
        hash: {name: "SHA-256"}, //can be "SHA-1", "SHA-256", "SHA-384", or "SHA-512"
        //length: 256, //optional, if you want your key length to differ from the hash length
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["sign", "verify"] //can be any combination of "sign" and "verify"
)
.then(function(key){
    //returns a key object
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
###importKey
```javascript
window.crypto.subtle.importKey(
    "jwk", //can be "jwk" or "raw"
    {   //this is an example jwk key, "raw" would be an ArrayBuffer
        kty: "oct",
        k: "Y0zt37HgOx-BY7SQjYVmrqhPkO44Ii2Jcb9yydUDPfE",
        alg: "HS256",
        ext: true,
    },
    {   //this is the algorithm options
        name: "HMAC",
        hash: {name: "SHA-256"}, //can be "SHA-1", "SHA-256", "SHA-384", or "SHA-512"
        //length: 256, //optional, if you want your key length to differ from the hash length
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["sign", "verify"] //can be any combination of "sign" and "verify"
)
.then(function(key){
    //returns the symmetric key
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
###exportKey
```javascript
window.crypto.subtle.exportKey(
    "jwk", //can be "jwk" or "raw"
    key //extractable must be true
)
.then(function(keydata){
    //returns the exported key data
    console.log(keydata);
})
.catch(function(err){
    console.error(err);
});
```
###sign
```javascript
window.crypto.subtle.sign(
    {
        name: "HMAC",
    },
    key, //from generateKey or importKey above
    data //ArrayBuffer of data you want to sign
)
.then(function(signature){
    //returns an ArrayBuffer containing the signature
    console.log(new Uint8Array(signature));
})
.catch(function(err){
    console.error(err);
});
```
###verify
```javascript
window.crypto.subtle.verify(
    {
        name: "HMAC",
    },
    key, //from generateKey or importKey above
    signature, //ArrayBuffer of the signature
    data //ArrayBuffer of the data
)
.then(function(isvalid){
    //returns a boolean on whether the signature is true or not
    console.log(isvalid);
})
.catch(function(err){
    console.error(err);
});
```

##DH
###generateKey
```javascript
window.crypto.subtle.generateKey(
    {
        name: "DH",
        //NOTE: THIS IS A SMALL PRIME FOR TESTING ONLY! DO NOT USE IT FOR REAL!
        //See http://datatracker.ietf.org/doc/rfc3526/ for better primes
        prime: new Uint8Array([
            255,255,255,255,255,255,255,255,201,15,218,162,33,104,194,52,196,198,98,139,
            128,220,28,209,41,2,78,8,138,103,204,116,2,11,190,166,59,19,155,34,81,74,8,
            121,142,52,4,221,239,149,25,179,205,58,67,27,48,43,10,109,242,95,20,55,79,225,
            53,109,109,81,194,69,228,133,181,118,98,94,126,198,244,76,66,233,166,55,237,
            107,11,255,92,182,244,6,183,237,238,56,107,251,90,137,159,165,174,159,36,17,
            124,75,31,230,73,40,102,81,236,228,91,61,194,0,124,184,161,99,191,5,152,218,
            72,54,28,85,211,154,105,22,63,168,253,36,207,95,131,101,93,35,220,163,173,
            150,28,98,243,86,32,133,82,187,158,213,41,7,112,150,150,109,103,12,53,78,74,
            188,152,4,241,116,108,8,202,35,115,39,255,255,255,255,255,255,255,255
        ]),
        generator: new Uint8Array([2]),
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["deriveKey", "deriveBits"] //can be any combination of "deriveKey" and "deriveBits"
)
.then(function(key){
    //returns a keypair object
    console.log(key);
    console.log(key.publicKey);
    console.log(key.privateKey);
})
.catch(function(err){
    console.error(err);
});
```
###importKey
```javascript
window.crypto.subtle.importKey(
    "raw", //can be "spki", "pkcs8", or "raw"
    new Uint8Array([ //this is an example raw key, "raw" would be an ArrayBuffer
        203,25,0,203,43,75,46,159,217,37,185,181,25,220,71,187,112,195,251,233,152,56,206,
        93,18,96,87,132,17,113,166,110,123,190,194,168,100,147,21,174,131,80,8,247,125,35,
        210,70,103,141,152,173,99,74,34,132,92,134,216,55,171,186,89,167,189,217,164,119,
        22,139,55,26,239,242,30,241,140,139,202,116,174,137,77,11,29,4,30,47,118,170,84,243,
        97,132,86,58,24,82,36,149,45,185,23,172,67,162,48,43,110,251,175,20,102,237,113,148,
        5,242,29,209,34,173,52,72,251,254,84,86,226,151,202,110,61,145,198,244,80,227,65,
        203,118,217,91,45,58,172,165,224,122,230,50,135,120,124,37,190,186,204,103,218,19,
        91,246,115,6,199,45,121,156,149,6,208,85,26,94,171,165,228,58,200,49,82,210,170,243,
        154,190,15,2,225,143,159
    ]),
    {   //these are the algorithm options
        name: "DH",
        //NOTE: THIS IS A SMALL PRIME FOR TESTING ONLY! DO NOT USE IT FOR REAL!
        //See http://datatracker.ietf.org/doc/rfc3526/ for better primes
        prime: new Uint8Array([
            255,255,255,255,255,255,255,255,201,15,218,162,33,104,194,52,196,198,98,139,
            128,220,28,209,41,2,78,8,138,103,204,116,2,11,190,166,59,19,155,34,81,74,8,
            121,142,52,4,221,239,149,25,179,205,58,67,27,48,43,10,109,242,95,20,55,79,225,
            53,109,109,81,194,69,228,133,181,118,98,94,126,198,244,76,66,233,166,55,237,
            107,11,255,92,182,244,6,183,237,238,56,107,251,90,137,159,165,174,159,36,17,
            124,75,31,230,73,40,102,81,236,228,91,61,194,0,124,184,161,99,191,5,152,218,
            72,54,28,85,211,154,105,22,63,168,253,36,207,95,131,101,93,35,220,163,173,
            150,28,98,243,86,32,133,82,187,158,213,41,7,112,150,150,109,103,12,53,78,74,
            188,152,4,241,116,108,8,202,35,115,39,255,255,255,255,255,255,255,255
        ]),
        generator: new Uint8Array([2]),
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["deriveKey", "deriveBits"] //can be any combination of "deriveKey" and "deriveBits"
)
.then(function(publicKey){
    //returns a publicKey (private keys cannot be imported)
    console.log(publicKey);
})
.catch(function(err){
    console.error(err);
});
```
###exportKey
```javascript
window.crypto.subtle.exportKey(
    "jwk", //can be "spki", "pkcs8", or "raw"
    publicKey //public key (private keys cannot be exported)
)
.then(function(keydata){
    //returns the exported public key data
    console.log(keydata);
})
.catch(function(err){
    console.error(err);
});
```
###deriveKey
```javascript
window.crypto.subtle.deriveKey(
    {
        name: "DH",
        //NOTE: THIS IS A SMALL PRIME FOR TESTING ONLY! DO NOT USE IT FOR REAL!
        //See http://datatracker.ietf.org/doc/rfc3526/ for better primes
        prime: new Uint8Array([
            255,255,255,255,255,255,255,255,201,15,218,162,33,104,194,52,196,198,98,139,
            128,220,28,209,41,2,78,8,138,103,204,116,2,11,190,166,59,19,155,34,81,74,8,
            121,142,52,4,221,239,149,25,179,205,58,67,27,48,43,10,109,242,95,20,55,79,225,
            53,109,109,81,194,69,228,133,181,118,98,94,126,198,244,76,66,233,166,55,237,
            107,11,255,92,182,244,6,183,237,238,56,107,251,90,137,159,165,174,159,36,17,
            124,75,31,230,73,40,102,81,236,228,91,61,194,0,124,184,161,99,191,5,152,218,
            72,54,28,85,211,154,105,22,63,168,253,36,207,95,131,101,93,35,220,163,173,
            150,28,98,243,86,32,133,82,187,158,213,41,7,112,150,150,109,103,12,53,78,74,
            188,152,4,241,116,108,8,202,35,115,39,255,255,255,255,255,255,255,255
        ]),
        generator: new Uint8Array([2]),
        public: publicKey, //a DH public key from generateKey or importKey
    },
    privateKey, //your DH private key from generateKey or importKey
    { //the key type you want to create based on the derived bits
        name: "AES-CTR", //can be any AES algorithm ("AES-CTR", "AES-CBC", "AES-CMAC", "AES-GCM", "AES-CFB", "AES-KW", "ECDH", "DH", or "HMAC")
        //the generateKey parameters for that type of algorithm
        length: 256, //can be  128, 192, or 256
    },
    false, //whether the derived key is extractable (i.e. can be used in exportKey)
    ["encrypt", "decrypt"] //limited to the options in that algorithm's importKey
)
.then(function(key){
    //returns the derived key
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
###deriveBits
```javascript
window.crypto.subtle.deriveBits(
    {
        name: "DH",
        //NOTE: THIS IS A SMALL PRIME FOR TESTING ONLY! DO NOT USE IT FOR REAL!
        //See http://datatracker.ietf.org/doc/rfc3526/ for better primes
        prime: new Uint8Array([
            255,255,255,255,255,255,255,255,201,15,218,162,33,104,194,52,196,198,98,139,
            128,220,28,209,41,2,78,8,138,103,204,116,2,11,190,166,59,19,155,34,81,74,8,
            121,142,52,4,221,239,149,25,179,205,58,67,27,48,43,10,109,242,95,20,55,79,225,
            53,109,109,81,194,69,228,133,181,118,98,94,126,198,244,76,66,233,166,55,237,
            107,11,255,92,182,244,6,183,237,238,56,107,251,90,137,159,165,174,159,36,17,
            124,75,31,230,73,40,102,81,236,228,91,61,194,0,124,184,161,99,191,5,152,218,
            72,54,28,85,211,154,105,22,63,168,253,36,207,95,131,101,93,35,220,163,173,
            150,28,98,243,86,32,133,82,187,158,213,41,7,112,150,150,109,103,12,53,78,74,
            188,152,4,241,116,108,8,202,35,115,39,255,255,255,255,255,255,255,255
        ]),
        generator: new Uint8Array([2]),
        public: publicKey, //a DH public key from generateKey or importKey
    },
    privateKey, //your DH private key from generateKey or importKey
    256 //the number of bits you want to derive
)
.then(function(bits){
    //returns the derived bits as an ArrayBuffer
    console.log(new Uint8Array(bits));
})
.catch(function(err){
    console.error(err);
});
```

##SHA-1
###digest
```javascript
window.crypto.subtle.digest(
    {
        name: "SHA-1",
    },
    new Uint8Array([1,2,3,4]) //The data you want to hash as an ArrayBuffer
)
.then(function(hash){
    //returns the hash as an ArrayBuffer
    console.log(new Uint8Array(hash));
})
.catch(function(err){
    console.error(err);
});
```

##SHA-256
###digest
```javascript
window.crypto.subtle.digest(
    {
        name: "SHA-256",
    },
    new Uint8Array([1,2,3,4]) //The data you want to hash as an ArrayBuffer
)
.then(function(hash){
    //returns the hash as an ArrayBuffer
    console.log(new Uint8Array(hash));
})
.catch(function(err){
    console.error(err);
});
```

##SHA-384
###digest
```javascript
window.crypto.subtle.digest(
    {
        name: "SHA-384",
    },
    new Uint8Array([1,2,3,4]) //The data you want to hash as an ArrayBuffer
)
.then(function(hash){
    //returns the hash as an ArrayBuffer
    console.log(new Uint8Array(hash));
})
.catch(function(err){
    console.error(err);
});
```

##SHA-512
###digest
```javascript
window.crypto.subtle.digest(
    {
        name: "SHA-512",
    },
    new Uint8Array([1,2,3,4]) //The data you want to hash as an ArrayBuffer
)
.then(function(hash){
    //returns the hash as an ArrayBuffer
    console.log(new Uint8Array(hash));
})
.catch(function(err){
    console.error(err);
});
```

##CONCAT
###importKey
```javascript
window.crypto.subtle.importKey(
    "raw", //only "raw" is allowed
    keydata, //your raw key data as an ArrayBuffer
    {
        name: "CONCAT",
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["deriveKey", "deriveBits"] //can be any combination of "deriveKey" and "deriveBits"
)
.then(function(key){
    //returns a key object
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
###deriveKey
```javascript
window.crypto.subtle.deriveKey(
    {
        "name": "CONCAT",
        algorithmId: ArrayBuffer, //?????? I don't know what this should be
        partyUInfo: ArrayBuffer, //?????? I don't know what this should be
        partyVInfo: ArrayBuffer, //?????? I don't know what this should be
        publicInfo: ArrayBuffer, //?????? I don't know what this should be
        privateInfo: ArrayBuffer, //?????? I don't know what this should be
        hash: {name: "SHA-1"}, //can be "SHA-1", "SHA-256", "SHA-384", or "SHA-512"
    },
    key, //your key from importKey
    { //the key type you want to create based on the derived bits
        name: "AES-CTR", //can be any AES algorithm ("AES-CTR", "AES-CBC", "AES-CMAC", "AES-GCM", "AES-CFB", "AES-KW", "ECDH", "DH", or "HMAC")
        //the generateKey parameters for that type of algorithm
        length: 256, //can be  128, 192, or 256
    },
    false, //whether the derived key is extractable (i.e. can be used in exportKey)
    ["encrypt", "decrypt"] //limited to the options in that algorithm's importKey
)
.then(function(key){
    //returns the derived key
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
###deriveBits
```javascript
window.crypto.subtle.deriveBits(
    {
        "name": "CONCAT",
        algorithmId: ArrayBuffer, //?????? I don't know what this should be
        partyUInfo: ArrayBuffer, //?????? I don't know what this should be
        partyVInfo: ArrayBuffer, //?????? I don't know what this should be
        publicInfo: ArrayBuffer, //?????? I don't know what this should be
        privateInfo: ArrayBuffer, //?????? I don't know what this should be
        hash: {name: "SHA-1"}, //can be "SHA-1", "SHA-256", "SHA-384", or "SHA-512"
    },
    key, //your key importKey
    256 //the number of bits you want to derive
)
.then(function(bits){
    //returns the derived bits as an ArrayBuffer
    console.log(new Uint8Array(bits));
})
.catch(function(err){
    console.error(err);
});
```

##HKDF-CTR
###importKey
```javascript
window.crypto.subtle.importKey(
    "raw", //only "raw" is allowed
    keydata, //your raw key data as an ArrayBuffer
    {
        name: "HKDF-CTR",
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["deriveKey", "deriveBits"] //can be any combination of "deriveKey" and "deriveBits"
)
.then(function(key){
    //returns a key object
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
###deriveKey
```javascript
window.crypto.subtle.deriveKey(
    {
        "name": "HKDF-CTR",
        label: ArrayBuffer, //?????? I don't know what this should be
        context: ArrayBuffer, //?????? I don't know what this should be
        hash: {name: "SHA-1"}, //can be "SHA-1", "SHA-256", "SHA-384", or "SHA-512"
    },
    key, //your key from importKey
    { //the key type you want to create based on the derived bits
        name: "AES-CTR", //can be any AES algorithm ("AES-CTR", "AES-CBC", "AES-CMAC", "AES-GCM", "AES-CFB", "AES-KW", "ECDH", "DH", or "HMAC")
        //the generateKey parameters for that type of algorithm
        length: 256, //can be  128, 192, or 256
    },
    false, //whether the derived key is extractable (i.e. can be used in exportKey)
    ["encrypt", "decrypt"] //limited to the options in that algorithm's importKey
)
.then(function(key){
    //returns the derived key
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
###deriveBits
```javascript
window.crypto.subtle.deriveBits(
    {
        "name": "HKDF-CTR",
        label: ArrayBuffer, //?????? I don't know what this should be
        context: ArrayBuffer, //?????? I don't know what this should be
        hash: {name: "SHA-1"}, //can be "SHA-1", "SHA-256", "SHA-384", or "SHA-512"
    },
    key, //your key importKey
    256 //the number of bits you want to derive
)
.then(function(bits){
    //returns the derived bits as an ArrayBuffer
    console.log(new Uint8Array(bits));
})
.catch(function(err){
    console.error(err);
});
```

##PBKDF2
###generateKey
```javascript
//NOTE: This prompts the user to enter a password.
window.crypto.subtle.generateKey(
    {
        name: "PBKDF2",
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["deriveKey", "deriveBits"] //can be any combination of "deriveKey" and "deriveBits"
)
.then(function(key){
    //returns a key object
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
###importKey
```javascript
window.crypto.subtle.importKey(
    "raw", //only "raw" is allowed
    window.crypto.getRandomValues(new Uint8Array(16)), //your password
    {
        name: "PBKDF2",
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["deriveKey", "deriveBits"] //can be any combination of "deriveKey" and "deriveBits"
)
.then(function(key){
    //returns a key object
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
###deriveKey
```javascript
window.crypto.subtle.deriveKey(
    {
        "name": "PBKDF2",
        salt: window.crypto.getRandomValues(new Uint8Array(16)),
        iterations: 1000,
        hash: {name: "SHA-1"}, //can be "SHA-1", "SHA-256", "SHA-384", or "SHA-512"
    },
    key, //your key from generateKey or importKey
    { //the key type you want to create based on the derived bits
        name: "AES-CTR", //can be any AES algorithm ("AES-CTR", "AES-CBC", "AES-CMAC", "AES-GCM", "AES-CFB", "AES-KW", "ECDH", "DH", or "HMAC")
        //the generateKey parameters for that type of algorithm
        length: 256, //can be  128, 192, or 256
    },
    false, //whether the derived key is extractable (i.e. can be used in exportKey)
    ["encrypt", "decrypt"] //limited to the options in that algorithm's importKey
)
.then(function(key){
    //returns the derived key
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
###deriveBits
```javascript
window.crypto.subtle.deriveBits(
    {
        "name": "PBKDF2",
        salt: window.crypto.getRandomValues(new Uint8Array(16)),
        iterations: 1000,
        hash: {name: "SHA-1"}, //can be "SHA-1", "SHA-256", "SHA-384", or "SHA-512"
    },
    key, //your key from generateKey or importKey
    256 //the number of bits you want to derive
)
.then(function(bits){
    //returns the derived bits as an ArrayBuffer
    console.log(new Uint8Array(bits));
})
.catch(function(err){
    console.error(err);
});
```





