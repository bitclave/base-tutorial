# Base Platform Tutorial

This reference application demonstrates how to use BASE API using [BASE JS LIBRARY](https://github.com/bitclave/base-client-js). 

The application lets user to choose a passphrase to create his private & public key pair and use private key to encrypt his data and save to BASE. Saved user retrieve his data any time and decrypt it using his private key. Either passphrase or private key is never sent to BASE platform.

# How to use Base Platform
1) Initialise Base
```
const base = new Base("https://base-node-staging.herokuapp.com", 'localhost', '', '');    
```

2) Choose a passphrase and crate a keypair
```
base.createKeyPairHelper('').createKeyPair("some passphrase").then(keyPair => {
    console.log("PublicKey:" + keyPair.publicKey);
    console.log("PrivateKey:" + keyPair.privateKey);     
});
```

3) Create account or check for existence
```
let account;
try {
    account = await base.accountManager.checkAccount(passphrase, "somemessage");
} catch(e) {
    account = await base.accountManager.registration(passphrase, "somemessage");
}
```

4) Save & Retrieve your data
```
//Save
let data = new Map();
data.set("email", "im@host.com");
let encryptedData = await base.profileManager.updateData(data);

//Read
let decryptedData = await base.profileManager.getData();
console.log(decryptedData.get("email"));
```

# Steps to run this tutorial

```
$ node --version
v8.11.2
$ npm --version
6.1.0

$ npm i
$ npm run start
```