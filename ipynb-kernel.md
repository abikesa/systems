 
## 🔁 Option 1: **Use `stata_kernel` (BEST Choice for Full Jupyter Integration)**

> A community-built Jupyter kernel that lets you run `.do` and `.ado` code in Jupyter notebooks, just like Python.

### ✅ Step-by-step Setup (macOS)

#### 1. **Install Python + Jupyter**

If you don’t already:

```bash
brew install python
pip install jupyter
```

#### 2. **Install `stata_kernel`**

```bash
pip install stata_kernel
python -m stata_kernel.install
```

#### 3. **Configure `stata_kernel`**

Open or create config file:

```bash
nano ~/.stata_kernel.conf
```

Add:

```ini
[stata]
stata_path = /Applications/Stata/StataMP.app/Contents/MacOS/stata-mp
stata_version = 18
```

⚠️ Replace with your Stata version.

#### 4. **Launch Jupyter**

```bash
jupyter notebook
```

You’ll now see **Stata** as a kernel option!

---

### ✅ Bonus Features of `stata_kernel`:

* **Inline results and plots**
* Run `do`/`ado` blocks like Python cells
* Cell magics: `%browse`, `%graph`, `%macro`, etc.
* Works with VS Code Jupyter notebooks too

📚 Docs: [https://kylebarron.dev/stata\_kernel/](https://kylebarron.dev/stata_kernel/)

---

## 🧪 Option 2: Call `stata-mp` from Jupyter using `!` or subprocess

This is simpler but much more limited.

```python
!stata-mp -b do myscript.do
```

Or in Python:

```python
import subprocess
subprocess.run(["stata-mp", "-b", "do", "myscript.do"])
```

This won’t return inline output or graphs — just executes the `.do` file and writes to `stata.log`.

---

## 🧠 Recommendation

> ✅ Use `stata_kernel` for an actual notebook interface with rich results.
> ❌ Avoid shell hacks unless you only want batch-style execution.

Would you like a working `.ipynb` example preloaded with Stata code cells and config reminders?
