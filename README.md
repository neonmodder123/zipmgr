# zipmgr
A pure Swift library for reading and extracting .zip archives

## Installation
Add zipmgr to your SwiftPM dependencies in Package.swift:

```swift
dependencies: [
    .package(url: "https://github.com/neonmodder123/zipmgr.git", from: "1.0.0")
]
```

Then import it in your Swift code:
```swift
import zipmgr
```

## Usage
### Load an archive
```swift
// load archive data
let data = try Data(contentsOf: URL(fileURLWithPath: "archive.zip"))

// initialize zipmgr
let archive = try ZipArchive(data: data)
```

### List entries
```swift
// path is optional
for entry in archive.entries {
    print("path: \(entry.path), size: \(entry.uncompressedSize)")
}
```

### Extract a file
```swift
if let entry = archive["example.txt"] {
    let contents = try archive.extract(entry)
    print("extracted \(entry.path), bytes: \(contents.count)")
}
```

### One-liner example
```swift
let contents = try ZipArchive(data: Data(contentsOf: URL(fileURLWithPath: "archive.zip"))).extract(archive["example.txt"]!)
```