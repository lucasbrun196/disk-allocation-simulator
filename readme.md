# Disk File Manager

This project implements a disk file manager, simulating memory allocation and management for files. It supports different allocation and management strategies, such as:

- **Contiguous Allocation**
- **Linked Allocation**
- **Indexed Allocation**

## Build and Run

### Requirements
- C++ compiler with **C++11** support or higher.

### Build
Use the following command to compile:

```bash
g++ simulator.cpp -o simulator -Wall
./simulator
```

## Features

1. **File Creation**:
   - Creates files using different allocation strategies.
   - Ensures efficient use of memory blocks.

2. **File Deletion**:
   - Removes files and frees the allocated memory.

3. **Memory Display**:
   - Displays the disk state and memory block usage.

4. **Specific File View**:
   - Details such as name, size, and block location.

5. **Error Handling**:
   - Ensures valid input and provides helpful error messages.

## Data Structures

### `Block` Structure
Represents a block on the disk:
```cpp
struct Block {
    string color;          // Color associated with the file's block
    string file_name;      // File name
    int block_index;       // Block index
    int blocks_length;     // Total number of blocks used by the file
    int start_block;       // Starting block index
    Block *next;           // Pointer to the next block
    set<Block*> nexts_blocks; // Related blocks (indexed allocation)
};
```

### `FileInfo` Structure
Stores information about the file:
```cpp
struct FileInfo {
    string file_name_info;       // File name
    int logic_blocks_num_info;   // Number of logical blocks required
};
```

## Colors
Colors are used to visually identify files. Example mapping:

- `\033[30m`: Black
- `\033[31m`: Red

Other colors are configured in `initColors()`.

---

## Functions

### Initialization
- **`initColors()`**: Initializes the map of available colors.

### File Handling
- **`contiguousFileCreate()`**: Creates files using contiguous allocation.
- **`linkedFileCreate()`**: Creates files using linked allocation.
- **`indexedFileCreate()`**: Creates files using indexed allocation.
- **`contiguousFileDelete()`**: Removes contiguously allocated files.
- **`linkedFileDelete()`**: Removes files allocated with linked allocation.
- **`recursiveDeleteLinkedFile()`**: Frees the deleted file's memory and creates new empty blocks where it was removed.
- **`indexedFileDelete()`**: Removes files allocated with indexed allocation.

### File Descriptor
- **`findInFileDescriptor()`**: Checks whether the file is in the descriptor.
- **`deleteFileInDescriptor()`**: Deletes a file from the descriptor.

### Display
- **`showDiskMemory()`**: Displays the disk memory.
- **`showTableFileInDescriptor()`**: Calls the function that displays disk information, deciding whether to show a specific file or all files.
- **`showBlock()`**: Displays file information.
- **`showSpecificFile()`**: Displays details of a specific file.
- **`showLinkedBlocks()`**: Recursively displays the blocks for the CONTIGUOUS and LINKED algorithms.
- **`showIndexTable()`**: Displays the blocks stored in a file's block table for the INDEXED algorithm.

### Helpers
- **`instructionAllocation()`**: Decides which function to call for each algorithm (C || E || S).
- **`integerTreatment()`**: Validates integer input.
- **`findAvaliableColor()`**: Finds an available color for a file.
- **`findFreeBlocks()`**: Locates free blocks on the disk.
- **`deepCopyVector()`**: Creates a copy of the block vector for display.
- **`deleteDeepCopy()`**: Deletes the copy of the block vector created for display.
- **`cinFileInfo()`**: Reads the input for files to be created.
- **`verifyFileNameToDelete()`**: Checks whether the file to be deleted is valid.
