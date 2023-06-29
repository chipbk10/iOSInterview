# Security

## How Apple handles secure data storing?

### Apple App Sandbox

- Each app runs in its own sandbox, and the app can only use the data stored in its sandbox
- If your app wants to access to the photos, or iCloud, the app has to use the services that OS provides

### Data Protection API

- Apple introduces several protection levels when we want to create data and store in a secured way on the device
- For example, the data is decrypted only until you unlock the device and starts using the app

### Keychain

- Data is encrypted in the keychain. Each iOS app gets its own space in the keychain, that no other apps can access to.
- There’s no need to store encryption keys in our app. We rely on the system to do the encryption and decryption for us.


### ATS (https), SSL-Pinning (certificate & public key), Obfuscation
