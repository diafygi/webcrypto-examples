# Web Cryptography API Examples

Live Table: https://diafygi.github.io/webcrypto-examples/

I couldn't find anywhere that had clear examples of WebCrytoAPI, so I
wrote examples and made a live table with them. Pull requests welcome!

1. [RSASSA-PKCS1-v1_5](#rsassa-pkcs1-v1_5)
  * [generateKey](#rsassa-pkcs1-v1_5---generatekey) | 
[importKey](#rsassa-pkcs1-v1_5---importkey) | 
[exportKey](#rsassa-pkcs1-v1_5---exportkey) | 
[sign](#rsassa-pkcs1-v1_5---sign) | 
[verify](#rsassa-pkcs1-v1_5---verify)

2. [RSA-PSS](#rsa-pss)
  * [generateKey](#rsa-pss---generatekey) | 
[importKey](#rsa-pss---importkey) | 
[exportKey](#rsa-pss---exportkey) | 
[sign](#rsa-pss---sign) | 
[verify](#rsa-pss---verify)

3. [RSA-OAEP](#rsa-oaep)
  * [generateKey](#rsa-oaep---generatekey) | 
[importKey](#rsa-oaep---importkey) | 
[exportKey](#rsa-oaep---exportkey) | 
[encrypt](#rsa-oaep---encrypt) | 
[decrypt](#rsa-oaep---decrypt) |
[wrapKey](#rsa-oaep---wrapkey) |
[unwrapKey](#rsa-oaep---unwrapkey)

4. [ECDSA](#ecdsa)
  * [generateKey](#ecdsa---generatekey) | 
[importKey](#ecdsa---importkey) | 
[exportKey](#ecdsa---exportkey) | 
[sign](#ecdsa---sign) | 
[verify](#ecdsa---verify)

5. [ECDH](#ecdh)
  * [generateKey](#ecdh---generatekey) | 
[importKey](#ecdh---importkey) | 
[exportKey](#ecdh---exportkey) | 
[deriveKey](#ecdh---derivekey) | 
[deriveBits](#ecdh---derivebits)

6. [AES-CTR](#aes-ctr)
  * [generateKey](#aes-ctr---generatekey) | 
[importKey](#aes-ctr---importkey) | 
[exportKey](#aes-ctr---exportkey) | 
[encrypt](#aes-ctr---encrypt) | 
[decrypt](#aes-ctr---decrypt) |
[wrapKey](#aes-ctr---wrapkey) |
[unwrapKey](#aes-ctr---unwrapkey)

7. [AES-CBC](#aes-cbc)
  * [generateKey](#aes-cbc---generatekey) | 
[importKey](#aes-cbc---importkey) | 
[exportKey](#aes-cbc---exportkey) | 
[encrypt](#aes-cbc---encrypt) | 
[decrypt](#aes-cbc---decrypt) |
[wrapKey](#aes-cbc---wrapkey) |
[unwrapKey](#aes-cbc---unwrapkey)

8. [AES-CMAC](#aes-cmac)
  * [generateKey](#aes-cmac---generatekey) | 
[importKey](#aes-cmac---importkey) | 
[exportKey](#aes-cmac---exportkey) | 
[sign](#aes-cmac---sign) | 
[verify](#aes-cmac---verify)

9. [AES-GCM](#aes-gcm)
  * [generateKey](#aes-gcm---generatekey) | 
[importKey](#aes-gcm---importkey) | 
[exportKey](#aes-gcm---exportkey) | 
[encrypt](#aes-gcm---encrypt) | 
[decrypt](#aes-gcm---decrypt) |
[wrapKey](#aes-gcm---wrapkey) |
[unwrapKey](#aes-gcm---unwrapkey)

10. [AES-CFB](#aes-cfb)
  * [generateKey](#aes-cfb---generatekey) | 
[importKey](#aes-cfb---importkey) | 
[exportKey](#aes-cfb---exportkey) | 
[encrypt](#aes-cfb---encrypt) | 
[decrypt](#aes-cfb---decrypt) |
[wrapKey](#aes-cfb---wrapkey) |
[unwrapKey](#aes-cfb---unwrapkey)

11. [AES-KW](#aes-kw)
  * [generateKey](#aes-kw---generatekey) | 
[importKey](#aes-kw---importkey) | 
[exportKey](#aes-kw---exportkey) |
[wrapKey](#aes-kw---wrapkey) |
[unwrapKey](#aes-kw---unwrapkey)

12. [HMAC](#hmac)
  * [generateKey](#hmac---generatekey) | 
[importKey](#hmac---importkey) | 
[exportKey](#hmac---exportkey) | 
[sign](#hmac---sign) | 
[verify](#hmac-verify)

13. [DH](#dh)
  * [generateKey](#dh---generatekey) | 
[importKey](#dh---importkey) | 
[exportKey](#dh---exportkey) | 
[deriveKey](#dh---derivekey) | 
[deriveBits](#dh---derivebits)

14. [SHA](#sha-1)
  * [SHA-1 digest](#sha-1---digest) | 
[SHA-256 digest](#sha-256---digest) | 
[SHA-384 digest](#sha-384---digest) | 
[SHA-512 digest](#sha-512---digest)

18. [CONCAT](#concat)
  * [importKey](#concat---importkey) | 
[deriveKey](#concat---derivekey) | 
[deriveBits](#concat---derivebits)

19. [HKDF-CTR](#hkdf-ctr)
  * [importKey](#hkdf-ctr---importkey) | 
[deriveKey](#hkdf-ctr---derivekey) | 
[deriveBits](#hkdf-ctr---derivebits)

20. [PBKDF2](#pbkdf2)
  * [generateKey](#pbkdf2---generatekey) | 
[importKey](#pbkdf2---importkey) | 
[deriveKey](#pbkdf2---derivekey) | 
[deriveBits](#pbkdf2---derivebits)

##RSASSA-PKCS1-v1_5
####RSASSA-PKCS1-v1_5 - generateKey
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
####RSASSA-PKCS1-v1_5 - importKey
```javascript
window.crypto.subtle.importKey(
    "jwk", //can be "jwk" (public or private), "spki" (public only), or "pkcs8" (private only)
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
####RSASSA-PKCS1-v1_5 - exportKey
```javascript
window.crypto.subtle.exportKey(
    "jwk", //can be "jwk" (public or private), "spki" (public only), or "pkcs8" (private only)
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
####RSASSA-PKCS1-v1_5 - sign
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
####RSASSA-PKCS1-v1_5 - verify
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
####RSA-PSS - generateKey
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
####RSA-PSS - importKey
```javascript
window.crypto.subtle.importKey(
    "jwk", //can be "jwk" (public or private), "spki" (public only), or "pkcs8" (private only)
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
####RSA-PSS - exportKey
```javascript
window.crypto.subtle.exportKey(
    "jwk", //can be "jwk" (public or private), "spki" (public only), or "pkcs8" (private only)
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
####RSA-PSS - sign
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
####RSA-PSS - verify
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
####RSA-OAEP - generateKey
```javascript
window.crypto.subtle.generateKey(
    {
        name: "RSA-OAEP",
        modulusLength: 2048, //can be 1024, 2048, or 4096
        publicExponent: new Uint8Array([0x01, 0x00, 0x01]),
        hash: {name: "SHA-256"}, //can be "SHA-1", "SHA-256", "SHA-384", or "SHA-512"
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["encrypt", "decrypt"] //must be ["encrypt", "decrypt"] or ["wrapKey", "unwrapKey"]
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
####RSA-OAEP - importKey
```javascript
window.crypto.subtle.importKey(
    "jwk", //can be "jwk" (public or private), "spki" (public only), or "pkcs8" (private only)
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
    ["encrypt"] //"encrypt" or "wrapKey" for public key import or
                //"decrypt" or "unwrapKey" for private key imports
)
.then(function(publicKey){
    //returns a publicKey (or privateKey if you are importing a private key)
    console.log(publicKey);
})
.catch(function(err){
    console.error(err);
});
```
####RSA-OAEP - exportKey
```javascript
window.crypto.subtle.exportKey(
    "jwk", //can be "jwk" (public or private), "spki" (public only), or "pkcs8" (private only)
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
####RSA-OAEP - encrypt
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
####RSA-OAEP - decrypt
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
####RSA-OAEP - wrapKey
```javascript
window.crypto.subtle.wrapKey(
    "raw", //the export format, must be "raw" (only available sometimes)
    key, //the key you want to wrap, must be able to fit in RSA-OAEP padding
    publicKey, //the public key with "wrapKey" usage flag
    {   //these are the wrapping key's algorithm options
        name: "RSA-OAEP",
        hash: {name: "SHA-256"},
    }
)
.then(function(wrapped){
    //returns an ArrayBuffer containing the encrypted data
    console.log(new Uint8Array(wrapped));
})
.catch(function(err){
    console.error(err);
});
```
####RSA-OAEP - unwrapKey
```javascript
window.crypto.subtle.unwrapKey(
    "raw", //the import format, must be "raw" (only available sometimes)
    wrapped, //the key you want to unwrap
    privateKey, //the private key with "unwrapKey" usage flag
    {   //these are the wrapping key's algorithm options
        name: "RSA-OAEP",
        modulusLength: 2048,
        publicExponent: new Uint8Array([0x01, 0x00, 0x01]),
        hash: {name: "SHA-256"},
    },
    {   //this what you want the wrapped key to become (same as when wrapping)
        name: "AES-GCM",
        length: 256
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["encrypt", "decrypt"] //the usages you want the unwrapped key to have
)
.then(function(key){
    //returns a key object
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```

##ECDSA
####ECDSA - generateKey
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
####ECDSA - importKey
```javascript
window.crypto.subtle.importKey(
    "jwk", //can be "jwk" (public or private), "spki" (public only), or "pkcs8" (private only)
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
####ECDSA - exportKey
```javascript
window.crypto.subtle.exportKey(
    "jwk", //can be "jwk" (public or private), "spki" (public only), or "pkcs8" (private only)
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
####ECDSA - sign
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
####ECDSA - verify
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
####ECDH - generateKey
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
####ECDH - importKey
```javascript
window.crypto.subtle.importKey(
    "jwk", //can be "jwk" (public or private), "raw" (public only), "spki" (public only), or "pkcs8" (private only)
    {   //this is an example jwk key, other key types are Uint8Array objects
        kty: "EC",
        crv: "P-256",
        x: "kgR_PqO07L8sZOBbw6rvv7O_f7clqDeiE3WnMkb5EoI",
        y: "djI-XqCqSyO9GFk_QT_stROMCAROIvU8KOORBgQUemE",
        d: "5aPFSt0UFVXYGu-ZKyC9FQIUOAMmnjzdIwkxCMe3Iok",
        ext: true,
    },
    {   //these are the algorithm options
        name: "ECDH",
        namedCurve: "P-256", //can be "P-256", "P-384", or "P-521"
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["deriveKey", "deriveBits"] //"deriveKey" and/or "deriveBits" for private keys only (just put an empty list if importing a public key)
)
.then(function(privateKey){
    //returns a privateKey (or publicKey if you are importing a public key)
    console.log(privateKey);
})
.catch(function(err){
    console.error(err);
});
```
####ECDH - exportKey
```javascript
window.crypto.subtle.exportKey(
    "jwk", //can be "jwk" (public or private), "raw" (public only), "spki" (public only), or "pkcs8" (private only)
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
####ECDH - deriveKey
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
####ECDH - deriveBits
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
####AES-CTR - generateKey
```javascript
window.crypto.subtle.generateKey(
    {
        name: "AES-CTR",
        length: 256, //can be  128, 192, or 256
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["encrypt", "decrypt"] //can "encrypt", "decrypt", "wrapKey", or "unwrapKey"
)
.then(function(key){
    //returns a key object
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
####AES-CTR - importKey
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
    ["encrypt", "decrypt"] //can "encrypt", "decrypt", "wrapKey", or "unwrapKey"
)
.then(function(key){
    //returns the symmetric key
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
####AES-CTR - exportKey
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
####AES-CTR - encrypt
```javascript
window.crypto.subtle.encrypt(
    {
        name: "AES-CTR",
        //Don't re-use counters!
        //Always use a new counter every time your encrypt!
        counter: new Uint8Array(16),
        length: 128, //can be 1-128
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
####AES-CTR - decrypt
```javascript
window.crypto.subtle.decrypt(
    {
        name: "AES-CTR",
        counter: ArrayBuffer(16), //The same counter you used to encrypt
        length: 128, //The same length you used to encrypt
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
####AES-CTR - wrapKey
```javascript
window.crypto.subtle.wrapKey(
    "jwk", //can be "jwk", "raw", "spki", or "pkcs8"
    key, //the key you want to wrap, must be able to export to "raw" format
    wrappingKey, //the AES-CTR key with "wrapKey" usage flag
    {   //these are the wrapping key's algorithm options
        name: "AES-CTR",
        //Don't re-use counters!
        //Always use a new counter every time your encrypt!
        counter: new Uint8Array(16),
        length: 128, //can be 1-128
    }
)
.then(function(wrapped){
    //returns an ArrayBuffer containing the encrypted data
    console.log(new Uint8Array(wrapped));
})
.catch(function(err){
    console.error(err);
});
```
####AES-CTR - unwrapKey
```javascript
window.crypto.subtle.unwrapKey(
    "jwk", //"jwk", "raw", "spki", or "pkcs8" (whatever was used in wrapping)
    wrapped, //the key you want to unwrap
    wrappingKey, //the AES-CTR key with "unwrapKey" usage flag
    {   //these are the wrapping key's algorithm options
        name: "AES-CTR",
        //Don't re-use counters!
        //Always use a new counter every time your encrypt!
        counter: new Uint8Array(16),
        length: 128, //can be 1-128
    },
    {   //this what you want the wrapped key to become (same as when wrapping)
        name: "AES-GCM",
        length: 256
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["encrypt", "decrypt"] //the usages you want the unwrapped key to have
)
.then(function(key){
    //returns a key object
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```

##AES-CBC
####AES-CBC - generateKey
```javascript
window.crypto.subtle.generateKey(
    {
        name: "AES-CBC",
        length: 256, //can be  128, 192, or 256
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["encrypt", "decrypt"] //can be "encrypt", "decrypt", "wrapKey", or "unwrapKey"
)
.then(function(key){
    //returns a key object
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
####AES-CBC - importKey
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
    ["encrypt", "decrypt"] //can be "encrypt", "decrypt", "wrapKey", or "unwrapKey"
)
.then(function(key){
    //returns the symmetric key
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
####AES-CBC - exportKey
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
####AES-CBC - encrypt
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
####AES-CBC - decrypt
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
####AES-CBC - wrapKey
```javascript
window.crypto.subtle.wrapKey(
    "jwk", //can be "jwk", "raw", "spki", or "pkcs8"
    key, //the key you want to wrap, must be able to export to above format
    wrappingKey, //the AES-CBC key with "wrapKey" usage flag
    {   //these are the wrapping key's algorithm options
        name: "AES-CBC",
        //Don't re-use initialization vectors!
        //Always generate a new iv every time your encrypt!
        iv: window.crypto.getRandomValues(new Uint8Array(16)),
    }
)
.then(function(wrapped){
    //returns an ArrayBuffer containing the encrypted data
    console.log(new Uint8Array(wrapped));
})
.catch(function(err){
    console.error(err);
});
```
####AES-CBC - unwrapKey
```javascript
window.crypto.subtle.unwrapKey(
    "jwk", //"jwk", "raw", "spki", or "pkcs8" (whatever was used in wrapping)
    wrapped, //the key you want to unwrap
    wrappingKey, //the AES-CBC key with "unwrapKey" usage flag
    {   //these are the wrapping key's algorithm options
        name: "AES-CBC",
        iv: ArrayBuffer(16), //The initialization vector you used to encrypt
    },
    {   //this what you want the wrapped key to become (same as when wrapping)
        name: "AES-GCM",
        length: 256
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["encrypt", "decrypt"] //the usages you want the unwrapped key to have
)
.then(function(key){
    //returns a key object
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```

##AES-CMAC
####AES-CMAC - generateKey
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
####AES-CMAC - importKey
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
####AES-CMAC - exportKey
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
####AES-CMAC - sign
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
####AES-CMAC - verify
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
####AES-GCM - generateKey
```javascript
window.crypto.subtle.generateKey(
    {
        name: "AES-GCM",
        length: 256, //can be  128, 192, or 256
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["encrypt", "decrypt"] //can "encrypt", "decrypt", "wrapKey", or "unwrapKey"
)
.then(function(key){
    //returns a key object
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
####AES-GCM - importKey
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
    ["encrypt", "decrypt"] //can "encrypt", "decrypt", "wrapKey", or "unwrapKey"
)
.then(function(key){
    //returns the symmetric key
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
####AES-GCM - exportKey
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
####AES-GCM - encrypt
```javascript
window.crypto.subtle.encrypt(
    {
        name: "AES-GCM",

        //Don't re-use initialization vectors!
        //Always generate a new iv every time your encrypt!
        //Recommended to use 12 bytes length
        iv: window.crypto.getRandomValues(new Uint8Array(12)),

        //Additional authentication data (optional)
        additionalData: ArrayBuffer,

        //Tag length (optional)
        tagLength: 128, //can be 32, 64, 96, 104, 112, 120 or 128 (default)
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
####AES-GCM - decrypt
```javascript
window.crypto.subtle.decrypt(
    {
        name: "AES-GCM",
        iv: ArrayBuffer(12), //The initialization vector you used to encrypt
        additionalData: ArrayBuffer, //The addtionalData you used to encrypt (if any)
        tagLength: 128, //The tagLength you used to encrypt (if any)
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
####AES-GCM - wrapKey
```javascript
window.crypto.subtle.wrapKey(
    "jwk", //can be "jwk", "raw", "spki", or "pkcs8"
    key, //the key you want to wrap, must be able to export to above format
    wrappingKey, //the AES-GCM key with "wrapKey" usage flag
    {   //these are the wrapping key's algorithm options
        name: "AES-GCM",

        //Don't re-use initialization vectors!
        //Always generate a new iv every time your encrypt!
        //Recommended to use 12 bytes length
        iv: window.crypto.getRandomValues(new Uint8Array(12)),

        //Additional authentication data (optional)
        additionalData: ArrayBuffer,

        //Tag length (optional)
        tagLength: 128, //can be 32, 64, 96, 104, 112, 120 or 128 (default)
    }
)
.then(function(wrapped){
    //returns an ArrayBuffer containing the encrypted data
    console.log(new Uint8Array(wrapped));
})
.catch(function(err){
    console.error(err);
});
```
####AES-GCM - unwrapKey
```javascript
window.crypto.subtle.unwrapKey(
    "jwk", //"jwk", "raw", "spki", or "pkcs8" (whatever was used in wrapping)
    wrapped, //the key you want to unwrap
    wrappingKey, //the AES-GCM key with "unwrapKey" usage flag
    {   //these are the wrapping key's algorithm options
        name: "AES-GCM",
        iv: ArrayBuffer(12), //The initialization vector you used to encrypt
        additionalData: ArrayBuffer, //The addtionalData you used to encrypt (if any)
        tagLength: 128, //The tagLength you used to encrypt (if any)
    },
    {   //this what you want the wrapped key to become (same as when wrapping)
        name: "AES-CBC",
        length: 256
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["encrypt", "decrypt"] //the usages you want the unwrapped key to have
)
.then(function(key){
    //returns a key object
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```

##AES-CFB
####AES-CFB - generateKey
```javascript
window.crypto.subtle.generateKey(
    {
        name: "AES-CFB-8",
        length: 256, //can be  128, 192, or 256
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["encrypt", "decrypt"] //can "encrypt", "decrypt", "wrapKey", or "unwrapKey"
)
.then(function(key){
    //returns a key object
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
####AES-CFB - importKey
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
    ["encrypt", "decrypt"] //can "encrypt", "decrypt", "wrapKey", or "unwrapKey"
)
.then(function(key){
    //returns the symmetric key
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```
####AES-CFB - exportKey
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
####AES-CFB - encrypt
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
####AES-CFB - decrypt
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
####AES-CFB - wrapKey
```javascript
window.crypto.subtle.wrapKey(
    "jwk", //can be "jwk", "raw", "spki", or "pkcs8"
    key, //the key you want to wrap, must be able to export to above format
    wrappingKey, //the AES-CFB key with "wrapKey" usage flag
    {   //these are the wrapping key's algorithm options
        name: "AES-CFB",
        //Don't re-use initialization vectors!
        //Always generate a new iv every time your encrypt!
        iv: window.crypto.getRandomValues(new Uint8Array(16)),
    }
)
.then(function(wrapped){
    //returns an ArrayBuffer containing the encrypted data
    console.log(new Uint8Array(wrapped));
})
.catch(function(err){
    console.error(err);
});
```
####AES-CFB - unwrapKey
```javascript
window.crypto.subtle.unwrapKey(
    "jwk", //"jwk", "raw", "spki", or "pkcs8" (whatever was used in wrapping)
    wrapped, //the key you want to unwrap
    wrappingKey, //the AES-CFB key with "unwrapKey" usage flag
    {   //these are the wrapping key's algorithm options
        name: "AES-CFB",
        iv: ArrayBuffer(16), //The initialization vector you used to encrypt
    },
    {   //this what you want the wrapped key to become (same as when wrapping)
        name: "AES-GCM",
        length: 256
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["encrypt", "decrypt"] //the usages you want the unwrapped key to have
)
.then(function(key){
    //returns a key object
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```

##AES-KW
####AES-KW - generateKey
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
####AES-KW - importKey
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
####AES-KW - exportKey
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
####AES-KW - wrapKey
```javascript
window.crypto.subtle.wrapKey(
    "raw", //the export format, must be "raw" (only available sometimes)
    key, //the key you want to wrap, must export in 8 byte increments
    wrappingKey, //the AES-KW key with "wrapKey" usage flag
    {   //these are the wrapping key's algorithm options
        name: "AES-KW",
    }
)
.then(function(wrapped){
    //returns an ArrayBuffer containing the encrypted data
    console.log(new Uint8Array(wrapped));
})
.catch(function(err){
    console.error(err);
});
```
####AES-KW - unwrapKey
```javascript
window.crypto.subtle.unwrapKey(
    "raw", //the import format, must be "raw" (only available sometimes)
    wrapped, //the key you want to unwrap
    wrappingKey, //the AES-KW key with "unwrapKey" usage flag
    {   //these are the wrapping key's algorithm options
        name: "AES-KW",
    },
    {   //this what you want the wrapped key to become (same as when wrapping)
        name: "AES-GCM",
        length: 256
    },
    false, //whether the key is extractable (i.e. can be used in exportKey)
    ["encrypt", "decrypt"] //the usages you want the unwrapped key to have
)
.then(function(key){
    //returns a key object
    console.log(key);
})
.catch(function(err){
    console.error(err);
});
```

##HMAC
####HMAC - generateKey
```javascript
window.crypto.subtle.generateKey(
    {
        name: "HMAC",
        hash: {name: "SHA-256"}, //can be "SHA-1", "SHA-256", "SHA-384", or "SHA-512"
        //length: 256, //optional, if you want your key length to differ from the hash function's block length
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
####HMAC - importKey
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
        //length: 256, //optional, if you want your key length to differ from the hash function's block length
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
####HMAC - exportKey
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
####HMAC - sign
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
####HMAC - verify
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
####DH - generateKey
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
####DH - importKey
```javascript
window.crypto.subtle.importKey(
    "raw", //can be "raw" (public only), "spki" (public only), or "pkcs8" (private only)
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
    [] //use ["deriveKey", "deriveBits"] if importing a private key
)
.then(function(publicKey){
    //returns a publicKey (or privateKey if you are importing a private key)
    console.log(publicKey);
})
.catch(function(err){
    console.error(err);
});
```
####DH - exportKey
```javascript
window.crypto.subtle.exportKey(
    "jwk", //can be "raw" (public or private), "spki" (public only), or "pkcs8" (private only)
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
####DH - deriveKey
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
####DH - deriveBits
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

##SHA
####SHA-1 - digest
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

####SHA-256 - digest
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

####SHA-384 - digest
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

####SHA-512 - digest
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
####CONCAT - importKey
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
####CONCAT - deriveKey
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
####CONCAT - deriveBits
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
####HKDF-CTR - importKey
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
####HKDF-CTR - deriveKey
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
####HKDF-CTR - deriveBits
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
####PBKDF2 - generateKey
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
####PBKDF2 - importKey
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
####PBKDF2 - deriveKey
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
####PBKDF2 - deriveBits
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

