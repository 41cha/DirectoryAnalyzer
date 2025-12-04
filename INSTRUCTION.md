# Directory Analyzer – Instructions

This document explains how the program works internally and shows an example of its output.

## How it works

1. The program receives a directory path from the command line.
2. It uses `os.walk()` to recursively traverse all subdirectories and files.
3. For each file it:
   - Counts total files and folders.
   - Determines the file extension and adds the file size to extension statistics.
   - Stores the file path and size for later sorting (top 10 largest files).
   - Reads the file in small chunks and calculates an MD5 hash to detect duplicates.
4. After scanning, the program:
   - Builds a list of the top 10 largest files.
   - Groups files by hash and keeps only hashes that have more than one file (duplicates).
   - Generates a text report with all collected statistics.

## Main functions / methods

- `analyze_directory(path)` or class method `DirectoryAnalyzer.analyze_directory()`  
  Scans the directory recursively and fills all statistics.

- `get_top_files(n=10)`  
  Returns a list of the largest files (path and size).

- `find_duplicates()`  
  Returns groups of files that have identical content.

- `generate_report()`  
  Builds a formatted text report that can be printed or saved.

## Example report (simplified)

Analysis of: /home/user/documents
Files: 1247, Folders: 156

Extensions (total size in bytes):
.jpg: 2456789
.py: 124567
.txt: 45678

Top-10 largest files:
1234567 bytes: images/photo.jpg
987654 bytes: videos/movie.mp4

Duplicates:
Group (2 files):
/home/user/documents/file1.txt
/home/user/documents/copy/file1_copy.txt

## Download

pip install directory-analyzer==0.1.0

## Example of usage

1. from directory_analyzer import DirectoryAnalyzer

2. path = r'C:\directory'
3. analyzer = DirectoryAnalyzer(path)
4. analyzer.analyze_directory()
5. print(analyzer.generate_report())