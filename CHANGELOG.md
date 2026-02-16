# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### 🔧 Fixed

- **Compiler Compatibility**: Fixed `mkdir_wrap` function signature to use `mode_t` instead of `char *` for better compatibility with modern C compilers
- **Linker Issues**: Resolved alignment errors in protobuf-generated code by adding explicit alignment attributes
- **Build Warnings**: Reduced compiler warnings by improving flags and removing strict aliasing issues

### ✨ Added

- **Build System**: Added automatic binary stripping in Release builds
- **Installation**: Added `make install` target for system-wide installation to `/usr/local/bin`
- **Uninstallation**: Added `make uninstall` target for clean removal
- **Documentation**: Complete rewrite of documentation in Markdown format
  - New comprehensive [README.md](README.md) with modern formatting
  - Detailed [BUILD.md](tools/sacd_extract/BUILD.md) with platform-specific build instructions
  - Extensive [USAGE.md](tools/sacd_extract/USAGE.md) with examples and best practices
- **CI/CD**: Added GitHub Actions workflow for automated building and testing across Linux, macOS, and Windows
- **Project Structure**: Added changelog and improved project organization

### 🚀 Improved

- **Build Performance**: Optimized CMake configuration for faster builds
- **Binary Size**: Release builds now produce smaller, stripped binaries
- **Developer Experience**: Enhanced build process with better error handling and clearer instructions

### 📝 Documentation Enhancements

- **Restructured**: Moved from single `readme.rst` to organized Markdown documentation
- **Comprehensive**: Added detailed platform-specific build instructions
- **User-Friendly**: Improved examples and troubleshooting sections
- **Searchable**: Better organization with clear sections and cross-references

## [Previous Versions]

For changes in earlier versions, please refer to the original [sacd-ripper project](https://github.com/sacd-ripper/sacd-ripper) and the git commit history.

### Core Features (Inherited from Fork Base)

- **Padding-less DSF generation** (`-z`): Eliminates zero-padding for gapless playback
- **Concurrent processing** (`-w`): Simultaneous ISO+DSF/DSDIFF extraction
- **Enhanced metadata**: Extended ID3v2 tag support (ISRC, Publisher, Copyright, Composer, Album Artist)
- **Multi-format output**: DSF, DSDIFF, DSDIFF Edit Master, RAW ISO support
- **Performance optimizations**: ~3x DST decoding speed improvement
- **Cross-platform**: Linux, macOS, Windows (Mingw-w64) support
- **Advanced threading**: Parallel raw read and DST decoding
- **Flexible extraction**: Simultaneous stereo and multi-channel extraction

---

## Legend

- 🔧 **Fixed**: Bug fixes and compatibility improvements
- ✨ **Added**: New features and capabilities
- 🚀 **Improved**: Enhancements to existing functionality
- 📝 **Documentation**: Changes to documentation and guides
- ⚠️ **Changed**: Breaking changes or significant modifications
- 🗑️ **Removed**: Deprecated or removed features
