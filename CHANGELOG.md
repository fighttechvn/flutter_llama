## 1.1.3 — iOS 15 launch-crash fix

- Rebuilt `ios/llama.xcframework` (device + simulator slices) with `GGML_BLAS=OFF`
  and a minimum deployment target of iOS 14.0 (was 16.4). The previous build
  linked Apple Accelerate's new-LAPACK ILP64 BLAS symbol
  `cblas_sgemm$NEWLAPACK$ILP64`, which only exists on iOS 16.4+. On iOS 15 and
  earlier, dyld could not resolve it and the host app crashed at launch
  (EXC_CRASH / SIGABRT, "Symbol missing"). Metal GPU acceleration is unchanged;
  CPU matmul now uses ggml's built-in kernels + vDSP instead of Accelerate BLAS.
- Added a runtime capability guard in `FlutterLlamaPlugin.loadModel` that returns
  `UNSUPPORTED_OS` on iOS < 14 so callers degrade gracefully.
- Bumped the iOS podspec platform to 14.0 to match the framework floor.
- Note: macOS / tvOS / visionOS slices were left as-is (not consumed by the iOS
  app that needed this fix); rebuild them the same way if those platforms ship.

# Changelog

All notable changes to this project will be documented in this file.

## [1.1.2] - 2025-01-28

### Changed
- Optimized package size by excluding debug symbols and build artifacts
- Added comprehensive .pubignore to reduce package size from 234 MB to 20 MB

## [1.1.1] - 2025-01-28

### Fixed
- Fixed package dependencies: moved `http`, `path`, and `path_provider` from `dev_dependencies` to `dependencies` for proper pub.dev publishing
- Resolved package validation errors for service dependencies

### Changed
- Updated package structure for better dependency management

## [1.0.1] - 2025-01-27

### Fixed
- Fixed macOS library build artifacts for pub.dev publishing
- Removed unused imports in multimodal implementation
- Removed unnecessary library name declaration
- Improved .pubignore to reduce package size

### Changed
- Updated package metadata

## [1.0.0] - 2025-01-27

### Added
- Initial stable release
- Full support for llama.cpp GGUF models on iOS and macOS
- GPU acceleration via Metal
- CPU optimization via Accelerate framework
- Streaming text generation
- Batch processing support
- Multiple model format support
- Comprehensive documentation
- Example application with demos
- Integration tests

## [0.1.1] - 2025-01-26

### Added
- Multimodal support (vision models)
- Enhanced model loading
- Improved error handling

## [0.1.0] - 2025-01-25

### Added
- Initial beta release
- Basic llama.cpp integration
- iOS and macOS platform support
- Model loading and text generation
- Basic configuration options

