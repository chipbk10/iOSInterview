# SSL-Pinning

## HTTPS

- Client pings the server
- The server will return a certificate
- The client will check if the certificate is issued by a trusted CA (Certificate Authority)
- If the certificate is valid, the client will use the public key in the certificate to encrypt a secret key, and send back to the server
- The server will use its private key to decrypt this key
- From now on, the client and server use this secret key to encrypt and decrypt the data which is transferred between them

## Why is HTTPs still not secured?

- HTTPS is still not secured enough, because when the client receive a certificate, it only checks if the certificate is issued by a trusted CA
- A hacker can play a role as a man in the middle who sends a fake certificate to the client to receive the key, and then use the public key from the server to decrypt this key, and send back to the server
- A fake certificate can be installed on the client’s device, and the OS system will trust the communication.

## SSL-Pinning

- To fix this issue, there should be a way through which the client can identify that this is a fake certificate, or not the certificate of the server that the client wants to communicate with

### SSL-Pinning Certificate

- We can pin the certificate of the server into the bundle of the application. Because the actual certificate of the server, we can access to it, we can download and put it into the bundle of the app
- When our app starts a https connection, and receives a certificate, we will compare this certificate with the one we have in the bundle
- Cons: we need to release a new build whenever the certificate is expired 

### SSL-Pinning Public Key

- We keep the public key of the server’s certificate in our code
- We do the same, we compare the public key of the certificate with the one we have in our code
- Pros: we don’t need to release a new build, because the public key remains the same, even if the certificate is changed

## Obfuscation

- SSL-Pinning can be bypassed. On the rooted device, if the hacker get access to your source code, they will change or manipulate the source code to always return success from the method where we compare the certificate or public key.
- For example, if I’m not mistaken on jailed break device, the hacker can do reverse engineering and they run Frida script  to bypass the SSL-Pinning
- We can prevent it by using `Obfuscation` technique, which will change the name of the methods, properties, parameters name in the signature of the methods after your build has been successful. So when the hacker try to access the source code, and try to manipulate it. The obfuscation will make the source code difficult to understand or identify where the comparison of the certificates or public key happens.


# Conclusion
- We use https over http to secure the communication
- We use ssl-pinning upon https to be sure that we are talking to a right person
- We use obfuscation upon ssl-pinning to make the ssl-pinning difficult to bypass (popular in Android, but iOS)

# Source

- [iOS SSL-Pinning](https://www.youtube.com/watch?v=HWJ3cCNdKKA&ab_channel=iCode)
