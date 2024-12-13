# Setting Up and Using Doxygen with MATLAB on Windows

This guide will walk you through installing and configuring Doxygen, Perl, and all necessary tools to generate documentation for MATLAB projects on a Windows system.

---

## Prerequisites

Before starting, ensure you have the following:
- A Windows computer
- Administrator privileges
- MATLAB source files for documentation

---

## Step 1: Install Doxygen

1. Download the latest version of Doxygen from [Doxygen's official website](https://www.doxygen.nl/download.html).
2. Run the installer and follow the setup instructions.
3. During installation, ensure the option **"Add doxygen to the system PATH for all users"** is selected.
4. Verify the installation:
   ```cmd
   doxygen --version
   ```

---

## Step 2: Install Perl

1. Download and install Strawberry Perl from [Strawberry Perl's website](https://strawberryperl.com/).
2. Ensure that the Perl binary is added to your system PATH during installation.
3. Verify the installation:
   ```cmd
   perl --version
   ```

---

## Step 3: Install Graphviz

1. Download and install Graphviz from [Graphviz's website](https://graphviz.org/download/).
2. During installation, ensure **"Add Graphviz to the system PATH"** is selected.
3. Verify the installation:
   ```cmd
   dot -version
   ```

---

## Step 4: Configure Doxygen

1. Generate a default `Doxyfile`:
   ```cmd
   doxygen -g
   ```
2. Open the generated `Doxyfile` in a text editor and make the following modifications:
   - Set the project name:
     ```plaintext
     PROJECT_NAME = "MATLAB Documentation"
     ```
   - Define the input directory where your MATLAB files are located:
     ```plaintext
     INPUT = path\to\your\matlab\project
     ```
   - Enable recursive search for subdirectories:
     ```plaintext
     RECURSIVE = YES
     ```
   - Specify the input file patterns:
     ```plaintext
     FILE_PATTERNS = *.m
     ```
   - Set the input filter to use the `m2cpp.pl` script:
     ```plaintext
     FILTER_PATTERNS = *.m=path\to\m2cpp.pl
     ```
   - Enable class diagrams and graphs using Graphviz:
     ```plaintext
     HAVE_DOT = YES
     DOT_PATH = path\to\graphviz\bin
     ```

---

## Step 5: Update `m2cpp.pl`

1. Open the `m2cpp.pl` script in a text editor.
2. Modify the shebang line at the top of the file to point to the Perl executable (MacOs: use which perl to find the path. Windows: where perl):
   ```perl
   #!C:/Strawberry/perl/bin/perl
   ```
3. Save and close the file.

---

## Step 6: Generate Documentation

1. Run Doxygen with the updated `Doxyfile`:
   ```cmd
   doxygen Doxyfile
   ```
2. The documentation will be generated in the output directory specified in the `Doxyfile` (default is `./html`).

---

## Step 7: Verify the Output

1. Navigate to the output directory.
2. Open `index.html` in a browser to view the generated documentation.
3. Ensure that:
   - Functions and classes are documented.
   - Graphs and diagrams are included if applicable.

---

## Troubleshooting

### Common Issues and Solutions
- **Doxygen cannot find the `dot` executable**: Ensure Graphviz is correctly installed and added to the system PATH.
- **Perl script errors**: Verify the correct path to the Perl interpreter in `m2cpp.pl`.
- **Missing documentation for functions**: Ensure functions are properly formatted in MATLAB files and follow Doxygen's syntax for comments.

---

## Additional Resources
- [Old guid for Doxygen for MATLAB](https://www.mathworks.com/matlabcentral/fileexchange/25925-using-doxygen-with-matlab)
- [Doxygen Documentation](https://www.doxygen.nl/manual/index.html)
- [Graphviz Documentation](https://graphviz.org/documentation/)
- [Strawberry Perl Documentation](https://strawberryperl.com/)

---

This setup should allow you to generate comprehensive documentation for your MATLAB projects using Doxygen on Windows.
