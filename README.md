**This fork updates this action to using upload-artifact and checkout v4**

Check all available usable tags [here](../../tags)
<br>
You can also use any major tags like `@v1` for any `@v1.*.*`


<br>


# 🔰 PyInstaller
  - This action packages the python source code into executables using [pyinstaller](https://pyinstaller.org).
  - Use this action in your workflow to **create** & **upload** executables to GitHub _(as artifacts)_.
  - Use [inputs](#-inputs--outputs) to configure this action.
  - Use [outputs](#-inputs--outputs) to get information from this action.


<br>
<br>
<br>


# 🔰 Features
### 💠 Multi-OS support
  - Create executable for different kinds of os like linux, windows, mac etc.
  - Specify OS in `jobs.<job-id>.runs-on=<your-os-name>` in your workflow file.
  - see [examples](#-examples) for more info.

### 💠 .py and .spec support
  - You can use either `.py` or `.spec` file to create the executable.
  - Specify it in `inputs.spec: <file.py/file.spec>`.
  - When `.py` file is used, generated `.spec` file will also be uploaded as artifact.
  - Modify your `.spec` file according to your needs.

### 💠 Third party modules
  - Write your third party modules in a file _(Ex: `requirements.txt`)_ , and
  - Use `inputs.requirements: <path-to-your-requirement-file>`.

### 💠 Pyinstaller options
  - Specify pyinstaller options in `inputs.options: <comma-seperated-options-here>`.
  - `.py` and `.spec` both supports different kind of options.
  - Check list of all [supported options here](#-supported-pyinstaller-options).

### 💠 Python versions
  - You can specify any python version for the executable.
  - Specify specific python-version in `inputs.python_ver: <python-version-here>`.

### 💠 Executable uploads
  - You can control if generated executable needs to be uploaded as artifact.
  - You can choose a name of your liking.
  - Specify the artifact name in `inputs.upload_exe_with_name: <name-here>`.


<br>
<br>
<br>


# 🔰 Inputs & Outputs
  - Some **inputs** are **required**, while rest are optional. 
  - Check detailed info about these inputs & outputs [here](/action.yml).

### 💠 Available Inputs
  | Input                 | Default <br> _(`-` = empty string)_  | Description 
  |-----------------------|:--------:|-------------
  | `spec`  _(required)_  | -        | Path of your `.py` or `.spec` file
  | `requirements`        | -        | Path of your `requirements.txt` file
  | `options`             | -        | Options to set for pyinstaller command
  | `python_ver`          | 3.10     | Specific python version you want to use
  | `python_arch`         | x64      | Specific python architecture you want to use
  | `exe_path`            | ./dist   | Path on runner-os, where executable will be stored
  | `upload_exe_with_name`| -        | Upload exe_ artifact with this name. Else, it won't upload

<br>

### 💠 Available Outputs
  | Output                | Description 
  |-----------------------|-------------
  | `executable_path`     | Path on runner-os, where executable will be stored
  | `is_uploaded`         | `true`, if packaged executable has been uploaded as artifact

<br>

### 💠 Supported [Pyinstaller options](https://pyinstaller.org/en/stable/usage.html#options)
 | For `.py`                               | For `.py`                               | For `.spec`
 |-----------------------------------------|-----------------------------------------|------------
 | `--uac-admin`                           | `--name <NAME>`,        `-n <NAME>`     | `--ascii`,  `-a`
 | `--uac-uiaccess`                        | `--icon <FILEICON>`,    `-i <FILEICON>` | `--upx-dir <UPX_DIR>`
 | `--noupx`                               | `--key <KEY>`                           | 
 | `--onedir`,                        `-D` | `--upx-dir <UPX_DIR>`                   |
 | `--onefile`,                       `-F` | `--upx-exclude <FILE>`                  |
 | `--ascii`,                         `-a` | `--add-data <SRC;DEST or SRC:DEST>`     |
 | `--console`,    `--nowindowed`,    `-c` | `--add-binary <SRC;DEST or SRC:DEST>`   |
 | `--windowed`,   `--noconsole`,     `-w` | `--collect-data <MODULENAME>`


<br>
<br>
<br>


# 🔰 Examples

```yaml
jobs:
  pyinstaller-build:
    runs-on: <windows-latest / ubuntu-latest / ..... etc>
    steps:
      - name: Create Executable
        uses: sayyid5416/pyinstaller@v1
        with:
          python_ver: '3.6'
          spec: 'src/build.spec'
          requirements: 'src/requirements.txt'
          upload_exe_with_name: 'My executable'
          options: --onefile, --name "My App", --windowed, 
```
