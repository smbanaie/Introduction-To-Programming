# Text Encoding Standards: From ASCII to Unicode

## The Evolution of Text Encoding

Text encoding has evolved from simple 7-bit ASCII to comprehensive Unicode systems that support every writing system in the world.

## ASCII: The Beginning

### Historical Context
- **Created**: 1963 by ANSI committee
- **Purpose**: Standardize teleprinter communication
- **Design**: 7 bits for reliability, 1 bit for error checking
- **Coverage**: 128 characters (95 printable, 33 control)

### ASCII Character Set
```
0-31: Control characters (null, bell, backspace, etc.)
32: Space
33-47: !"#$%&'()*+,-./
48-57: 0123456789
58-64: :;<=>?@
65-90: ABCDEFGHIJKLMNOPQRSTUVWXYZ
91-96: [\]^_`
97-122: abcdefghijklmnopqrstuvwxyz
123-126: {|}~
127: Delete
```

### ASCII Properties
- **Fixed width**: 7 bits per character
- **US-centric**: Only English and basic symbols
- **Efficient**: Minimal space usage
- **Universal**: Same on all ASCII-compatible systems

## Extended ASCII Variants

### 8-Bit ASCII
- **Extended range**: 128-255 (additional 128 characters)
- **Backwards compatible**: First 128 same as 7-bit ASCII
- **Problem**: Multiple incompatible variants

### Code Page Systems
Different regions created their own extensions:
- **CP437**: Original IBM PC character set
- **CP1252**: Windows Western European
- **ISO-8859-1**: Internet standard for Western European
- **KOI8-R**: Russian character set

### Problems with Extended ASCII
- **Incompatibility**: Same byte meant different characters
- **Limited coverage**: Still couldn't represent all languages
- **Web issues**: Documents looked wrong on different systems

## The Unicode Revolution

### Unicode Creation
- **Started**: 1987 by Xerox and Apple engineers
- **Goal**: Universal character encoding
- **Current version**: Unicode 15.0 (September 2022)
- **Coverage**: 149,186 characters across 161 scripts

### Unicode Design Principles
- **Universal**: Every character in every language
- **Unique**: One code point per character
- **Logical**: Related characters have related codes
- **Efficient**: Common characters use fewer bytes

### Unicode Character Properties
Each Unicode character has:
- **Code point**: Unique identifier (U+0041 for 'A')
- **Name**: LATIN CAPITAL LETTER A
- **Category**: Letter, number, punctuation, etc.
- **Script**: Latin, Arabic, Devanagari, etc.
- **Block**: Range of related characters

## Unicode Transformation Formats

### UTF-8: The Dominant Format

#### Design
- **Variable length**: 1-4 bytes per character
- **ASCII compatible**: ASCII characters unchanged
- **Self-synchronizing**: Can find boundaries anywhere
- **Internet standard**: 95%+ of web pages

#### Byte Distribution
```
1 byte:  U+0000 to U+007F (ASCII, 0xxxxxxx)
2 bytes: U+0080 to U+07FF (110xxxxx 10xxxxxx)
3 bytes: U+0800 to U+FFFF (1110xxxx 10xxxxxx 10xxxxxx)
4 bytes: U+10000 to U+10FFFF (11110xxx 10xxxxxx 10xxxxxx 10xxxxxx)
```

#### UTF-8 Examples
```
A:  01000001 (1 byte, same as ASCII)
é:  11000011 10101001 (2 bytes)
中: 11100100 10111000 10101101 (3 bytes)
🎵: 11110000 10011111 10001110 10110101 (4 bytes)
```

### UTF-16: Windows Standard

#### Design
- **Variable length**: 2 or 4 bytes per character
- **BMP optimization**: Most characters in 2 bytes
- **Byte order mark**: Detects endianness
- **Windows internal**: Used by Windows OS and Java

#### UTF-16 Structure
```
2 bytes: U+0000 to U+FFFF (most characters)
4 bytes: U+10000 to U+10FFFF (surrogate pairs)
```

### UTF-32: Fixed Width

#### Design
- **Fixed length**: 4 bytes per character
- **Simple**: Direct mapping from code points
- **Space wasteful**: 4 bytes even for ASCII
- **Rarely used**: Too inefficient for most applications

## Encoding Detection and BOM

### Byte Order Mark (BOM)
Special sequence at file start:
```
UTF-8:    EF BB BF
UTF-16BE: FE FF
UTF-16LE: FF FE
UTF-32BE: 00 00 FE FF
UTF-32LE: FF FE 00 00
```

### Automatic Detection
- **Browser heuristics**: Guess encoding from content
- **Library functions**: chardet, cchardet
- **Metadata**: HTTP headers, XML declarations

## Character Properties and Categories

### Unicode Categories
```
Letter: Lu (uppercase), Ll (lowercase), Lt (titlecase), Lm (modifier), Lo (other)
Mark: Mn (nonspacing), Mc (spacing combining), Me (enclosing)
Number: Nd (decimal digit), Nl (letter-like), No (other)
Punctuation: Pc (connector), Pd (dash), Ps (open), Pe (close), Pi (initial), Pf (final), Po (other)
Symbol: Sm (math), Sc (currency), Sk (modifier), So (other)
Separator: Zs (space), Zl (line), Zp (paragraph)
Other: Cc (control), Cf (format), Cs (surrogate), Co (private use), Cn (not assigned)
```

### Normalization Forms
Different ways to represent same text:
- **NFC**: Composed (é = U+00E9)
- **NFD**: Decomposed (é = U+0065 U+0301)
- **NFKC/NFKD**: Compatibility forms

## International Text Issues

### Text Direction
- **LTR**: Left-to-right (English, Spanish, German)
- **RTL**: Right-to-left (Arabic, Hebrew, Persian)
- **BiDi**: Mixed directional text

### Line Breaking
Different languages break lines differently:
- **English**: Break on spaces
- **Chinese/Japanese**: Can break anywhere
- **Thai**: Complex rules for syllable boundaries

### Collation (Sorting)
Language-specific sorting rules:
- **English**: A, B, C (alphabetical)
- **German**: Ä sorts with A
- **Swedish**: W, V, X, Y, Z, Å, Ä, Ö

## Implementation in Programming Languages

### Python Unicode Support
```python
# Strings are Unicode by default (Python 3)
text = "Hello, 世界, سلام"
print(len(text))  # 15 characters

