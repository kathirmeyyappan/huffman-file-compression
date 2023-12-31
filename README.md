# Huffman File Compression Application
#### Desktop application that employs lossless compression methods (Huffman coding!) to zip and unzip files with 100% accuracy. 

#### Supported filetypes: .txt, .csv, .html, .py, .js, .c, .giggitygiggity, and basically ANY text-based file!

## Demonstration
Below is an example use of the tool. We compress ```TESTFILE.giggitygiggity``` into a binary zip file called ```compressed_TESTFILE.giggitygiggity.zip```, <b>which is about 1/93 the size of the original</b> (414 bytes vs 38.6 KB). Then, we unzip (using the decoding algorithm) ```compressed_TESTFILE.giggitygiggity.zip``` into ```decompressed_TESTFILE.giggitygiggity```, which is perfectly identical in size and contents to the original file.

https://github.com/kathirmeyyappan/huffman-file-compression/assets/71161498/66c31dbe-c94e-4034-a6ab-64715c424198

## Methodology
The idea behind lossless compression is that we can re-express data with less information without actually omitting any of it. Typically, in text-based files, one character (as long as it is a "common" enough character) is represented by 1 byte. Using Huffman coding, we can actually encode our data such that one character (on average) is less than a byte!

First, we record the frequency of each character, and contruct a binary tree such that traversals (where right and left correpond to 1 and 0) to leaves each point to a character. This is our key for encoding the data. We write the encoded text data to a binary file along with with binary-ified version of the Huffman tree (for decoding purposes) and zip it up, giving us our compressed file! I also wrote a decoding algorithm to parse the file into the Huffman tree I embedded as well as raw text data.

## Limitations
For very small files, running the Huffman encoding algorithm actually increased size. This is because storing the decoding info (Huffman tree data) within the binary file takes some space, often more than what a very small file may have contained in the first place (a couple hundred bytes).

For files with a large variety of characters (> 2^8), each encoded character will take up more than a byte on average based on our Huffman tree (because that would mean 1 character is more than 8 bits on average). This may not be result in a net increase in file-size per say (because many types of characters would take up 2 or 3 bytes in standard utf-8 encoding), but it has diminishing returns. On the flipside, files with very few unique characters (e.g.. a file with just the letters a, b, and c) get compressed immensely because one character may take up 1 or 2 bits instead of 8.
