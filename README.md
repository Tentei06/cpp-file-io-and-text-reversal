# C++ File I/O and Text Reversal

A C++ console application developed for **CSC450 — Programming III** at Colorado State University Global.

This project demonstrates user input, file input/output operations, appending data to an existing file, and reversing text using fundamental C++ string manipulation and file-handling techniques.

## Project Overview

The application prompts the user to enter a line of text and appends that input to an existing text file without overwriting its contents.

After appending the new text, the program reads the complete file, reverses its characters, and saves the reversed contents to a separate output file.

The assignment focuses on:

- Accepting user input using `getline()`
- Reading and writing text files
- Appending data using `ios::app`
- Working with `ifstream` and `ofstream`
- Processing file contents character by character
- Reversing strings using a loop
- Handling basic file-opening errors
- Preserving existing file contents

## Technologies Used

- **C++** — Programming language
- **C++ Standard Library** — File streams, strings, and console input/output
- **Visual Studio Code** — Development environment
- **MSYS2 / MinGW-w64** — C++ compiler toolchain
- **Git and GitHub** — Version control and documentation

## Project Structure

```text
cpp-file-io-and-text-reversal/
├── CSC450_CT5_UserInput.cpp
├── CSC450_CT5_mod5.txt
├── CSC450-mod5-reverse.txt
├── .gitignore
├── LICENSE
└── README.md
```

### Project Files

| File | Purpose |
|------|---------|
| `CSC450_CT5_UserInput.cpp` | C++ source code and original pseudocode |
| `CSC450_CT5_mod5.txt` | Instructor-provided text file containing original and appended data |
| `CSC450-mod5-reverse.txt` | Output file containing the reversed text |
| `.gitignore` | Excludes compiled files and generated artifacts |
| `LICENSE` | MIT License |
| `README.md` | Project documentation |

The two text files are retained in the repository to demonstrate the original assignment's input and output.

## How the Program Works

The program performs the following operations:

1. Prompts the user to enter a line of text.
2. Opens `CSC450_CT5_mod5.txt` in append mode.
3. Adds the entered text to the end of the file.
4. Closes the file after writing.
5. Reopens the file for reading.
6. Reads its contents character by character.
7. Reverses the complete character sequence.
8. Creates or overwrites `CSC450-mod5-reverse.txt`.
9. Writes the reversed contents to the output file.
10. Displays confirmation messages.

The program checks whether each file opens successfully before attempting to read or write data.

## Key Programming Concepts

### Console Input

The application accepts user input using `getline()`:

```cpp
string userInput;

cout << "Enter text to add to the file: ";
getline(cin, userInput);
```

Unlike `cin >>`, `getline()` can read an entire line containing spaces.

This allows the user to enter sentences rather than individual words.

### Appending to an Existing File

The program opens the original text file using:

```cpp
ofstream appendFile("CSC450_CT5_mod5.txt", ios::app);
```

The `ios::app` flag instructs the program to append new information to the end of the file.

This preserves the existing contents rather than replacing them.

The user's input is appended using:

```cpp
appendFile << userInput << endl;
```

The `endl` manipulator adds a newline after the entered text.

### Reading File Contents

The program uses an input file stream to read the updated file:

```cpp
ifstream inputFile("CSC450_CT5_mod5.txt");
```

It then reads the contents one character at a time:

```cpp
char currentCharacter;

while (inputFile.get(currentCharacter))
{
    fileContents += currentCharacter;
}
```

Using `get()` allows the program to read spaces and newline characters along with ordinary text.

This is important because the assignment requires reversing the complete file contents.

### Reversing the Text

The program uses a loop to swap characters from opposite ends of the string:

```cpp
for (int i = 0; i < fileContents.length() / 2; i++)
{
    char temporaryCharacter = fileContents[i];

    fileContents[i] = fileContents[fileContents.length() - 1 - i];

    fileContents[fileContents.length() - 1 - i] = temporaryCharacter;
}
```

The loop continues until it reaches the middle of the string.

Each iteration exchanges two characters, gradually reversing the entire sequence.

This approach reverses the string in place without requiring a second string for the reversed result.

### Reversing the Entire File

The assignment requires reversing all characters in the file, not simply reversing each individual line.

The implementation treats the complete file as one sequence of characters, including:

- Letters
- Numbers
- Spaces
- Punctuation
- Newline characters

Because newline characters are included, reversing the complete sequence also reverses the order of the lines.

The output may therefore appear differently from a program that reverses each line independently.

This behavior is intentional and follows the original assignment requirements.

### Writing the Reversed Output

The program creates the output file using:

```cpp
ofstream reverseFile("CSC450-mod5-reverse.txt");
```

It then writes the reversed contents:

```cpp
reverseFile << fileContents;
```

Opening the output file this way replaces its previous contents if the file already exists.

The original input file remains intact apart from the newly appended user text.

### File Error Handling

Before reading or writing, the program checks whether each file opened successfully.

