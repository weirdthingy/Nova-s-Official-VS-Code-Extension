# 🚀 Nova's Extension for VS Code

## 💻 VS Code Extension & Syntax Highlighting

Nova 1.1 comes with its own official Visual Studio Code extension to provide full syntax highlighting (colors) for your code blocks, comments, strings, and numbers, as well as automatic bracket/quotation auto-closing and code running.

### How to Install the Extension:
1. Download the `nova-lang-1.0.0.vsix` file from the zip file `nova-lang-v1.0`
2. Open **VS Code**.
3. Go to the **Extensions** tab on the left sidebar (Ctrl+Shift+X).
4. Click on the three dots `...` in the top-right corner of the Extensions panel.
5. Select **"Install from VSIX..."** and choose the downloaded file.
6. Open any `.nova` file and watch your custom syntax light up!

---

## 🛠️ Structure & Strict Syntax

### 1. Variables and Constants
Nova fixes Python's loose variable declaration weakness by introducing two mandatory keywords:
*   `let`: Declares a mutable variable. It must be declared before assigning a value to it.
*   `const`: Declares a constant. The compiler automatically converts the variable name to **UPPERCASE** and blocks any reassignment attempts at compile-time.

```text
const pi = 3.14159
let radio = 10
```

### 2. Flow Control via Curly Braces `{}`
Unlike Python, Nova completely removes mandatory visual indentation and forces the structured use of curly braces to delimit code blocks.

```text
let x = 0
while x < 5 {
    shout.nl(x)
    x = x + 1
}

if x == 5 {
    shout.nl("Limit reached")
} else {
    shout.nl("Continuing...")
}
```

### 3. C++ Style Logical Operators
Nova incorporates traditional lower-level logical operators: `&&` (and) and `||` (or).

```text
if user == "NovaDeveloper" && key == "123" {
    shout.nl("Access granted")
}
```

### 4. Custom Functions (`custom`)
Functions are defined using the `custom` keyword and natively support parameter passing.

```text
custom calculate_area(r) {
    let area = 3.14 * (r * r)
    shout("The area is: ")
    shout.nl(area)
}
```

---

## 🧰 Built-in Standard Library

Nova automatically injects an optimized suite of commands into every single compilation:
*   `shout("text")`: Prints text to the console without a newline (low-level style print).
*   `shout.nl("text")`: Prints text to the console with a newline.
*   `userget()`: Captures user input from the terminal (input replacement).
*   `clear()`: Cross-platform full-screen terminal clearer (Windows/Mac/Linux).
*   `clear(N)`: Erases exactly the last N lines of the console (ideal for screen frame updates or text animations).
*   `wait(N)`: Pauses the execution thread of the program for N seconds.
*   `math.pow(b, e)` / `math.sqrt(n)`: Native access to math operations.
*   `system.exit()`: Forces the program to terminate immediately.

---

## 🔒 Special Security Restrictions

Nova is engineered to foster good lower-level development practices and block Python's lazy shortcuts.
*   **Strict File Management:** Using automated `with` blocks or `as` assignment aliases is strictly forbidden. If the compiler detects them, it will throw the famous customized error:
    `"This ain't Python bro. No 'with' allowed."`
*   The programmer is strictly forced to manage memory channels manually by opening and closing Operating System streams:
    ```text
    f = open("log.txt", "w")
    f.write("Nova Engine\n")
    f.close() // Mandatory close
    ```

---

## 📦 Modular Project Compilation & Hybrid Imports

Nova 1.5 supports smart, hybrid importing via the `#use` directive. The compiler automatically detects the source type:

1. **Native Nova Modules:** If `module_name.nova` exists in the directory, Nova will compile it in chains and link it seamlessly.
2. **Python Ecosystem Compatibility:** If no `.nova` file is found, Nova passes the directive directly to the Python backend. This grants Nova developers instant, out-of-the-box access to millions of existing Python packages and libraries (like `numpy`, `pygame`, or standard modules) while maintaining Nova's strict syntax style.

```text
#use custom_game_logic // Imports and compiles custom_game_logic.nova
#use math              // Directly taps into Python's native math package
```
