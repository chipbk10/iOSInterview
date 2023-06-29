# SPM vs CocoaPod vs Carthage

## SPM

### Pros

- Standard built-in, better UI (for adding a package, manage packages)
- `Package.resolved` file is stored in our project directory
- Open source

### Cons

- No way to update a single package. If I’m not mistaken, we have to update all packages if there is a new version of a package
- All dependencies are stored in the derived data folder (not in the project directory as in cocoa pod)
- Doesn’t support libraries that are mixed Objective-C and Swift

## CocoaPod

- Centralise

## Carthage

- Decentralise

# Source

- [Migrate from CocoaPod to SPM](https://www.jessesquires.com/blog/2020/02/24/replacing-cocoapods-with-swiftpm/)
