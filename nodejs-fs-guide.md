# Node.js File System (fs) Library Comprehensive Guide

## Table of Contents
1. [Introduction](#introduction)
2. [Installation](#installation)
3. [File Reading](#file-reading)
4. [File Writing](#file-writing)
5. [File System Operations](#file-system-operations)
6. [File Streams](#file-streams)
7. [Error Handling](#error-handling)
8. [Best Practices](#best-practices)
9. [Advanced Examples](#advanced-examples)

## Introduction

The Node.js `fs` (File System) module provides a powerful API for interacting with the file system. It allows you to:
- Read and write files
- Manage directories
- Handle file permissions
- Create and delete files/directories
- Watch file changes

## Installation

No separate installation is required. The `fs` module is built-in to Node.js.

```javascript
// CommonJS
const fs = require('fs');

// ES Module
import fs from 'fs';
```

## File Reading

### Synchronous Reading
```javascript
try {
    const data = fs.readFileSync('example.txt', 'utf8');
    console.log(data);
} catch (error) {
    console.error('Sync Read Error:', error);
}
```

### Asynchronous Reading (Callback)
```javascript
fs.readFile('example.txt', 'utf8', (err, data) => {
    if (err) {
        console.error('Async Read Error:', err);
        return;
    }
    console.log(data);
});
```

### Promise-based Reading
```javascript
async function readFileExample() {
    try {
        const data = await fs.promises.readFile('example.txt', 'utf8');
        console.log(data);
    } catch (error) {
        console.error('Promise Read Error:', error);
    }
}
```

### Reading Large Files with Streams
```javascript
const readStream = fs.createReadStream('large-file.txt', {
    encoding: 'utf8',
    highWaterMark: 1024  // Read in 1KB chunks
});

readStream.on('data', (chunk) => {
    console.log('Chunk:', chunk);
});

readStream.on('end', () => {
    console.log('Finished reading');
});
```

## File Writing

### Synchronous Writing
```javascript
try {
    fs.writeFileSync('output.txt', 'Hello, World!', 'utf8');
} catch (error) {
    console.error('Sync Write Error:', error);
}
```

### Asynchronous Writing (Callback)
```javascript
fs.writeFile('output.txt', 'Hello, World!', 'utf8', (err) => {
    if (err) {
        console.error('Async Write Error:', err);
    }
});
```

### Promise-based Writing
```javascript
async function writeFileExample() {
    try {
        await fs.promises.writeFile('output.txt', 'Hello, World!', 'utf8');
    } catch (error) {
        console.error('Promise Write Error:', error);
    }
}
```

## File System Operations

### Directory Operations
```javascript
// Create Directory
fs.mkdirSync('new-directory');

// Read Directory Contents
const files = fs.readdirSync('directory-path');
console.log(files);

// Check File/Directory Existence
const exists = fs.existsSync('file-path');

// Get File Stats
const stats = fs.statSync('file-path');
console.log({
    size: stats.size,
    isFile: stats.isFile(),
    createdAt: stats.birthtime
});
```

## File Streams

### Copying Files with Streams
```javascript
const readStream = fs.createReadStream('source.txt');
const writeStream = fs.createWriteStream('destination.txt');

readStream.pipe(writeStream);
```

## Error Handling

### Comprehensive Error Handling
```javascript
function handleFileError(err) {
    switch (err.code) {
        case 'ENOENT':
            console.log('File not found');
            break;
        case 'EACCES':
            console.log('Permission denied');
            break;
        default:
            console.error('Unexpected error:', err);
    }
}
```

## Best Practices

1. **Use Async Methods**: Prefer `promises` or callback methods in production
2. **Stream Large Files**: Use streams for files larger than memory
3. **Handle Errors**: Always implement comprehensive error handling
4. **Use Appropriate Encoding**: Specify encoding for text files
5. **Close Streams**: Properly close file streams and handles

## Advanced Examples

### Watching Files
```javascript
fs.watch('directory-path', (eventType, filename) => {
    console.log(`Event: ${eventType}, File: ${filename}`);
});
```

### File Permissions
```javascript
// Change file permissions (Unix-like systems)
fs.chmodSync('file-path', 0o755);
```

### Recursive Directory Creation
```javascript
// Recursively create nested directories
fs.mkdirSync('path/to/nested/directory', { recursive: true });
```

## Performance Considerations

- Use `fs.promises` for better performance and readability
- Implement caching for frequently read files
- Avoid synchronous methods in production
- Use streams for large file operations

## Conclusion

The `fs` module is a powerful tool for file system operations in Node.js. Always consider performance, error handling, and use the most appropriate method for your specific use case.

## Contributing

Contributions and improvements to this guide are welcome! 

## License

MIT License

Copyright (c) 2024 Suraj Raj

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

```

## Additional Notes

This comprehensive markdown guide covers:
- Detailed explanations of file system operations
- Multiple examples for each method
- Best practices and performance considerations
- Error handling techniques
- Advanced use cases

