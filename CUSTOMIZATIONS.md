# Fork Customizations

This document tracks modifications made to the original sacd-ripper project.

## Changes Made

### Build System Improvements
- **CMake Compatibility (2026-02-16)**: Updated `cmake_minimum_required` from 2.6 to 3.10
  - **Files**: `tools/sacd_extract/CMakeLists.txt`, `tools/sacd_extract/BUILD.md`  
  - **Reason**: Fix compatibility with modern CMake versions on macOS and other systems
  - **Commit**: fbc7534

### macOS-Specific Changes
- **Branch**: `macos`
- **Purpose**: Platform-specific optimizations and compatibility fixes

## Maintenance Notes
- Upstream: https://github.com/EuFlo/sacd-ripper  
- Fork: https://github.com/szaniszlo/sacd-ripper
- Main customization branch: `macos`
- Strategy: Keep `master` synchronized with upstream, develop on `macos` branch

## Building
See [BUILD.md](tools/sacd_extract/BUILD.md) for detailed build instructions.