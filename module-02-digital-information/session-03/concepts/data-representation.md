# Data Representation: How Information Becomes Digital

## The Digital Transformation

All information in computers - whether text, images, sound, or video - must be converted to digital form. This process of **data representation** is fundamental to computing.

## Why Digital Representation?

### Advantages Over Analog
- **Precision**: Exact values, no loss from copying
- **Reliability**: Can detect and correct errors
- **Processing**: Easy to manipulate with algorithms
- **Storage**: Compact and durable
- **Transmission**: Reliable over long distances

### The Sampling Principle
Analog signals are continuous; digital is discrete:
- **Sample**: Take measurements at regular intervals
- **Quantize**: Convert measurements to discrete values
- **Encode**: Represent values as binary numbers

## Representing Different Data Types

### Numbers

#### Integers
Direct binary representation:
```
Decimal 42 → Binary 101010 → Hex 2A
Decimal 255 → Binary 11111111 → Hex FF
```

#### Floating Point Numbers
Special format for decimals:
```
Sign (1 bit) + Exponent (8 bits) + Mantissa (23 bits)
Example: 3.14159 → Special binary encoding
```

### Text

#### ASCII (American Standard Code)
7 bits per character (128 characters):
```
'A' = 01000001 (decimal 65)
'B' = 01000010 (decimal 66)
'Hello' = 01001000 01100101 01101100 01101100 01101111
```

#### Unicode
Up to 32 bits per character (global support):
```
English 'A' = U+0041 (same as ASCII)
Arabic 'ا' = U+0627
Emoji 😀 = U+1F600
Chinese '中' = U+4E2D
```

### Images

#### Bitmap Images
Each pixel is a color value:
```
Pixel format: RGB (Red, Green, Blue)
Each color: 8 bits (0-255)
Total per pixel: 24 bits
Image size: width × height × bits_per_pixel
```

#### Vector Images
Mathematical descriptions of shapes:
```
Line: start_point, end_point, thickness, color
Circle: center_point, radius, fill_color, border
Stored as: Binary-encoded mathematical formulas
```

### Sound

#### Digital Audio
- **Sample rate**: Measurements per second (44,100 Hz for CD quality)
- **Bit depth**: Precision per sample (16 bits for CD)
- **Channels**: Mono (1) or stereo (2)
- **File size**: sample_rate × bit_depth × channels × duration

```
CD Quality: 44,100 × 16 × 2 = 1,411,200 bits/second
3-minute song: ~304 MB
```

### Video

#### Digital Video
Combination of images over time:
```
Frame rate: 30 frames per second
Resolution: 1920×1080 pixels
Color depth: 24 bits per pixel
Data rate: frame_rate × width × height × color_depth

HD Video (1080p): ~1.5 billion bits/second
```

## Data Compression

### Why Compress?
- **Storage efficiency**: Reduce file sizes
- **Transmission speed**: Faster downloads/uploads
- **Cost reduction**: Less storage space needed

### Lossless Compression
No data loss - can perfectly reconstruct original:
- **Run-length encoding**: RRR → 3R
- **Dictionary methods**: Replace repeated patterns
- **Examples**: ZIP, PNG, FLAC

### Lossy Compression
Accept some quality loss for better compression:
- **Perceptual coding**: Remove inaudible/ invisible data
- **Examples**: JPEG, MP3, MPEG

## Data Structures

### Arrays
Contiguous memory blocks:
```
[10, 20, 30, 40] → Stored in sequential memory locations
Access: array[index] → instant lookup
```

### Linked Lists
Elements connected by pointers:
```
Node1 → Node2 → Node3 → null
Each node: [data, pointer_to_next]
```

### Trees
Hierarchical structures:
```
Root
├── Branch1
│   ├── Leaf1
│   └── Leaf2
└── Branch2
    └── Leaf3
```

### Hash Tables
Key-value mappings:
```
"Alice" → 95
"Bob" → 87
Fast lookup by key using hash functions
```

## File Formats

### Text Files
Human-readable text:
- **Plain text**: .txt files
- **Markup**: HTML, XML, Markdown
- **Configuration**: JSON, YAML, INI

### Binary Files
Machine-readable data:
- **Executables**: .exe, .app, .bin
- **Libraries**: .dll, .so, .dylib
- **Databases**: Custom binary formats
- **Media**: Compressed audio/video

### Structured Formats
Self-describing data:
- **JSON**: JavaScript Object Notation
- **XML**: Extensible Markup Language
- **Protocol Buffers**: Google's binary format

## Encoding and Decoding

### Character Encoding
Converting characters to bytes:
```python
# UTF-8 encoding
text = "Hello"
bytes = text.encode('utf-8')  # b'Hello'
decoded = bytes.decode('utf-8')  # "Hello"
```

### Serialization
Converting objects to storable format:
```python
# Python object to JSON
import json
data = {"name": "Alice", "age": 25}
json_string = json.dumps(data)  # '{"name": "Alice", "age": 25}'
restored = json.loads(json_string)  # Back to dictionary
```

## Endianness

### What is Endianness?
Order of storing multi-byte values:
- **Big-endian**: Most significant byte first
- **Little-endian**: Least significant byte first

### Example
```
Number: 1025 (decimal) = 00000100 00000001 (binary)
Big-endian:    04 01
Little-endian: 01 04
```

### Why It Matters
- **Compatibility**: Different systems use different endianness
- **Network protocols**: Usually big-endian
- **x86 processors**: Little-endian
- **ARM processors**: Can be either

## Data Integrity

### Checksums
Verify data hasn't changed:
- **Simple**: Sum of all bytes
- **CRC**: Cyclic redundancy check
- **Hash functions**: MD5, SHA-256

### Error Detection
Find corrupted data:
- **Parity bits**: Simple error detection
- **Hamming codes**: Error correction
- **Reed-Solomon**: Advanced error correction

## Real-World Applications

### Databases
- **Tables**: Rows and columns of data
- **Indexes**: Fast lookup structures
- **Transactions**: Reliable multi-step operations

### Networking
- **Packets**: Structured data for transmission
- **Protocols**: Rules for data exchange
- **Encryption**: Secure data representation

### Multimedia
- **Codecs**: Compress/decompress audio/video
- **Containers**: Combine multiple data streams
- **Streaming**: Real-time data transmission

## Key Takeaways

1. **All data becomes digital**: Analog information is sampled and quantized
2. **Different types need different representations**: Numbers, text, images, sound all have optimal formats
3. **Compression balances size and quality**: Lossless vs lossy approaches
4. **Data structures enable efficient operations**: Arrays, trees, hash tables for different needs
5. **File formats standardize representation**: Enable interoperability between systems

## Further Reading
- Study specific file formats (JPEG, MP3, MP4)
- Learn about data compression algorithms
- Explore database storage techniques
- Understand network protocol data formats