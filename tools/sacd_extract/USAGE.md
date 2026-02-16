# Usage Guide - sacd_extract

This guide provides comprehensive usage instructions, examples, and best practices for `sacd_extract`.

## 🎵 Input Sources

### ISO Files

Most common usage - extract from SACD ISO image files:

```bash
sacd_extract -i "album.iso" [options]
sacd_extract -i "/path/to/album.iso" [options]
```

### Network Servers

Extract directly from SACD ripping servers:

```bash
sacd_extract -i 192.168.1.10:2002 [options]
sacd_extract -i server.domain.com:2002 [options]
```

### Physical Devices

Direct access to SACD drives (Linux/Unix):

```bash
sacd_extract -i /dev/cdrom [options]
sacd_extract -i /dev/sr0 [options]
```

## 📁 Output Formats

### Sony DSF Format

High-quality DSD audio format supported by most DSD-capable players:

```bash
# Basic DSF extraction (stereo tracks)
sacd_extract -2 -s -i "album.iso"

# DSF with padding elimination (recommended for gapless playback)
sacd_extract -2 -s -z -i "album.iso"

# DSF with custom output directory
sacd_extract -2 -s -i "album.iso" -o "/output/directory"
```

### Philips DSDIFF Format

Professional DSD format with excellent metadata support:

```bash
# Standard DSDIFF
sacd_extract -2 -p -i "album.iso"

# DSDIFF Edit Master (enhanced format)
sacd_extract -2 -e -i "album.iso"

# DSDIFF with DST decompression
sacd_extract -2 -p -c -i "album.iso"
```

### RAW ISO Format

Creates bit-perfect ISO image of the SACD:

```bash
# Extract complete ISO
sacd_extract -I -i server:2002 -o "/iso/directory"
```

## 🎛️ Channel Configuration

### Stereo Tracks (2-channel)

```bash
# Extract stereo tracks only (default behavior)
sacd_extract -2 -s -i "album.iso"
```

### Multi-channel Tracks (5.1/6-channel)

```bash
# Extract multi-channel tracks only
sacd_extract -m -s -i "album.iso"
```

### Both Stereo and Multi-channel

```bash
# Extract both formats in one pass (recommended)
sacd_extract -2 -m -s -i "album.iso"
```

## 🚀 Advanced Features

### Concurrent Processing

Process multiple output formats simultaneously for maximum efficiency:

```bash
# Concurrent ISO + DSF extraction
sacd_extract -I -s -w -z -i server:2002 -o "/iso/dir" -y "/dsf/dir"

# Concurrent with both stereo and multi-channel
sacd_extract -I -s -w -z -2 -m -i server:2002 -o "/iso/dir" -y "/dsf/dir"
```

**Benefits:**

- Significantly faster than sequential processing
- ISO extraction is CPU-light while DSF/DSDIFF is CPU-heavy
- Overall time ≈ max(ISO_time, DSF_time) instead of ISO_time + DSF_time

### Padding-less DSF (`-z`)

Eliminates zero-padding between tracks for gapless playback:

```bash
# Standard DSF (with padding)
sacd_extract -2 -s -i "album.iso"

# Padding-less DSF (recommended for gapless albums)
sacd_extract -2 -s -z -i "album.iso"
```

**Important Notes:**

- Cannot be combined with `-t` (track selection)
- Requires processing entire album continuously
- Recommended for classical music, concept albums, DJ mixes

### Selective Track Extraction

Extract only specific tracks:

```bash
# Extract tracks 1, 5, and 13
sacd_extract -2 -s -t 1,5,13 -i "album.iso"

# Extract track range (if supported)
sacd_extract -2 -s -t 3,4,5,6,7 -i "album.iso"
```

## 📋 Complete Usage Examples

### Basic Album Extraction

```bash
# Simple stereo DSF extraction
sacd_extract -2 -s -i "Mozart_Symphonies.iso" -o "/music/Mozart"

# High-quality DSDIFF with decompression
sacd_extract -2 -p -c -i "Jazz_Album.iso" -o "/music/Jazz"

# Both stereo and surround with gapless DSF
sacd_extract -2 -m -s -z -i "Pink_Floyd.iso" -o "/music/Progressive"
```

### Server-based Extraction

```bash
# Extract ISO from network server
sacd_extract -I -i 192.168.1.100:2002 -o "/backups/sacd"

# Extract tracks directly from server to DSF
sacd_extract -2 -s -z -i 192.168.1.100:2002 -o "/music/new_albums"

# Full concurrent extraction from server
sacd_extract -I -s -w -z -2 -m -i music.server.com:2002 -o "/iso" -y "/music"
```

### Professional Workflow

```bash
# Archive: Create ISO backup + extract music files
sacd_extract -I -s -w -c -2 -m -i server:2002 -o "/archive/iso" -y "/music/library"

# Preview: Check disc information before extraction
sacd_extract -P -i "unknown_album.iso"

# Selective: Extract only best tracks with CUE sheet
sacd_extract -2 -s -z -C -t 1,3,7,12 -i "compilation.iso" -o "/music/best_of"
```

