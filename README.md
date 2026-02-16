# SACD Ripper - sacd_extract

[![License](https://img.shields.io/badge/License-BSD%203--Clause-blue.svg)](https://opensource.org/licenses/BSD-3-Clause)
[![Build Status](https://img.shields.io/badge/Build-Passing-brightgreen.svg)]()

A powerful command-line tool for extracting Super Audio CD (SACD) content to various formats including DSF, DSDIFF, and ISO.

## 🚀 Features

This fork focuses on improvements to `sacd_extract` with the following enhanced features:

### **Enhanced Audio Processing**

- **🔇 Padding-less DSF generation** (`-z`): Eliminates zero-padding for seamless track transitions
- **⚡ Concurrent ISO+DSF/DSDIFF processing** (`-w`): Process multiple formats simultaneously for maximum efficiency
- **🎵 Dual extraction**: Extract both stereo (`-2`) and multi-channel (`-m`) tracks in one pass

### **Advanced Output Control**

- **📁 Flexible output directories** (`-o`, `-y`): Specify separate directories for different formats
- **🏷️ Enhanced ID3v2 metadata**: TSRC (ISRC), TPUB (Publisher), TCOP (Copyright), TCOM (Composer), TPE2 (Album Artist)
- **📄 Multiple export formats**: DSF, DSDIFF, DSDIFF Edit Master, RAW ISO

### **Performance Optimizations**

- **🚀 Compiler optimizations**: ~3x speed boost for DST decoding on Linux/macOS
- **🧵 Aggressive multithreading**: Parallel raw read and DST decoding
- **⚙️ Cross-platform support**: Linux, macOS, and Windows (via Mingw-w64)

## 📋 Quick Start

### Prerequisites

- **Linux/macOS**: GCC/Clang, CMake 3.10+
- **Windows**: Mingw-w64 toolchain
- **macOS**: Xcode Command Line Tools, Homebrew (for CMake)

### Installation

```bash
# Clone the repository
git clone https://github.com/szaniszlo/sacd-ripper.git
cd sacd-ripper

# Build and install (see tools/sacd_extract/BUILD.md for detailed instructions)
cd tools/sacd_extract
cmake -DCMAKE_BUILD_TYPE=Release .
make
sudo make install
```

### Basic Usage

```bash
# Extract stereo tracks as DSF files
sacd_extract -2 -s -i "album.iso"

# Extract with padding-less DSF for seamless playback
sacd_extract -2 -s -z -i "album.iso" -o /output/directory

# Concurrent ISO + DSF extraction from server
sacd_extract -I -s -w -z -2 -i 192.168.1.10:2002 -o /iso/dir -y /dsf/dir

# Extract both stereo and multi-channel tracks
sacd_extract -2 -m -s -i "album.iso"
```

## 🎛️ Command Line Options

| Option                        | Description                                    |
| ----------------------------- | ---------------------------------------------- |
| `-2, --2ch-tracks`            | Export stereo tracks (default)                 |
| `-m, --mch-tracks`            | Export multi-channel tracks                    |
| `-s, --output-dsf`            | Output as Sony DSF files                       |
| `-p, --output-dsdiff`         | Output as Philips DSDIFF files                 |
| `-e, --output-dsdiff-em`      | Output as DSDIFF Edit Master                   |
| `-I, --output-iso`            | Output as RAW ISO                              |
| `-z, --dsf-nopad`             | Padding-less DSF (cannot be used with `-t`)    |
| `-w, --concurrent`            | Concurrent ISO+DSF/DSDIFF processing           |
| `-c, --convert-dst`           | Convert DST to DSD                             |
| `-C, --export-cue`            | Export CUE sheet                               |
| `-t, --select-track`          | Select specific tracks (e.g., `-t 1,5,13`)     |
| `-i, --input[=FILE]`          | Set input source (ISO, device, or server)      |
| `-o, --output-dir[=DIR]`      | Output directory (ISO dir for concurrent mode) |
| `-y, --output-dir-conc[=DIR]` | DSF/DSDIFF directory for concurrent mode       |
| `-P, --print`                 | Display disc and track information             |

## 📚 Examples

### Basic Extraction

```bash
# Extract all stereo tracks as uncompressed DSDIFF
sacd_extract -2 -p -c -i "Foo_Bar_RIP.ISO" -o /home/user/music

# Extract as padding-less DSF files
sacd_extract -2 -s -z -i "Foo_Bar_RIP.ISO" -o /home/user/music
```

### Server Extraction

```bash
# Extract ISO from network server
sacd_extract -I -i 192.168.1.10:2002 -o /home/user/iso

# Concurrent extraction from server
sacd_extract -I -s -w -z -2 -m -i 192.168.1.10:2002 -o /iso/dir -y /dsf/dir
```

### Advanced Usage

```bash
# Extract specific tracks only
sacd_extract -2 -s -t 1,3,7 -i "album.iso" -o /output

# Display disc information without extraction
sacd_extract -P -i "album.iso"

# Extract with CUE sheet generation
sacd_extract -2 -s -C -i "album.iso" -o /output
```

## 📖 Documentation

- **[BUILD.md](tools/sacd_extract/BUILD.md)** - Detailed build and installation instructions
- **[USAGE.md](tools/sacd_extract/USAGE.md)** - Comprehensive usage guide and examples

## 🔧 Development

This software is primarily developed on Linux with functionality verified on Windows and macOS. Windows builds require Mingw-w64 (Visual Studio is no longer supported).

## 📄 License

```
DISCLAIMER: THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
"AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO,
THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE
FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
```

## 🔗 Links

- **Original Project**: [sacd-ripper/sacd-ripper](https://github.com/sacd-ripper/sacd-ripper)
- **This Fork**: [szaniszlo/sacd-ripper](https://github.com/szaniszlo/sacd-ripper)

---

_This is a fork focused on improving sacd_extract functionality. For original release information, refer to the upstream project._
