# Setting Up and Using Doxygen with MATLAB on Windows and macOS

This guide provides step-by-step instructions for installing and configuring Doxygen, Perl, and other necessary tools to generate documentation for MATLAB projects on both Windows and macOS systems.

---

## Prerequisites

Ensure you have the following:
- A computer running Windows or macOS
- Administrator privileges
- MATLAB source files for documentation

---

## Step 1: Install Doxygen

### **Windows**

1. Download the latest version of Doxygen from [Doxygen's official website](https://www.doxygen.nl/download.html).
2. Run the installer and follow the setup instructions.
3. During installation, ensure the option **"Add doxygen to the system PATH for all users"** is selected.
4. Verify the installation:
   ```cmd
   doxygen --version
   ```

### **macOS**

1. Install Homebrew if not already installed:
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```
2. Use Homebrew to install Doxygen:
   ```bash
   brew install doxygen
   ```
3. Verify the installation:
   ```bash
   doxygen --version
   ```

---

## Step 2: Install Perl

### **Windows**

1. Download and install Strawberry Perl from [Strawberry Perl's website](https://strawberryperl.com/).
2. Ensure that the Perl binary is added to your system PATH during installation.
3. Find the Perl path by running:
   ```cmd
   where perl
   ```
4. Verify the installation:
   ```cmd
   perl --version
   ```

### **macOS**

1. Perl is pre-installed on macOS. Verify the installation:
   ```bash
   perl --version
   ```
2. Find the Perl path by running:
   ```bash
   which perl
   ```

---

## Step 3: Install Graphviz

### **Windows**

1. Download and install Graphviz from [Graphviz's website](https://graphviz.org/download/).
2. During installation, ensure **"Add Graphviz to the system PATH"** is selected.
3. Find the Graphviz `dot` path by running:
   ```cmd
   where dot
   ```
4. Verify the installation:
   ```cmd
   dot -version
   ```

### **macOS**

1. Use Homebrew to install Graphviz:
   ```bash
   brew install graphviz
   ```
2. Find the Graphviz `dot` path by running:
   ```bash
   which dot
   ```
3. Verify the installation:
   ```bash
   dot -version
   ```

---

## Step 4: Configure Doxygen

1. Generate a default `Doxyfile`:
   ```bash
   doxygen -g
   ```
2. Open the generated `Doxyfile` in a text editor and make the following modifications:
   - Set the project name:
     ```plaintext
     PROJECT_NAME = "MATLAB Documentation"
     ```
   - Define the input directory where your MATLAB files are located:
     ```plaintext
     INPUT = path/to/your/matlab/project
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
     FILTER_PATTERNS = *.m=path/to/m2cpp.pl
     ```
   - Enable class diagrams and graphs using Graphviz:
     ```plaintext
     HAVE_DOT = YES
     DOT_PATH = path/to/graphviz/bin
     ```
   - Modify the following settings to include more detailed documentation:
     ```plaintext
     EXTRACT_ALL = YES
     EXTRACT_STATIC = YES
     EXTRACT_LOCAL_CLASSES = YES
     HIDE_UNDOC_MEMBERS = NO
     HIDE_UNDOC_CLASSES = NO
     ```

---

## Step 5: Update `m2cpp.pl`

1. Open the `m2cpp.pl` script in a text editor.
2. Modify the shebang line at the top of the file to point to the Perl executable:

   ### **Windows**
   ```perl
   #! [path_of_perl(look_above)]
   ```
   example: #!/usr/local/bin/perl


   ### **macOS**
   ```perl
   #![path_of_perl(look_above)]
   ```
   example: #!/usr/local/bin/perl

3. Save and close the file.

---

## Step 6: Generate Documentation

1. Run Doxygen with the updated `Doxyfile`:
   ```bash
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

## Commenting Guidelines

To ensure your MATLAB files are properly documented, follow these guidelines:
Below is a table describing how to structure comments in MATLAB files to ensure compatibility with the `m2cpp.pl` script and Doxygen.

| **Code Element**      | **Comment Structure**                                                                                   | **Example**                                                                                                                        |
|------------------------|-------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| **File**              | Use `@file` for the filename and `@brief` for a short description.                                     | ```matlab %> @file FileName.m %> @brief Short description of the file. %> Additional details if necessary. ```                     |
| **Class**             | Add `@brief` above the class declaration, explaining its purpose.                                      | ```matlab %> @brief Description of the class. %> Additional details about its functionality. classdef MyClass ```                 |
| **Public Properties** | Use `%>` above the property to describe it.                                                           | ```matlab properties (Access = public) %> Description of the public property publicProperty end ```                                |
| **Constant Properties**| Specify the property as constant and describe it with `%>`.                                          | ```matlab properties (Constant = true) %> Description of a constant property constantProperty = 42; end ```                        |
| **Method**            | Use `@brief` for a short description, `@param` for parameters, and `@retval` for return values.        | ```matlab %> @brief Short description of the method. %> Detailed explanation. %> @param input Description of the input parameter. %> @retval output Description of the output value. function output = exampleMethod(obj, input) end ``` |
| **Enumerations**      | Use `%>` above each enumeration element for its description.                                           | ```matlab enumeration %> Description of the first element FirstElement %> Description of the second element SecondElement end ``` |
| **Events**            | Use `%>` to describe each event declared in the class.                                                | ```matlab events %> Description of the first event FirstEvent %> Description of the second event SecondEvent end ```               |
| **Static/Protected Methods** | Indicate the accessibility of the method and use `@brief`, `@param`, and `@retval` as for regular methods. | ```matlab methods (Static, Access = protected) %> @brief Static and protected method. %> Detailed explanation. %> @param input Description of the parameter. %> @retval output Return value. function output = exampleStaticMethod(input) end end ``` |
| **Abstract Methods**  | Add a description to the abstract method and specify parameters and return values.                     | ```matlab methods (Abstract = true) %> @brief Abstract method. %> Only the signature is declared. %> @param input Description of the parameter. %> @retval output Return value. output = abstractMethod(input); end ``` |

---

### General Rules:
1. **Consistency**: Always follow a consistent commenting style across all MATLAB files.
2. **Clarity**: Ensure comments are clear, concise, and professional.
3. **Mandatory Fields**: Always include `@brief`, and when applicable, use `@param`, `@retval`, and `%>`.


---

### Example

#### Wrong Comments
```matlab
classdef MyClass
properties
    data
end
methods
    function obj = MyClass(inputData)
        obj.data = inputData;
    end
end
end
```

#### Right Comments
```matlab
%> @file MyClass.m
%> @brief Example class demonstrating documentation style.
%> This class serves as a container for data.

classdef MyClass
    properties
        %> Stored data in the class
        data
    end
    methods
        % ======================================================================
        %> @brief Constructor for the MyClass class.
        %> Initializes an instance of the class with the provided data.
        %>
        %> @param inputData Input data for initialization.
        %> @retval obj Instantiated object of the MyClass class.
        % ======================================================================
        function obj = MyClass(inputData)
            obj.data = inputData;
        end
    end
end
```

---

## Troubleshooting

### Common Issues and Solutions
- **Doxygen cannot find the `dot` executable**: Ensure Graphviz is correctly installed and added to the system PATH.
- **Perl script errors**: Verify the correct path to the Perl interpreter in `m2cpp.pl`.
- **Missing documentation for functions**: Ensure functions are properly formatted in MATLAB files and follow Doxygen's syntax for comments.

---

## Additional Resources
- [Old guide for Doxygen for MATLAB](https://www.mathworks.com/matlabcentral/fileexchange/25925-using-doxygen-with-matlab)
- [Doxygen Documentation](https://www.doxygen.nl/manual/index.html)
- [Graphviz Documentation](https://graphviz.org/documentation/)
- [Strawberry Perl Documentation](https://strawberryperl.com/)

---

## Acknowledgements
This project utilizes the `m2cpp.pl` script from the package "Using Doxygen with Matlab" by Fabrice, available on MATLAB Central File Exchange.

Cite as:
Fabrice (2024). Using Doxygen with Matlab (https://www.mathworks.com/matlabcentral/fileexchange/25925-using-doxygen-with-matlab), MATLAB Central File Exchange. Retrieved December 13, 2024.

---