## 🎯 Optimization Tips

### Performance Optimization

#### CPU Usage

- Use `-w` (concurrent mode) when extracting multiple formats
- Multi-channel extraction is more CPU intensive than stereo
- DST decompression (`-c`) is CPU-heavy but provides better quality

#### Storage Optimization

- DSF files: ~6MB per minute (stereo), ~18MB per minute (5.1)
- DSDIFF files: Similar to DSF, better metadata support
- Use `-z` for slightly smaller DSF files with no quality loss

#### Network Extraction

```bash
# Optimize network extraction with concurrent processing
sacd_extract -I -s -w -z -2 -i server:2002 -o "/fast/ssd" -y "/slower/hdd"
```

### Quality Settings

#### Maximum Quality

```bash
# Uncompressed DSDIFF with full metadata
sacd_extract -2 -m -e -c -C -i "audiophile.iso" -o "/audiophile/collection"
```

#### Balanced Quality/Size

```bash
# Padding-less DSF (good quality, reasonable size)
sacd_extract -2 -m -s -z -i "album.iso" -o "/music/library"
```

#### Space-Efficient

```bash
# Compressed DSDIFF (smaller files)
sacd_extract -2 -p -i "album.iso" -o "/music/mobile"
```

## 📊 Output Directory Structure

### Default Structure

```
Output Directory/
├── Album Name/
│   ├── 01 - Track Name.dsf
│   ├── 02 - Track Name.dsf
│   ├── ...
│   └── folder.jpg (if available)
```

### Multi-channel Structure

```
Output Directory/
├── Album Name/
│   ├── Stereo/
│   │   ├── 01 - Track Name.dsf
│   │   └── ...
│   └── Multi-channel/
│       ├── 01 - Track Name.dsf
│       └── ...
```

### Concurrent Mode Structure

```
ISO Directory/
└── Album Name.iso

DSF Directory/
└── Album Name/
    ├── 01 - Track Name.dsf
    └── ...
```

## 🛠️ Troubleshooting

### Common Issues

#### "Cannot open input file"

```bash
# Check file exists and is readable
ls -la "album.iso"
file "album.iso"

# Try absolute path
sacd_extract -2 -s -i "/full/path/to/album.iso"
```

#### "Output directory does not exist"

```bash
# Create output directory first
mkdir -p "/output/directory"
sacd_extract -2 -s -i "album.iso" -o "/output/directory"
```

#### "Server connection failed"

```bash
# Test server connectivity
ping server_ip
telnet server_ip 2002

# Try with explicit port
sacd_extract -2 -s -i "server_ip:2002"
```

#### Incomplete extractions

```bash
# Check disc information first
sacd_extract -P -i "album.iso"

# Verify input file integrity
md5sum "album.iso"
```

### Performance Issues

#### Slow extraction

```bash
# Use concurrent mode
sacd_extract -I -s -w -2 -i "album.iso" -o "/iso" -y "/music"

# Check available CPU cores
nproc  # Linux
sysctl -n hw.ncpu  # macOS
```

#### Out of disk space

```bash
# Check available space
df -h /output/directory

# Estimate space requirements (SACD ≈ 4-6 GB as DSF)
du -sh "album.iso"
```

## 📝 Metadata and Tagging

### ID3v2 Tags Included

- **Basic**: Title, Artist, Album, Track Number, Year
- **Extended**: ISRC (TSRC), Publisher (TPUB), Copyright (TCOP)
- **Advanced**: Composer (TCOM), Album Artist (TPE2)

### CUE Sheet Generation

```bash
# Generate CUE sheet with extraction
sacd_extract -2 -s -C -i "album.iso" -o "/music/with_cue"
```

## 🎵 Format Recommendations

### By Use Case

| Use Case          | Recommended Format | Command             |
| ----------------- | ------------------ | ------------------- |
| **Archival**      | ISO + DSDIFF       | `-I -e -w -c -2 -m` |
| **Music Library** | Padding-less DSF   | `-2 -m -s -z`       |
| **Audiophile**    | DSDIFF Edit Master | `-2 -m -e -c -C`    |
| **Portable**      | Compressed DSF     | `-2 -s`             |
| **Quick Preview** | Stereo DSF         | `-2 -s -t 1,3,5`    |

### By Player Compatibility

| Player Type             | Recommended Format         |
| ----------------------- | -------------------------- |
| **Foobar2000, JRiver**  | DSF or DSDIFF              |
| **Audirvana, HQPlayer** | DSDIFF Edit Master         |
| **Mobile Players**      | DSF (better compatibility) |
| **Professional DAWs**   | DSDIFF Edit Master         |

---

**Need Help?** Check [BUILD.md](BUILD.md) for installation issues or refer to the original [sacd-ripper documentation](https://github.com/sacd-ripper/sacd-ripper) for advanced topics.
