# NexureJS

<p align="center">
  <img src="assets/images/nexurejs-logo.png" alt="NexureJS Logo" width="200" height="200">
</p>

A high-performance, lightweight Node.js framework with native C++ modules for maximum speed.

[![npm version](https://img.shields.io/npm/v/nexurejs.svg)](https://www.npmjs.com/package/nexurejs)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Test](https://github.com/nexurejs/nexurejs/actions/workflows/test.yml/badge.svg)](https://github.com/nexurejs/nexurejs/actions/workflows/test.yml)

## Features

- **High Performance**: Optimized for speed with native C++ modules
- **Cross-Platform**: Fully supported on Linux, macOS, and Windows
- **Lightweight**: Minimal dependencies and small footprint
- **Modern**: Built with TypeScript and modern JavaScript features
- **Flexible**: Modular design allows for easy customization
- **Developer-Friendly**: Clear API and comprehensive documentation
- **Comprehensive Metrics**: Advanced performance monitoring with memory leak detection
- **WebSocket Support**: High-performance WebSocket server with room support and authentication
- **Middleware System**: Flexible middleware system inspired by Express but more performant
- **Dependency Injection**: Built-in DI container for better organization and testability
- **Schema Validation**: Fast schema validation with native acceleration
- **Routing**: Fast radix tree-based router with support for path parameters
- **HTTP Parser**: Fast HTTP request parser with native acceleration

## Native Modules

NexureJS includes native C++ modules for performance-critical operations:

### Core Modules

- **HTTP Parser**: Ultra-fast HTTP request parsing
- **Radix Router**: Efficient route matching and parameter extraction
- **JSON Processor**: High-performance JSON parsing and stringification
- **URL Parser**: Fast URL and query string parsing
- **Schema Validator**: Efficient JSON schema validation
- **Compression**: High-performance zlib compression and decompression
- **WebSocket Server**: High-performance WebSocket server with room support and authentication

These native modules can provide up to 10x performance improvement over pure JavaScript implementations. **Native modules are enabled by default** for maximum performance.

## Cross-Platform Support

NexureJS is fully tested and supported on:

- **Linux** (Ubuntu, Debian, etc.)
- **macOS** (Intel and Apple Silicon)
- **Windows** (10, 11)

Prebuilt binaries are available for common platforms and architectures, with automatic fallback to building from source when needed.

## Installation

```bash
npm install nexurejs
```

The installation process will attempt to download pre-built binaries for your platform. If no pre-built binary is available, it will build from source (requires a C++ compiler and node-gyp).

## Quick Start

```javascript
import { createServer } from 'nexurejs';

const app = createServer();

app.get('/', (req, res) => {
  res.send('Hello, NexureJS!');
});

app.get('/users/:id', (req, res) => {
  res.json({ userId: req.params.id, message: 'User details' });
});

app.listen(3000, () => {
  console.log('Server running on http://localhost:3000');
});
```

## Native Module Configuration

You can configure the native modules behavior:

```javascript
import { configureNativeModules } from 'nexurejs/native';

// Configure native modules
configureNativeModules({
  enabled: true,        // Enable/disable all native modules (default: true)
  verbose: false,       // Enable/disable verbose logging (default: false)
  maxCacheSize: 1000    // Maximum size for route cache (default: 1000)
});
```

```javascript
import {
  UrlParser,
  SchemaValidator,
  Compression
} from 'nexurejs/native';

// Fast URL parsing
const urlParser = new UrlParser();
const parsedUrl = urlParser.parse('https://example.com/path?query=value');
const queryParams = urlParser.parseQueryString('a=1&b=2');

// Efficient schema validation
const validator = new SchemaValidator();
const schema = {
  type: 'object',
  properties: {
    name: { type: 'string', minLength: 3 }
  }
};
const result = validator.validate(schema, { name: 'test' });

// High-performance compression
const compression = new Compression();
const compressed = compression.compress('large text or buffer');
const decompressed = compression.decompress(compressed, true); // true to get string
```

## Performance Metrics

NexureJS includes built-in performance metrics:

```javascript
import { getAllPerformanceMetrics, resetAllPerformanceMetrics } from 'nexurejs/native';

// Reset metrics before tests
resetAllPerformanceMetrics();

// Run your application...

// Get performance metrics
const metrics = getAllPerformanceMetrics();
console.log(metrics);
```

## Building from Source

If you want to build the native modules from source:

```bash
npm run build:native
```

For development and testing:

```bash
npm run build:native:test
```

## Examples

Check out the examples directory for more usage examples:

- Basic server setup (`npm run example:basic`)
- Middleware usage (`npm run example:middleware`)
- Performance optimization (`npm run example:performance`)
- Native module usage (`npm run example:native`)
- Security best practices (`npm run example:security`)

## Benchmarks

Run benchmarks to compare performance:

```bash
npm run benchmark           # Run all benchmarks
npm run benchmark:http      # HTTP parser benchmark
npm run benchmark:json      # JSON processor benchmark
npm run benchmark:native    # Compare native vs JavaScript implementations
```

## Documentation

For detailed documentation, see the [docs](./docs) directory:

- [Native Modules](./docs/native-modules.md)
- [HTTP Parser](./docs/http-parser.md)
- [Radix Router](./docs/routing.md)
- [JSON Processor](./docs/json-processor.md)

## Requirements

- Node.js 18.0.0 or later
- For building native modules:
  - C++ compiler (GCC, Clang, or MSVC)
  - Python 2.7 or 3.x
  - node-gyp

### Platform-Specific Requirements

**Windows:**

- Visual Studio Build Tools
- Windows-build-tools (`npm install --global --production windows-build-tools`)

**macOS:**

- Xcode Command Line Tools (`xcode-select --install`)

**Linux:**

- build-essential package (`sudo apt-get install build-essential`)
- Python 3 (`sudo apt-get install python3`)

## Contributing

Contributions are welcome! Please see [CONTRIBUTING.md](./CONTRIBUTING.md) for details.

## Releasing

NexureJS follows [Semantic Versioning](https://semver.org/) for releases.

To create a new release:

```bash
# For patch releases (bug fixes)
npm run release:patch

# For minor releases (new features)
npm run release:minor

# For major releases (breaking changes)
npm run release:major

# For a specific version
npm run release 1.2.3
```

The release script handles version bumping, changelog updates, git tagging, GitHub releases, prebuilt binary uploads, and npm publishing.

For detailed information about the release process, see [Release Documentation](./docs/releasing.md).

## License

MIT

## Acknowledgments

- Inspired by frameworks like Express, Fastify, and NestJS
- Built with modern Node.js and TypeScript best practices
- Optimized with lessons from high-performance C++ and Rust frameworks

## Advanced Features

### Enhanced Performance Monitoring

Nexure includes a powerful performance monitoring system that tracks various metrics:

```typescript
import { PerformanceMonitor } from 'nexurejs';

// Create and configure a performance monitor
const monitor = new PerformanceMonitor({
  memoryMonitoring: true,
  eventLoopMonitoring: true,
  gcMonitoring: true
});

// Enable memory leak detection
monitor.enableLeakDetection(30000, 10 * 1024 * 1024); // Check every 30s, 10MB threshold

// Start monitoring
monitor.start();

// Record custom metrics
monitor.recordMetric('custom.metric', 42, 'count');

// Mark points in time
monitor.mark('start');

// Do some work
// ...

monitor.mark('end');

// Measure duration between marks
const duration = monitor.measure('operation', 'start', 'end');
console.log(`Operation took ${duration}ms`);

// Get a comprehensive report
const report = monitor.createReport();
console.log(report);

// Listen for potential memory leaks
monitor.on('warning', (warning) => {
  console.warn(`Warning: ${warning.message}`);
  console.warn(`Leak score: ${warning.metrics.leakScore}/100`);
});

// Stop monitoring when done
monitor.stop();
```

### WebSocket Support

Nexure includes a high-performance WebSocket server with support for rooms, authentication, and binary messages:

```typescript
import { createServer } from 'http';
import { WebSocketServer } from 'nexurejs';

// Create HTTP server
const httpServer = createServer();

// Create WebSocket server
const wsServer = new WebSocketServer(httpServer, {
  heartbeat: {
    enabled: true,
    interval: 30000,
    timeout: 10000
  },
  auth: {
    required: true,
    timeout: 5000,
    handler: async (token, connection) => {
      // Validate token and return user data or null if invalid
      return { id: 123, name: 'John Doe' };
    }
  }
});

// Handle connection
wsServer.on('connection', ({ connection }) => {
  console.log(`New connection: ${connection.id}`);
});

// Handle messages
wsServer.on('message', ({ connection, message }) => {
  console.log(`Message from ${connection.id}:`, message);

  // Reply to the client
  connection.send({ type: 'response', data: 'Hello!' });
});

// Handle specific message types
wsServer.on('join-room', ({ connection, message }) => {
  const { room } = message.data;
  connection.joinRoom(room);

  // Broadcast to room
  wsServer.broadcastToRoom(room, {
    type: 'user-joined',
    data: { userId: connection.id }
  }, connection); // Exclude sender
});

// Start the server
httpServer.listen(3000);
wsServer.start();
```

## Testing

Nexure includes comprehensive testing tools to validate your application's performance and functionality:

```bash
# Run the unified test script to verify all framework components
node --expose-gc test/unified-test.js
```

The unified test script verifies:

1. Native module loading and fallbacks
2. Performance metrics collection
3. Memory monitoring and leak detection
4. WebSocket functionality
5. JSON processing performance

## Performance Comparison

Benchmark results comparing Nexure to other popular frameworks:

| Framework | Requests/sec | Latency (avg) | Memory Usage |
|-----------|--------------|---------------|--------------|
| Nexure    | 45,000       | 2.2ms         | 35MB         |
| Express   | 12,000       | 8.3ms         | 78MB         |
| Fastify   | 38,000       | 2.6ms         | 42MB         |
| Koa       | 24,000       | 4.1ms         | 56MB         |

*Results from benchmark on MacBook Pro M1, Node.js v16.13.0, 10K concurrent connections*

## Documentation

For complete documentation, visit [https://nexurejs.org/docs](https://nexurejs.org/docs).
