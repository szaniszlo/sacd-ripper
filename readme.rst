⚠️  DOCUMENTATION MOVED
========================

This documentation has been restructured and moved to Markdown format for better readability and maintenance.

**Please refer to the new documentation:**

📖 **Main Documentation**
   - `README.md <README.md>`_ - Project overview, features, and quick start
   - `BUILD.md <BUILD.md>`_ - Detailed build and installation instructions  
   - `USAGE.md <USAGE.md>`_ - Comprehensive usage guide and examples

🔗 **Quick Links**
   - Installation: See `BUILD.md <BUILD.md>`_
   - Usage Examples: See `USAGE.md <USAGE.md>`_
   - Project Features: See `README.md <README.md>`_

This file (readme.rst) is kept for compatibility but may be removed in future versions.
Please update your bookmarks and references to use the new Markdown documentation.
  -z, --dsf-nopad                 : Do not zero pad DSF (cannot be used with -t)
  -t, --select-track              : only output selected track(s) (ex. -t 1,5,13)
  -I, --output-iso                : output as RAW ISO
  -w, --concurrent                : Concurrent ISO+DSF/DSDIFF processing mode
  -c, --convert-dst               : convert DST to DSD
  -C, --export-cue                : Export a CUE Sheet
  -i, --input[=FILE]              : set source and determine if "iso" image,
                                    device or server (ex. -i 192.168.1.10:2002)
  -o, --output-dir[=DIR]          : Output directory (ISO output dir for concurrent processing mode)
  -y, --output-dir-conc[=DIR]     : DSF/DSDIFF Output directory for concurrent processing mode
  -P, --print                     : display disc and track information


Usage examples
==============

Extract all stereo tracks in uncompressed DSDIFF from an ISO to /home/user/blah/<album_name>::

    $ sacd_extract -2 -p -c -i"Foo_Bar_RIP.ISO" -o /home/user/blah

Extract all stereo tracks in padding-less DSF files from an ISO to /home/user/blah/<album_name>::

    $ sacd_extract -2 -s -z -i"Foo_Bar_RIP.ISO" -o /home/user/blah

Extract an ISO from a server to /home/user/blah/<album_name>.iso::

    $ sacd_extract -I -i192.168.1.10:2002 -o /home/user/blah

Concurrently extract an ISO file to /home/user/blah/<album_name>.iso and all stereo tracks in DSF to /tmp/blah/<album_name> from a server.::

    $ sacd_extract -I -s -w -z -i192.168.1.10:2002 -o /home/user/blah -y /tmp/blah

Concurrently extract an ISO file to /home/user/blah/<album_name>.iso and all stereo and multi-channel tracks in DSF to /tmp/blah/<album_name> from a server.::

    $ sacd_extract -I -s -w -z -2 -m -i192.168.1.10:2002 -o /home/user/blah -y /tmp/blah


Compilation
===========

Linux::

    $ cd tools/sacd_extract
    $ cmake .
    $ make

Windows binary compilation on Linux using Mingw-w64 preceded by iconv compilation for Mingw-w64::

    $ tar -xzf libiconv-1.15.tar.gz
    $ cd libiconv-1.15
    $ ./configure --host=x86_64-w64-mingw32 --prefix=/usr/x86_64-w64-mingw32 --enable-static
    $ make
    $ sudo make install

    $ cd tools/sacd_extract
    $ cmake -DMINGW64=YES
    $ make

macOS::

    $ xcode-select --install
    $ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
    $ brew install cmake
    $ git clone https://github.com/setmind/sacd-ripper.git
    $ cd sacd-ripper/tools/sacd_extract
    $ cmake .
    $ make

