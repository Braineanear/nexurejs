# Changelog

All notable changes to NexureJS will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.2.0] - 2025-03-20

### Added

- Enhanced documentation across the entire codebase
- Detailed versioning strategy in release documentation
- Long-term support (LTS) planning information
- Post-release verification process
- Comprehensive release preparation checklist

### Changed

- Improved release process documentation with more detailed steps
- Updated roadmap with clearer development phases
- Enhanced contribution guidelines with more specific instructions
- Better organization of technical documentation

### Fixed

- Documentation formatting inconsistencies
- Missing steps in release verification process
- Outdated references in API documentation
- Improved cross-referencing between documentation files

## [0.1.9] - 2025-03-10

### Added

- Support for Node.js 23.x

### Changed

- Moved configuration files to root directory for better compatibility with build tools
- Updated TypeScript configuration for improved build process
- Improved ESLint configuration to reduce warnings and errors

### Fixed

- Fixed release script to correctly handle CHANGELOG.md in docs folder
- Fixed native module build process for cross-platform compatibility
- Resolved linting errors in prebuild.js script
- Fixed TypeScript configuration paths for proper module resolution

## [0.1.6] - 2025-03-09

### Added

- Multi-platform CI testing (Ubuntu, Windows, macOS)
- Automated build tools installation for different platforms
- Build artifacts collection on test failures
- C++17 standard enforcement across all platforms

### Changed

- Enhanced test workflow with parallel testing on multiple Node.js versions
- Improved error handling and debugging in CI pipeline
- Better naming and organization of test jobs

### Fixed

- Missing stdexcept header in HTTP parser
- Build tools setup for Windows and Ubuntu environments
- Cross-platform C++ compilation issues

## [0.1.5] - 2025-03-09

### Added

- Enhanced release script with improved GitHub release management
- Automated prebuilt binary uploads to GitHub releases
- Improved npm publishing workflow
- Better error handling and retry logic for asset uploads
- Progress tracking for binary uploads
- Dry run mode for testing release process

### Changed

- Combined separate release scripts into a single unified script
- Improved release process documentation
- Enhanced error messages and user feedback
- Better handling of GitHub API interactions

### Fixed

- Release script ES module compatibility
- Asset upload reliability with chunked uploads
- GitHub release creation error handling
- npm publishing version conflict handling

## [0.1.1] - 2025-03-09

### Added

- Initial documentation for native modules
- Performance metrics tracking for all native modules
- Comprehensive release documentation and process
- GitHub Actions workflows for automated releases and testing

### Fixed

- ES Module compatibility in build and installation scripts
- Native module building and loading in ES Module environment
- RadixRouter C++ code to use correct Node-API methods
- Installation and prebuild scripts for better cross-platform support

## [0.1.0] - 2023-11-15

### Added

- Initial release of NexureJS framework
- HTTP Parser native module for fast HTTP request parsing
- Radix Router native module for efficient route matching
- JSON Processor native module for high-performance JSON operations
- Basic server functionality with middleware support
- TypeScript support and type definitions
- Comprehensive documentation
- Example applications

### Changed

- Native modules are now enabled by default for maximum performance
- Default configuration includes maxCacheSize of 1000 for route caching

### Fixed

- HTTP Parser streaming functionality for handling large requests
- Native module loading path resolution for various environments