For example:

```cpp
if (!appendFile.is_open())
{
    cout << "Error: Unable to open CSC450_CT5_mod5.txt." << endl;
    return 1;
}
```

Similar checks are used for the input and reversed-output files.

These checks prevent the program from continuing when a required file cannot be opened.

## Pseudocode

The original source file includes pseudocode outlining the complete program.

```text
START

DECLARE userInput as string
DECLARE fileContents as string

ASK user to enter text
GET userInput

OPEN CSC450_CT5_mod5.txt in append mode

IF file does not open
    PRINT error message
    END program
END IF

APPEND userInput to CSC450_CT5_mod5.txt
CLOSE file

OPEN CSC450_CT5_mod5.txt for reading

IF file does not open
    PRINT error message
    END program
END IF

READ all characters from file into fileContents
CLOSE file

REVERSE all characters in fileContents

OPEN CSC450-mod5-reverse.txt for writing

IF file does not open
    PRINT error message
    END program
END IF

WRITE reversed fileContents to CSC450-mod5-reverse.txt
CLOSE file

PRINT confirmation that files were successfully processed

END
```

The pseudocode documents the intended sequence of input, file operations, character reversal, and output.

## How to Compile and Run

### Requirements

- A C++ compiler such as g++ through MSYS2 / MinGW-w64
- A terminal or command prompt
- Windows, Linux, or macOS with a compatible C++ development environment

### Step 1 — Clone the Repository

```bash
git clone https://github.com/Tentei06/cpp-file-io-and-text-reversal.git
```

Navigate to the repository:

```bash
cd cpp-file-io-and-text-reversal
```

### Step 2 — Compile the Program

```bash
g++ CSC450_CT5_UserInput.cpp -o file-io-reversal
```

### Step 3 — Run the Program

**Windows (PowerShell):**

```powershell
.\file-io-reversal.exe
```

**Linux or macOS:**

```bash
./file-io-reversal
```

Run the program from the repository's root directory so the relative file paths resolve correctly.

### Important Note About File Changes

Running this application modifies the text files in the working directory.

Each execution:

- Appends another line to `CSC450_CT5_mod5.txt`.
- Recreates `CSC450-mod5-reverse.txt` using the updated file contents.

If you want to preserve the original assignment files, create backup copies before running the program.

## Example Execution

The following example demonstrates the console interaction:

```text
Enter text to add to the file: Learning C++ file handling.
Your text was successfully added to CSC450_CT5_mod5.txt.
The reversed text was successfully saved to CSC450-mod5-reverse.txt.
```

The entered text is appended to the original file.

The program then reverses the entire updated file and writes the result to the separate output file.

For example, reversing only the text:

```text
Hello World
```

would produce:

```text
dlroW olleH
```

This short example illustrates the character-reversal operation. The actual output file contains the reversal of the complete updated input file, including any existing text and newline characters.

## Testing and Verification

The original assignment involved testing the application's file-handling and reversal behavior.

The following table describes the expected results.

| Test Scenario | Expected Result |
|---------------|-----------------|
| Enter a line of text | Input is accepted through `getline()` |
| Append user input | Existing file contents are preserved |
| Read the updated file | All characters are read, including spaces and newlines |
| Reverse file contents | Complete character sequence is reversed |
| Write reversed output | Separate output file is created or overwritten |
| Input file cannot be opened | Error message is displayed |
| Output file cannot be opened | Error message is displayed |
| Successful execution | Confirmation messages are displayed |

The repository includes the original input and reversed-output text files for inspection.

## Development Process

The original assignment involved:

1. Reviewing the file input/output requirements.
2. Writing pseudocode for the program.
3. Implementing console input using `getline()`.
4. Opening the provided text file in append mode.
5. Preserving existing data while adding new text.
6. Reading the updated file character by character.
7. Implementing an in-place character-reversal algorithm.
8. Writing the reversed contents to a second file.
9. Adding basic checks for file-opening failures.
10. Compiling and testing the application.

The source code preserves the original coursework implementation and explanatory comments.

## Limitations

This project is an introductory file-processing exercise.

- The application processes one line of user input per execution.
- It does not provide an interactive menu.
- Input is appended each time the program runs.
- The reversed output file is overwritten on each execution.
- File paths are hardcoded.
- The program reads the entire file into memory before reversing it.
- It checks file-opening failures but does not comprehensively validate every read or write operation.
- The reversal operates on individual characters/bytes rather than language-aware Unicode text elements.

These limitations reflect the scope of the original assignment.

## Educational Context

This application was developed for the **Module 5 Critical Thinking assignment** in CSC450 — Programming III at Colorado State University Global.

It demonstrates foundational programming skills in:

- User input and string handling
- File input/output
- File stream operations
- Appending and preserving existing data
- Iterative character processing
- String reversal algorithms
- Basic file error handling
- Pseudocode and program planning

The project also introduces concepts relevant to applications that store, retrieve, and process information using external files.

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
