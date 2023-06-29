# CI - Jenkins | Azure

## Pipeline


# CD - [Fastlane](https://fastlane.tools/)

## Automate screenshots

- Automatically generate localised screenshots for the App Store

## Beta deployment

- Distribute beta builds to testers on different platforms (like TestFlights, and Azure AppCenter)

## App Store deployment

- Publish a new release to the App Store

## Code Signing

- [Overview of iOS app signing](https://www.youtube.com/watch?v=0lJvQ-442OY&ab_channel=iLane)
- Certificate: 
    - Create CSR:
        - generate a pair (private_key, public_key)
        - store `private_key` in the key chain
        - create a certificate request by filling all info (like email, company name, etc), and attach the public key
        - send this CSR to the developer portal website
    - Download the certificate
        - Certificate is to prove who writes the code. The person who writes the code must be trusted by Apple.
- Provisioning Profile
    - Register your apps on App Store Connect website, where you have to fill all info (like teamId, bundleId, appId, device Ids, entitlements, etc.)
    - Provisioning Profile = Certificate + app info (like teamId, bundleId, appId, device Ids, entitlements, etc.)
    - Download the provisioning profile
    - Provisioning Profile is to define the rules for running the app on the device. 
    - For example, it’s must be an app with the AppId, that can run on certain devices included in the provisioning profile. And the app that has capabilities defined in the entitlement file
- Code Signing
    - For development, we can use XCODE to deploy on the device. We just need to specify the code signing identity, and XCODE will manage everything for us.
    - For Continuous Delivery, we can’t use local XCODE to ship applications. The applications have to be shipped from the Continuous Integration server.
        - Either we have to use the command line like `codesign`
        - Or use a tool like `fastlane` to automate this process
## Fastlane

- [fastlane overview](https://www.youtube.com/watch?v=N_NwcDO_S_s&list=PLHchrqMOsMH4GjzlB3oVJmE6gTtXyZ-zQ&index=1&ab_channel=iLane)
- [fastlane produce](https://www.youtube.com/watch?v=XlYd93HVakk&list=PLHchrqMOsMH4GjzlB3oVJmE6gTtXyZ-zQ&index=2&ab_channel=iLane)
    - Create new iOS apps on both Apple Developer Portal and App Store Connect 
- [fastlane cert & sigh](https://www.youtube.com/watch?v=90hJDqbUyqM&list=PLHchrqMOsMH4GjzlB3oVJmE6gTtXyZ-zQ&index=3&ab_channel=iLane)
    - Manage certificate & provisioning profile 
        - generate a pair of private & public key, create & send CSR, download certificate and install in the keychain
        - create a provisioning profile that link a certificate with a specific app in App Store Connect
- [fastlane match](https://www.youtube.com/watch?v=Edr88s5YlH4&list=PLHchrqMOsMH4GjzlB3oVJmE6gTtXyZ-zQ&index=4&ab_channel=iLane)
    - Store all encrypted certificate, provisioning profile, private key (for development or distribution) in cloud, or git repo
    - Developers can run `fastlane match development` to fetch all certificate, provisioning profile, and private key to their local machine (Note that developers must know the passphrase to decrypt)
