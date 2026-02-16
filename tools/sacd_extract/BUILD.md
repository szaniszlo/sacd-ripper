# Building SACD Ripper

This guide provides comprehensive instructions for building, installing, and configuring `sacd_extract` on different platforms.

## 🔧 Prerequisites

### Linux (Ubuntu/Debian)

```bash
sudo apt update
sudo apt install build-essential cmake git libiconv-hook-dev
```

### Linux (CentOS/RHEL/Fedora)

```bash
# CentOS/RHEL
sudo yum groupinstall "Development Tools"
sudo yum install cmake git

# Fedora
sudo dnf groupinstall "Development Tools"
sudo dnf install cmake git
```

### macOS

```bash
# Install Xcode Command Line Tools
xcode-select --install

# Install Homebrew (if not already installed)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install CMake
brew install cmake
```

### Windows (Cross-compilation on Linux)

```bash
# Install Mingw-w64 toolchain
sudo apt install mingw-w64 cmake

# Compile and install libiconv for Windows
wget http://ftp.gnu.org/pub/gnu/libiconv/libiconv-1.15.tar.gz
tar -xzf libiconv-1.15.tar.gz
cd libiconv-1.15
./configure --host=x86_64-w64-mingw32 --prefix=/usr/x86_64-w64-mingw32 --enable-static
make
sudo make install
```

## 🏗️ Standard Build Process

### 1. Clone the Repository

```bash
git clone https://github.com/szaniszlo/sacd-ripper.git
cd sacd-ripper/tools/sacd_extract
```

### 2. Configure Build Type

#### Debug Build (Development)

```bash
cmake -DCMAKE_BUILD_TYPE=Debug .
```

- **Features**: Debug symbols, verbose output, no optimizations
- **Use case**: Development, debugging, troubleshooting

#### Release Build (Production) - **Recommended**

```bash
cmake -DCMAKE_BUILD_TYPE=Release .
```

- **Features**: Full optimizations, stripped debug symbols, smaller binary size
- **Use case**: Production deployment, distribution
- **Performance**: ~3x faster DST decoding

### 3. Build

```bash
make -j$(nproc)  # Linux (use all CPU cores)
make -j$(sysctl -n hw.ncpu)  # macOS (use all CPU cores)
make  # Single-threaded build
```

### 4. Verify Build

```bash
ls -la sacd_extract
file sacd_extract
./sacd_extract --help
```

## 📦 Installation

### System-wide Installation

```bash
# Install to /usr/local/bin (requires sudo)
sudo make install

# Verify installation
which sacd_extract
sacd_extract --help
```

### Custom Installation Directory

```bash
# Install to custom directory
cmake -DCMAKE_INSTALL_PREFIX=/opt/sacd-tools .
make
sudo make install

# Add to PATH (add to ~/.bashrc or ~/.zshrc)
export PATH="/opt/sacd-tools/bin:$PATH"
```

### User Directory Installation

```bash
# Install to user's local bin
cmake -DCMAKE_INSTALL_PREFIX=$HOME/.local .
make
make install  # No sudo needed

# Add to PATH (add to ~/.bashrc or ~/.zshrc)
export PATH="$HOME/.local/bin:$PATH"
```

## 🔄 Uninstallation

```bash
# From build directory
sudo make uninstall

# Or manually remove
sudo rm /usr/local/bin/sacd_extract
```

## 🖥️ Platform-Specific Instructions

### Linux Build

```bash
cd tools/sacd_extract
cmake -DCMAKE_BUILD_TYPE=Release .
make -j$(nproc)
sudo make install
```

### macOS Build

```bash
cd tools/sacd_extract
cmake -DCMAKE_BUILD_TYPE=Release .
make -j$(sysctl -n hw.ncpu)
sudo make install
```

### Windows Cross-Compilation (Linux → Windows)

```bash
cd tools/sacd_extract
cmake -DMINGW64=YES -DCMAKE_BUILD_TYPE=Release .
make
# Creates sacd_extract.exe
```

## ⚡ Build Options

### CMake Configuration Options

| Option                 | Description               | Example                              |
| ---------------------- | ------------------------- | ------------------------------------ |
| `CMAKE_BUILD_TYPE`     | Build configuration       | `Debug`, `Release`, `RelWithDebInfo` |
| `CMAKE_INSTALL_PREFIX` | Installation directory    | `/usr/local`, `/opt/sacd-tools`      |
| `MINGW64`              | Windows cross-compilation | `YES`, `NO`                          |

### Advanced Configuration

```bash
# Release with debug info (for profiling)
cmake -DCMAKE_BUILD_TYPE=RelWithDebInfo .

# Custom compiler flags
cmake -DCMAKE_C_FLAGS="-march=native -O3" .

# Cross-compilation for Windows
cmake -DMINGW64=YES -DCMAKE_TOOLCHAIN_FILE=path/to/toolchain.cmake .
```

## 🎯 Build Targets

### Available Make Targets

| Target               | Description                   |
| -------------------- | ----------------------------- |
| `make` or `make all` | Build the sacd_extract binary |
| `make clean`         | Remove build artifacts        |
| `make install`       | Install binary to system      |
| `make uninstall`     | Remove installed binary       |

### Build Process Details

1. **Compilation**: C source files compiled with optimizations
2. **Linking**: Static libraries linked into final binary
3. **Stripping**: Debug symbols removed in Release mode (automatic)
4. **Installation**: Binary copied to system PATH

## 🐛 Troubleshooting

### Common Build Issues

#### CMake Version Too Old

```
CMake Error: CMake 3.10 or higher is required
```

**Solution**: Update CMake or use newer version

```bash
# Ubuntu/Debian
sudo apt install cmake

# macOS
brew upgrade cmake
```

#### Missing Dependencies

```
fatal error: iconv.h: No such file or directory
```

**Solution**: Install iconv development headers

```bash
# Ubuntu/Debian
sudo apt install libiconv-hook-dev

# CentOS/RHEL
sudo yum install glibc-devel
```

#### Linker Errors on macOS

```
ld: symbol(s) not found for architecture x86_64
```

**Solution**: Install Xcode Command Line Tools

```bash
xcode-select --install
sudo xcode-select --reset
```

#### Permission Denied During Installation

```
Permission denied: cannot create /usr/local/bin/sacd_extract
```

**Solution**: Use sudo or install to user directory

```bash
sudo make install
# OR
cmake -DCMAKE_INSTALL_PREFIX=$HOME/.local .
```

### Build Verification

#### Check Binary Properties

```bash
# File type and architecture
file sacd_extract

# Size comparison (Release vs Debug)
ls -lh sacd_extract

# Linked libraries
ldd sacd_extract  # Linux
otool -L sacd_extract  # macOS

# Test functionality
./sacd_extract --help
```

#### Performance Verification

```bash
# Quick benchmark (time a simple operation)
time ./sacd_extract -P -i "test.iso"
```

## 💡 Development Tips

### Incremental Builds

```bash
# Only rebuild changed files
make

# Force complete rebuild
make clean && make
```

### Debug Builds for Development

```bash
# Enable debug symbols and disable optimizations
cmake -DCMAKE_BUILD_TYPE=Debug .
make

# Use with debugger
gdb ./sacd_extract
lldb ./sacd_extract  # macOS
```

### Profiling Builds

```bash
# Release with debug info for profiling
cmake -DCMAKE_BUILD_TYPE=RelWithDebInfo .
make

# Profile with tools
valgrind ./sacd_extract [options]
perf record ./sacd_extract [options]  # Linux
```

---

**Next Steps**: After successful build and installation, see [USAGE.md](USAGE.md) for detailed usage instructions and examples.
