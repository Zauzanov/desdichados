# C
## 1. Windows preparations:
#### 1.1 Download the MSYS2 installer from the MSYS2 website — https://www.msys2.org/.
#### 1.2 Run the installer and follow the instructions.
#### 1.3 After installation, open the MSYS2 MinGW x64 terminal from your Start menu.
#### 1.4 Run the following command in the terminal to install the GCC C/C++ compiler toolset:
```bash
pacman -S mingw-w64-ucrt-x86_64-gcc
```
#### 1.5 Add the MinGW bin directory (`C:\msys64\ucrt64\bin`) to your Windows system's environment variables so that VS Code can find the compiler executable (gcc.exe).
#### 1.6 In the Windows search bar, type "environment variables" and select Edit the system environment variables.
#### 1.7 Copy and paste the path: Locate the bin folder containing gcc.exe (for example:C:\msys64\mingw64\bin). Click New and paste the copied path to your MinGW bin directory.
#### 1.8 Restart the system. 
## 2. Compile:
```bash
gcc fprog.c
```
## 3. Run:
```bash
./a.exe
```

