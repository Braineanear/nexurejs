# NexureJS Native Modules

NexureJS includes native C++ modules for performance-critical operations. These modules provide significant performance improvements over pure JavaScript implementations. **Native modules are enabled by default** for maximum performance.

## Overview

The native modules in NexureJS include:

1. **HTTP Parser**: Ultra-fast HTTP request parsing
2. **Radix Router**: Efficient route matching and parameter extraction
3. **JSON Processor**: High-performance JSON parsing and stringification

## Cross-Platform Support

NexureJS native modules are fully supported on:

- **Linux** (x64, arm64)
- **macOS** (x64, arm64)
- **Windows** (x64)

Prebuilt binaries are available for these platforms, and the installation process will automatically download the appropriate binary for your system. If a prebuilt binary is not available, the installation will fall back to building from source.

## Performance Benefits

The native modules provide significant performance improvements:

| Component | JavaScript (ops/sec) | Native (ops/sec) | Improvement |
|-----------|----------------------|------------------|-------------|
| HTTP Parser | 50,000 | 500,000 | 10x |
| Radix Router | 100,000 | 800,000 | 8x |
| JSON Parse | 200,000 | 1,200,000 | 6x |
| JSON Stringify | 150,000 | 900,000 | 6x |

*Note: Actual performance may vary depending on your hardware and the complexity of the data being processed.*

## Installation

The native modules are included with NexureJS and will be automatically installed when you install the package. The installation process will attempt to download pre-built binaries for your platform. If no pre-built binary is available, it will build from source.

### Prerequisites

To build from source, you need:

- Node.js 18 or later
- npm or yarn
- C++ compiler (GCC, Clang, or MSVC)
- Python 2.7 or 3.x
- node-gyp

#### Platform-Specific Requirements

**Windows:**
- Visual Studio Build Tools
- Windows-build-tools (`npm install --global --production windows-build-tools`)

**macOS:**
- Xcode Command Line Tools (`xcode-select --install`)

**Linux:**
- build-essential package (`sudo apt-get install build-essential`)
- Python 3 (`sudo apt-get install python3`)

### Building from Source

If you want to build the native modules from source:

```bash
npm run build:native
```

For development and testing:

```bash
npm run build:native:test
```

For building on all supported platforms (typically done in CI):

```bash
npm run build:native:all
```

## Usage

### Importing

```typescript
import {
  HttpParser,
  RadixRouter,
  JsonProcessor,
  configureNativeModules,
  getNativeModuleStatus
} from 'nexurejs/native';
```

### Configuration

You can configure the native modules behavior:

```typescript
configureNativeModules({
  enabled: true,        // Enable/disable all native modules (default: true)
  verbose: false,       // Enable/disable verbose logging (default: false)
  maxCacheSize: 1000    // Maximum size for route cache (default: 1000)
});
```

### Checking Status

You can check if the native modules are available:

```typescript
const status = getNativeModuleStatus();
console.log(status);
// {
//   loaded: true,
//   httpParser: true,
//   radixRouter: true,
//   jsonProcessor: true,
//   error: null
// }
```

### Performance Metrics

You can get performance metrics for the native modules:

```typescript
import { getAllPerformanceMetrics, resetAllPerformanceMetrics } from 'nexurejs/native';

// Reset metrics before tests
resetAllPerformanceMetrics();

// Run your application...

// Get performance metrics
const metrics = getAllPerformanceMetrics();
console.log(metrics);
```

## Components

### HTTP Parser

The HTTP Parser is responsible for parsing HTTP requests. It provides methods for parsing complete requests or streaming requests in chunks.

```typescript
import { HttpParser } from 'nexurejs/native';

const httpParser = new HttpParser();

// Parse a complete request
const buffer = Buffer.from('GET /api/users HTTP/1.1\r\nHost: example.com\r\n\r\n');
const result = httpParser.parse(buffer);

console.log(result);
// {
//   method: 'GET',
//   url: '/api/users',
//   httpVersion: '1.1',
//   headers: { host: 'example.com' },
//   body: null
// }
```

#### Streaming HTTP Parser

For parsing HTTP requests in chunks:

```typescript
import { HttpStreamParser } from 'nexurejs/http';

const streamParser = new HttpStreamParser();

// Process the request in chunks
const chunk1 = buffer.slice(0, 50);
const chunk2 = buffer.slice(50);

streamParser.write(chunk1);
console.log('Chunk 1 processed, state:', streamParser.getState());

streamParser.write(chunk2);
const result = streamParser.getResult();
console.log('Request parsed:', result);

// Reset the parser for the next request
streamParser.reset();
```

### Radix Router

The Radix Router is responsible for matching URLs to routes. It provides methods for adding, finding, and removing routes.

```typescript
import { RadixRouter } from 'nexurejs/native';

const router = new RadixRouter();

// Add routes
router.add('GET', '/api/users', getUsersHandler);
router.add('GET', '/api/users/:id', getUserHandler);

// Find a route
const match = router.find('GET', '/api/users/123');

console.log(match);
// {
//   handler: getUserHandler,
//   params: { id: '123' },
//   found: true
// }
```

### JSON Processor

The JSON Processor is responsible for parsing and stringifying JSON data. It provides methods for parsing JSON strings or buffers and stringifying JavaScript objects.

```typescript
import { JsonProcessor } from 'nexurejs/native';

const jsonProcessor = new JsonProcessor();

// Parse JSON
const jsonString = '{"name":"John","age":30}';
const parsed = jsonProcessor.parse(jsonString);

console.log(parsed);
// { name: 'John', age: 30 }

// Parse JSON from Buffer
const jsonBuffer = Buffer.from(jsonString);
const parsedFromBuffer = jsonProcessor.parse(jsonBuffer);

// Stringify JSON
const obj = { name: 'John', age: 30 };
const stringified = jsonProcessor.stringify(obj);

console.log(stringified);
// '{"name":"John","age":30}'
```

## Benchmarking

NexureJS includes benchmarks to compare the performance of native and JavaScript implementations:

```bash
# Run all benchmarks
npm run benchmark

# Run specific benchmarks
npm run benchmark:http
npm run benchmark:json

# Compare native vs JavaScript implementations
npm run benchmark:native
```

## Troubleshooting

### Module Not Found

If you get an error like `Error: Cannot find module 'nexurejs-native-xxx'`, it means the pre-built binary for your platform is not available. You can build from source:

```bash
npm run build:native
```

### Build Errors

If you encounter build errors, make sure you have the necessary build tools installed:

- C++ compiler (GCC, Clang, or MSVC)
- Python 2.7 or 3.x
- node-gyp

On Windows, you may need to install the Visual Studio Build Tools:
```bash
npm install --global --production windows-build-tools
```

On macOS, you may need to install the Xcode Command Line Tools:
```bash
xcode-select --install
```

On Linux, you may need to install the build-essential package:
```bash
sudo apt-get update
sudo apt-get install -y build-essential python3
```

### C++ Standard Issues

NexureJS native modules require C++17 support. If you encounter compilation errors related to C++ features, ensure your compiler supports C++17:

```bash
# When building manually, specify C++17
CXXFLAGS="-std=c++17" npm run build:native
```

### Performance Issues

If you're not seeing the expected performance improvements, make sure the native modules are actually being used:

```typescript
const status = getNativeModuleStatus();
console.log(status);
```

If `status.loaded` is `false`, the native modules are not being used. Check the `status.error` property for more information.

## Contributing

If you want to contribute to the native modules, see the [Contributing Guide](../CONTRIBUTING.md) for more information.

## License

The native modules are licensed under the MIT License. See the [LICENSE](../LICENSE) file for more information.
