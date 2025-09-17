# 🗜️ File Compression Tool

A Java-based file compression tool using Huffman coding algorithm. This project demonstrates advanced Java concepts including object-oriented programming, algorithms, and file I/O operations.

## 📋 Table of Contents
- [Features](#-features)
- [How It Works](#-how-it-works)
- [Installation](#-installation)
- [Usage](#-usage)
- [Project Structure](#-project-structure)
- [Examples](#-examples)
- [Technical Details](#-technical-details)
- [Contributing](#-contributing)

## ✨ Features

- **🗜️ File Compression** - Compress any file using Huffman coding
- **📂 File Decompression** - Restore compressed files to original format
- **📊 Statistics** - View compression ratios and space savings
- **📋 File Analysis** - Analyze files for compression potential
- **🧪 Built-in Testing** - Run tests to verify functionality
- **🎯 Multiple Formats** - Works with text files, documents, and binary data

## 🔬 How It Works

The tool uses **Huffman Coding**, a lossless compression algorithm that works by:

1. **Analyzing** the file to count character frequencies
2. **Building** a binary tree where frequent characters get shorter codes
3. **Encoding** the original data using these optimized codes
4. **Saving** both the compressed data and the decoding tree

**Example:**
```
Original text: "AAABBBCCCC" (10 characters = 80 bits)
Huffman codes: A=10, B=0, C=11
Compressed:    "101010000111111" (15 bits ≈ 81% compression)
```

## 🚀 Installation

### Prerequisites
- Java 11 or higher
- Maven 3.6 or higher

### Setup
```bash
# Clone the repository
git clone https://github.com/yourusername/filecompressor.git
cd filecompressor

# Compile the project
mvn clean compile

# Run tests
mvn test

# Build executable JAR
mvn clean package
```

## 💻 Usage

### Command Line Interface
```bash
java -jar target/file-compression-tool-1.0.0.jar <command> <input_file> [output_file]
```

### Available Commands

| Command | Description | Example |
|---------|-------------|---------|
| `compress` | Compress a file | `java -jar tool.jar compress document.txt` |
| `decompress` | Decompress a file | `java -jar tool.jar decompress document.huff` |
| `info` | Show file information | `java -jar tool.jar info document.txt` |
| `test` | Run functionality tests | `java -jar tool.jar test` |

### Quick Start
```bash
# Compress a file
java -jar target/file-compression-tool-1.0.0.jar compress sample.txt

# This creates sample.huff (compressed file)

# Decompress the file  
java -jar target/file-compression-tool-1.0.0.jar decompress sample.huff restored.txt

# View file information
java -jar target/file-compression-tool-1.0.0.jar info sample.txt
```

## 📁 Project Structure

```
src/
├── main/java/io/github/darlene13/filecompressiontool/
│   ├── 📦 models/                     # Data structures
│   │   ├── HuffmanNode.java           # Tree node for Huffman algorithm
│   │   ├── CompressionResult.java     # Compression output container
│   │   └── FileMetadata.java          # Original file information
│   ├── ⚙️ algorithms/                 # Compression algorithms
│   │   ├── CompressionStrategy.java   # Interface for all algorithms
│   │   ├── HuffmanCompressor.java     # Huffman coding implementation
│   │   └── LZWCompressor.java         # Future: LZW algorithm
│   ├── 🛠️ utils/                      # Helper utilities
│   │   ├── BitUtils.java              # Bit manipulation tools
│   │   ├── FileUtils.java             # File I/O operations
│   │   └── MathUtils.java             # Mathematical calculations
│   └── 🚀 FileCompressor.java         # Main application entry point
└── test/java/                         # Unit tests
    └── io/github/darlene13/filecompressiontool/
        └── models/
            └── HuffmanNodeTest.java
```

### Architecture Overview
- **Models** - Define what data looks like (HuffmanNode, CompressionResult)
- **Algorithms** - Define how compression works (Strategy pattern)
- **Utils** - Provide reusable helper functions
- **Main** - Coordinates everything and handles user interaction

## 📖 Examples

### Basic Compression
```bash
# Create a test file
echo "Hello World! This is a test file for compression." > test.txt

# Compress it
java -jar target/file-compression-tool-1.0.0.jar compress test.txt

# Check the results
ls -la test.*
# test.txt      - Original file
# test.huff     - Compressed file
```

### Analyzing Results
```bash
# Get detailed information
java -jar target/file-compression-tool-1.0.0.jar info test.txt

# Example output:
# 📋 File Information: test.txt  
# 📊 Size: 49 B
# 📄 Extension: txt
# 🎲 Entropy: 4.23 bits/byte
# 📈 Compression potential: Good (some patterns)
# 🔤 Unique characters: 23
```

### Compression Statistics
```bash
# After compression, you'll see:
# 📊 Compression Statistics
# ========================
# Original size:    49 B
# Compressed size:  38 B  
# Space saved:      11 B
# Compression ratio: 22.45%
```

## 🔧 Technical Details

### Huffman Algorithm Implementation

1. **Frequency Analysis**
   ```java
   // Count how often each character appears
   Map<Byte, Integer> frequencies = countFrequencies(data);
   ```

2. **Tree Construction**
   ```java
   // Build tree using priority queue (min-heap)
   PriorityQueue<HuffmanNode> queue = new PriorityQueue<>();
   ```

3. **Code Generation**
   ```java
   // Generate binary codes (left=0, right=1)
   Map<Byte, String> codes = generateCodes(root);
   ```

4. **Data Encoding**
   ```java
   // Replace characters with their codes
   String compressedBits = compressData(originalData, codes);
   ```

### Performance Characteristics

| Aspect | Complexity | Notes |
|--------|------------|-------|
| **Time** | O(n log n) | n = number of unique characters |
| **Space** | O(n) | Tree storage + frequency map |
| **Compression Ratio** | Varies | 10-60% typical for text files |

### Best Performance On
- ✅ Text files with repeated characters
- ✅ Source code files
- ✅ Configuration files
- ✅ Files with patterns

### Limited Performance On  
- ❌ Already compressed files (ZIP, JPEG, etc.)
- ❌ Random binary data
- ❌ Very small files (<100 bytes)
- ❌ Files with uniform character distribution

## 🧪 Testing

### Run All Tests
```bash
mvn test
```

### Built-in Application Tests
```bash
# Test core functionality
java -jar target/file-compression-tool-1.0.0.jar test

# Example output:
# 🧪 Running Basic Tests
# ======================
# Test 1: HuffmanNode creation
#   ✅ HuffmanNode test passed
# 
# Test 2: Bit manipulation  
#   ✅ BitUtils test passed
#
# Test 3: Simple compression
#   ✅ Basic compression test passed
```

### Manual Testing
```bash
# Create test files of different types
echo "AAABBBCCCC" > simple.txt          # High compression
echo "ABCDEFGHIJ" > diverse.txt         # Low compression  
dd if=/dev/urandom bs=100 count=1 of=random.bin  # Very low compression

# Test compression on each
for file in simple.txt diverse.txt random.bin; do
    echo "Testing $file:"
    java -jar target/file-compression-tool-1.0.0.jar compress $file
    java -jar target/file-compression-tool-1.0.0.jar info $file
    echo "---"
done
```

## 🎓 Learning Objectives

This project demonstrates:

### Object-Oriented Programming
- **Encapsulation** - Private fields with public methods
- **Inheritance** - CompressionStrategy interface  
- **Polymorphism** - Multiple algorithm implementations
- **Abstraction** - Clear separation of concerns

### Data Structures & Algorithms
- **Binary Trees** - Huffman tree construction
- **Priority Queues** - Min-heap for tree building
- **Hash Maps** - Frequency counting and code lookup
- **Bit Manipulation** - Binary string to byte conversion

### Software Engineering
- **Maven Build System** - Dependency management and building
- **Package Organization** - Logical code structure
- **Unit Testing** - JUnit test cases
- **Documentation** - Comprehensive code comments

### File I/O & Serialization
- **Binary File Operations** - Reading/writing byte arrays
- **Object Serialization** - Saving complex objects to files
- **Error Handling** - Proper exception management

## 🔄 Future Enhancements

### Planned Features
- [ ] **GUI Interface** - User-friendly desktop application
- [ ] **LZW Algorithm** - Alternative compression method
- [ ] **Directory Compression** - Compress entire folders
- [ ] **Progress Bars** - Visual feedback for large files
- [ ] **Batch Processing** - Compress multiple files at once

### Possible Improvements
- [ ] **Multithreading** - Parallel processing for large files
- [ ] **Memory Optimization** - Stream processing for huge files
- [ ] **Compression Profiles** - Optimize for speed vs. ratio
- [ ] **File Type Detection** - Automatic algorithm selection

## 🤝 Contributing

### Development Setup
```bash
# Fork and clone the repository
git clone https://github.com/yourusername/filecompressor.git
cd filecompressor

# Create feature branch
git checkout -b feature/new-algorithm

# Make changes and test
mvn clean test

# Commit and push
git commit -m "Add LZW compression algorithm"
git push origin feature/new-algorithm
```

### Code Style Guidelines
- Use descriptive variable names
- Add JavaDoc comments for public methods
- Follow existing package structure
- Write unit tests for new features
- Keep methods focused and small

### Adding New Algorithms
1. Implement `CompressionStrategy` interface
2. Create corresponding test class
3. Update main application to use new algorithm
4. Add documentation and examples

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👨‍💻 Author

**Darlene Wendie** - [GitHub Profile](https://github.com/darlene13)

## 🙏 Acknowledgments

- **David Huffman** - Creator of Huffman coding algorithm
- **Java Community** - For excellent documentation and libraries
- **Maven** - For simplifying project management

---

## 📚 Additional Resources

### Learning More About Compression
- [Huffman Coding Explained](https://en.wikipedia.org/wiki/Huffman_coding)
- [Information Theory Basics](https://en.wikipedia.org/wiki/Information_theory)
- [Lossless Compression Algorithms](https://en.wikipedia.org/wiki/Lossless_compression)

### Java Development Resources
- [Oracle Java Documentation](https://docs.oracle.com/en/java/)
- [Maven Getting Started](https://maven.apache.org/guides/getting-started/)
- [JUnit 5 User Guide](https://junit.org/junit5/docs/current/user-guide/)

---

*Built with ❤️ as a learning project to master Java and algorithms*