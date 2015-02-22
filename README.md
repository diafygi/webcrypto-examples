# Web Cryptography API Live Chart

Live Chart: https://diafygi.github.io/webcrypto-live-chart

I couldn't find anywhere that clear had examples of using WebCrytoAPI, so I
wrote examples and made a live chart with them. You can see the examples below
and see the live chart that checks which parts of WebCryptoAPI your browser
supports. Pull requests welcome!

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
    * [exportKey](#exportkey-13)
    * [deriveBits](#derivebits-2)
    * [deriveKey](#derivekey-2)
19. [HKDF-CTR](#hkdf-ctr)
    * [importKey](#importkey-14)
    * [exportKey](#exportkey-14)
    * [deriveBits](#derivebits-3)
    * [deriveKey](#derivekey-3)
20. [PBKDF2](#pbkdf2)
    * [generateKey](#generatekey-13)
    * [importKey](#importkey-15)
    * [exportKey](#exportkey-15)
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
    {   //this is an example jwk key, other key types like "spki" are Uint8Array objects
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
.then(function(data){
    //returns the exported key data
    console.log(data);
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
    privateKey,
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
    publicKey,
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
###importKey
###exportKey
###sign
###verify

##RSA-OAEP
###generateKey
###importKey
###exportKey
###encrypt
###decrypt

##ECDSA
###generateKey
###importKey
###exportKey
###sign
###verify

##ECDH
###generateKey
###importKey
###exportKey
###deriveKey
###deriveBits

##AES-CTR
###generateKey
###importKey
###exportKey
###encrypt
###decrypt

##AES-CBC
###generateKey
###importKey
###exportKey
###encrypt
###decrypt

##AES-CMAC
###generateKey
###importKey
###exportKey
###sign
###verify

##AES-GCM
###generateKey
###importKey
###exportKey
###encrypt
###decrypt

##AES-CFB
###generateKey
###importKey
###exportKey
###encrypt
###decrypt

##AES-KW
###generateKey
###importKey
###exportKey

##HMAC
###generateKey
###importKey
###exportKey
###sign
###verify

##DH
###generateKey
###importKey
###exportKey
###deriveKey
###deriveBits

##SHA-1
###digest

##SHA-256
###digest

##SHA-384
###digest

##SHA-512
###digest

##CONCAT
###importKey
###exportKey
###deriveKey
###deriveBits

##HKDF-CTR
###importKey
###exportKey
###deriveKey
###deriveBits

##PBKDF2
###generateKey
###importKey
###exportKey
###deriveKey
###deriveBits





