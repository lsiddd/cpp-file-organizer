# File Organizer

A command-line tool written in C++ for organizing files in a directory based on their metadata (creation, modification, or access time) and size. This program allows you to move files into subdirectories categorized by the date of creation/last modification/access time and file size (small, medium, or large).

## Features
- **Organize by file time**: Organize files based on their creation, last modification, or last access time.
- **Size categorization**: Files are categorized into "small", "medium", and "large" based on their size.
- **Dry-run mode**: Preview the actions without actually moving any files.
- **Verbose output**: Provides detailed logs of the operations performed.
- **Metadata-based directory structure**: Moves files into directories based on a combination of their file extension and metadata (time & size).

## Requirements
- **C++17** or later
- **Meson build system** (for build configuration)
- **Linux-based system** with `statx` support (Linux 4.11+)

## Compilation

To compile the program using **Meson**, follow these steps:

### 1. Install Meson and Ninja (if not already installed)

- On **Ubuntu/Debian**:

```bash
sudo apt install meson ninja-build
```

- On **Arch Linux**:

```bash
sudo pacman -S meson ninja
```

- On **macOS** (using Homebrew):

```bash
brew install meson ninja
```

### 2. Build the project

1. **Clone or copy the project** to your local machine.

2. **Navigate to the project directory**:

```bash
cd /path/to/file_organizer
```

3. **Create a build directory** and configure the project with Meson:

```bash
meson setup build
```

4. **Build the project** using Ninja:

```bash
ninja -C build
```

### 3. Install (optional)

To install the program on your system:

```bash
sudo ninja -C build install
```

This will place the executable in the system path, allowing you to run `file_organizer` from anywhere.

## Usage

```bash
./file_organizer [OPTIONS] <source_directory>
```

### Options
- `-h, --help`: Show help message and exit.
- `-v, --verbose`: Enable verbose output (shows detailed information about each operation).
- `-d, --dry-run`: Perform a trial run without making any actual changes.
- `-t, --time [creation|modification|access]`: Specify the time attribute to organize by. Default is `creation`.
- `--small <size_in_MB>`: Set the size threshold for "small" files (default: 1 MB).
- `--medium <size_in_MB>`: Set the size threshold for "medium" files (default: 10 MB).

### Examples

1. **Organize files by default (creation time)**:
   ```bash
   ./file_organizer -v /path/to/source
   ```

2. **Organize files by modification time, with custom size thresholds and dry-run**:
   ```bash
   ./file_organizer --dry-run --time modification --small 2 --medium 20 /path/to/source
   ```

3. **Organize files by access time without verbose output**:
   ```bash
   ./file_organizer --time access /path/to/source
   ```

## How It Works

1. **Metadata Collection**: The program collects all files recursively from the source directory and retrieves their metadata (size and time attributes).
   
2. **File Categorization**: Based on the file size and time attribute chosen by the user, the program categorizes the files into directories structured by:
   - Year/Month/Day (based on creation, modification, or access date).
   - File size (small, medium, or large).
   
3. **File Movement**: The program moves files into the appropriate directories. If files already exist in the target directory, it checks for file content differences to avoid overwriting.

4. **Dry-run**: In dry-run mode, no files are actually moved; instead, the program prints out what it would do without making changes.

5. **Verbose Logging**: When enabled, the program logs detailed information about every file processed and directory created.

## Directory Structure

Files are organized into directories like this:

```
<source_directory>/<file_extension>/<year>/<month>/<day>/<size_category>/<file_name>
```

For example, a file named `example.txt` with the creation date of `2024-12-06` and a size of 5 MB would be moved into a directory structure like:

```
<source_directory>/txt/2024/12/06/medium/example.txt
```

## Error Handling
- The program handles errors such as missing permissions, invalid directories, and failed file moves gracefully, providing clear error messages.
- It also checks for the existence of the target directory and handles file conflicts by renaming files if necessary.

## License
Idk just use if if you want i guess. QUEM SOU EU PRA IMPEDIR NE
