# Storage

## SQLite

- Light way, good performance (faster 35% than using NSFileManager to access a file on disk)
- No user & password login
- Easily portable
- No support encryption. SQLite relies on the file permission (using iOS data protection levels when creating sqlite file) to secure data

## CoreData

- uses SQLite as its persistence store.
- manages a complex object graph with many entities, attributes, relationships
- learning curve

## SwiftUI

- is built on top of Core Data (Core Data is not a native solution for both Swift and SwiftUI)
- starting from iOS17+
- as long as the model class is annotated with @Model, SwiftData will automatically observe the change and write the update to the database (SQLite)
- with SwiftData, there’s no need to worry about connecting to the database or understanding SQL in order to retrieve data records.
- source: [swiftData](https://www.appcoda.com/swiftdata/)

## File, Plist

- Plist: Key & Value (simple type) pattern

## UserDefault

- Key & Value (simple type) pattern

## Keychain

- The code for saving data is similar to the code for saving data in NUserDefaults

## NSCache

- in-memory cache uses Key & Value pattern
- support some policies to remove data when the cache is full

## NSURLCache

- support in-memory and on-disk caching mechanism
- caching directives in HTTP headers

## Offline approach

- UI will not directly use network to exchange data with the server
- UI will talk with DB. Now when we don’t have internet, we can still use the app, because our app will take or update data from the database
- Then we need a system that syncs changes in DB to the server
- We have to handle the syncs failure or sync conflicts

# Conclusion

- If the device is jail broken, none of your data is secure
