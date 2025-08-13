# extract-hwp

Python library for extracting text from Korean HWP files (HWP 5.0 and HWPX formats).

## Features

- **Multi-format support**: Both HWP 5.0 (OLE) and HWPX (ZIP/XML) files
- **Password detection**: Detect password-protected files before processing
- **Structured extraction**: Preserve paragraph structure during text extraction
- **Robust error handling**: Defensive handling of corrupted or invalid files
- **Unicode support**: Full support for Korean and multi-language text

## Installation

```bash
pip install extract-hwp
```

## Usage

### Basic Usage

```python
from extract_hwp import extract_text_from_hwp

# Extract text from HWP or HWPX file
text, error = extract_text_from_hwp("document.hwp")
if error is None:
    print(text)
else:
    print(f"Error: {error}")
```

### Format-specific Extraction

```python
from extract_hwp import extract_text_from_hwpx, extract_text_from_hwp5

# HWPX files only
hwpx_text = extract_text_from_hwpx("document.hwpx")

# HWP 5.0 files only
hwp5_text = extract_text_from_hwp5("document.hwp")
```

### Password Detection

```python
from extract_hwp import is_hwp_file_password_protected

if is_hwp_file_password_protected("document.hwp"):
    print("File is password protected.")
else:
    text, error = extract_text_from_hwp("document.hwp")
```

## API Reference

### Core Functions

#### `extract_text_from_hwp(filepath)`

Extract text from HWP/HWPX files (unified interface).

**Parameters:**
- `filepath` (str): Path to HWP or HWPX file

**Returns:**
- `tuple`: (extracted_text, error_message). On success, error_message is None

**Raises:**
- `FileNotFoundError`: File not found
- `PermissionError`: No file access permission
- `ValueError`: Unsupported file format

### Format-specific Functions

#### `extract_text_from_hwpx(hwpx_file_path)`

Extract text from HWPX files.

**Parameters:**
- `hwpx_file_path` (str): Path to HWPX file

**Returns:**
- `str`: Extracted text (empty string on error)

#### `extract_text_from_hwp5(filepath)`

Extract text from HWP 5.0 (OLE) files.

**Parameters:**
- `filepath` (str): Path to HWP file

**Returns:**
- `str`: Extracted text (empty string on error)

### Password Detection Functions

#### `is_hwp_file_password_protected(filepath)`

Check if HWP/HWPX file is password protected.

**Parameters:**
- `filepath` (str): File path to check

**Returns:**
- `bool`: True if password protected, False otherwise

## Supported Formats

### HWP 5.0 (OLE Format)
- Extension: `.hwp`
- Structure: OLE compound document format
- Compression: zlib compression support
- Features: Binary structure analysis for text extraction

### HWPX (ZIP/XML Format)
- Extension: `.hwpx`
- Structure: ZIP archive containing XML documents
- Features: XML parsing for structured text extraction

## Dependencies

- `olefile>=0.46`: HWP 5.0 OLE file processing

## Development

### Development Setup

```bash
# Clone repository
git clone https://github.com/your-username/extract-hwp.git
cd extract-hwp

# Install dependencies
uv sync

# Install with dev dependencies
uv sync --extra dev
```

### Testing

```bash
# Run tests
pytest

# With coverage
pytest --cov=src/extract_hwp
```

### Code Quality

```bash
# Format code
black src/ tests/

# Type checking
mypy src/
```

## License

MIT License - see [LICENSE](LICENSE) file for details.

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for version history.