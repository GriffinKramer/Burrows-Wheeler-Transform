# Burrows-Wheeler-Transform
A from-scratch Python implementation of the Burrows-Wheeler Transform (BWT), inverse BWT, and FM-index pattern matching using a custom Wavelet Tree class.

## Background
 
The Burrows-Wheeler Transform is the algorithmic foundation of widely-used sequence aligners including BWA and Bowtie2. It works by rearranging a string into a form that compresses well and enables efficient substring search via first-last (FL) matching. Understanding BWT from first principles is essential context for anyone working with NGS alignment pipelines.
 
- **Burrows-Wheeler Transform** — generates all rotations of an input string, sorts them, and returns the last column
- **Inverse BWT** — reconstructs the original string from the transform alone
- **Wavelet Tree (`Wtree` class)** — a recursive data structure that enables rank queries on the BWT without storing full rank arrays; implemented to work on arbitrary alphabets, not just DNA
- **First-Last (FL) matching** — uses the Wavelet Tree to count occurrences of a pattern within a reference string efficiently
 
## Motivation
 
Rather than implementing a naive rank array (which would require O(n × alphabet_size) space), this implementation uses a Wavelet Tree to answer rank queries in O(log σ) time, where σ is the alphabet size. The tree is built to optimally balance character distributions at each node, making it generalisable beyond DNA sequences.
 
The connection to real-world tools: Bowtie2 and BWA both use BWT-based FM-indexing for read alignment — the same principle implemented here, at production scale.
 
## Usage
 
Open `BurrowsWheeler.ipynb` in Jupyter and run cells sequentially. The notebook is self-contained with inline explanations of each step.
 
```python
# Example
transform = BurrowsWheeler("AACGT")
# Returns the BWT string
 
count = first_last_matching(transform, "AC")
# Returns number of occurrences of "AC" in original string
```
 
## Author
 
Griffin Kramer
