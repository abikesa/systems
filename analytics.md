 

## 🧠 Goal: Set Up Stata on macOS + VS Code (Clean Machine)

### ✅ 1. **Install Stata**

You already did this. If not:

* Install from official installer: [https://www.stata.com](https://www.stata.com)
* Launch once to register license.

### ✅ 2. **Add Stata CLI to your `$PATH`**

Edit your shell config file (e.g. `~/.zshrc` for zsh or `~/.bash_profile` for bash):

```bash
nano ~/.zshrc
```

Add this line:

```bash
export PATH="/Applications/Stata/StataMP.app/Contents/MacOS:$PATH"
```

Then reload your shell:

```bash
source ~/.zshrc
```

Confirm with:

```bash
which stata-mp
```

You should get:

```
/Applications/Stata/StataMP.app/Contents/MacOS/stata-mp
```

---

### ✅ 3. **Set up VS Code for Stata**

#### 3.1. Enable Stata Syntax Highlighting

Install this extension:

* Go to **Extensions** (`Cmd+Shift+X`)
* Search for: **Stata Enhanced** or **Stata Language Support**

  * [Stata Enhanced on GitHub](https://github.com/yxonic/stata-enhanced-vscode)
* Install it.

🔷 This gives you syntax highlighting, comment toggling (`Cmd+/`), and basic support for `.do` and `.ado` files.

---

### ✅ 4. **Add Run Command for `.do` Files**

You can create a custom **VS Code task** to run your `.do` file with `stata-mp`.

#### Step-by-step:

1. Open your workspace or folder
2. Press `Cmd+Shift+P` → “Tasks: Configure Task”
3. Choose `Create tasks.json from template`
4. Pick `Others`
5. Replace the contents with:

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Run Stata DO file",
      "type": "shell",
      "command": "stata-mp",
      "args": [
        "-b",
        "do",
        "${file}"
      ],
      "group": {
        "kind": "build",
        "isDefault": true
      },
      "presentation": {
        "echo": true,
        "reveal": "always",
        "focus": false,
        "panel": "shared"
      },
      "problemMatcher": []
    }
  ]
}
```

Save it as: `.vscode/tasks.json`

#### ✅ Now you can run your `.do` file from VS Code:

* Open `stata.do`
* Hit `Cmd+Shift+B` → it runs via `stata-mp -b do yourfile.do`
* Output will go to `stata.log` file in the same directory.

---

### ✅ 5. (Optional) Create a Keyboard Shortcut

To bind `Cmd+R` (or similar) to run your `.do` file:

1. Go to **Preferences** → **Keyboard Shortcuts**
2. Search `Tasks: Run Build Task`
3. Add your shortcut, e.g. `Cmd+R`

---

### 🧩 6. Optional: Bonus Automation

If you want auto-open of the `.log` file after run:

* Modify the `tasks.json` `args` to:

```json
"args": [
  "-b",
  "do",
  "${file} && open stata.log"
]
```

But this gets tricky if the log file name changes or if your `do` file changes directories. Safer to open manually or write a shell script.

---

## 🚀 TL;DR Script

Put this in your `~/.zshrc`:

```bash
export PATH="/Applications/Stata/StataMP.app/Contents/MacOS:$PATH"
alias stata-do='stata-mp -b do'
```

Then run from terminal:

```bash
stata-do stata.do
```

Or from VS Code with `Cmd+Shift+B`.

 