# Encode to bytes
utf8_bytes = text.encode('utf-8')
print(len(utf8_bytes))  # 21 bytes

# Decode back
decoded = utf8_bytes.decode('utf-8')
```

### JavaScript Unicode
```javascript
// Strings are UTF-16
let text = "Hello, 世界";
console.log(text.length);  // 9 (each Chinese char = 2 code units)

// Code points vs code units
console.log([...text].length);  // 8 (actual characters)
```

### C/C++ Unicode
```cpp
// Requires explicit Unicode handling
std::string utf8 = u8"Hello, 世界";
std::u16string utf16 = u"Hello, 世界";
std::u32string utf32 = U"Hello, 世界";
```

## Common Encoding Problems

### Mojibake (Garbled Text)
Wrong encoding interpretation:
```
UTF-8 bytes: c3 a9 (é)
Latin-1: Ã© (two characters)
```

### Character Corruption
Splitting multi-byte sequences:
```
"café" UTF-8: 63 61 66 c3 a9
Truncated: 63 61 66 c3 → "cafÃ"
```

### Mixed Encoding Files
Files with inconsistent encoding:
```
ASCII + UTF-8 = corruption
Windows-1252 + UTF-8 = garbage
```

## Best Practices

### Always Specify Encoding
```python
# Good
with open('file.txt', 'r', encoding='utf-8') as f:
    text = f.read()

# Bad - system dependent
with open('file.txt', 'r') as f:
    text = f.read()
```

### Use UTF-8 Everywhere
- **Web standard**: 95%+ of websites
- **ASCII compatible**: Existing text works
- **Space efficient**: Variable length saves space
- **Universal support**: All modern systems

### Handle Errors Gracefully
```python
try:
    with open('file.txt', 'r', encoding='utf-8') as f:
        text = f.read()
except UnicodeDecodeError:
    # Try alternative encodings
    for encoding in ['latin-1', 'cp1252', 'utf-16']:
        try:
            with open('file.txt', 'r', encoding=encoding) as f:
                text = f.read()
            break
        except UnicodeDecodeError:
            continue
```

## Future of Text Encoding

### Unicode Expansion
- **New scripts**: Support for ancient and constructed languages
- **Emoji evolution**: From simple to complex emoji sequences
- **Symbol expansion**: Mathematical, technical, and decorative symbols

### Beyond Unicode
- **ISO 10646**: Universal character set standard
- **Private use areas**: Custom character assignments
- **Ideographic variation**: Different glyphs for same character

## Key Takeaways

1. **ASCII was limited**: 128 characters for English only
2. **Unicode provides universality**: 149,000+ characters for all languages
3. **UTF-8 is the standard**: Efficient, compatible, dominant on web
4. **Encoding matters**: Wrong encoding corrupts text
5. **Always specify encoding**: Prevents platform-dependent issues

## Further Reading
- Unicode Standard documentation (unicode.org)
- Character encoding tutorials and guides
- Internationalization (i18n) best practices
- Text processing library documentation