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
## 4. Let's explore the binary file using `objdump` tool:
```bash
objdump -D a.exe | grep -A20 main.:
```
**OUTPUT**:
```bash
0000000140001450 <main>:
   140001450:   55                      push   %rbp
   140001451:   48 89 e5                mov    %rsp,%rbp
   140001454:   48 83 ec 30             sub    $0x30,%rsp
   140001458:   e8 03 01 00 00          call   140001560 <__main>
   14000145d:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
   140001464:   eb 13                   jmp    140001479 <main+0x29>
   140001466:   48 8d 05 93 2b 00 00    lea    0x2b93(%rip),%rax        # 140004000 <.rdata>
   14000146d:   48 89 c1                mov    %rax,%rcx
   140001470:   e8 9b 12 00 00          call   140002710 <puts>
   140001475:   83 45 fc 01             addl   $0x1,-0x4(%rbp)
   140001479:   83 7d fc 09             cmpl   $0x9,-0x4(%rbp)
   14000147d:   7e e7                   jle    140001466 <main+0x16>
   14000147f:   b8 00 00 00 00          mov    $0x0,%eax
   140001484:   48 83 c4 30             add    $0x30,%rsp
   140001488:   5d                      pop    %rbp
   140001489:   c3                      ret
   14000148a:   90                      nop
   14000148b:   90                      nop
   14000148c:   90                      nop
   14000148d:   90                      nop
--
0000000140001560 <__main>:
   140001560:   8b 05 ca 5a 00 00       mov    0x5aca(%rip),%eax        # 140007030 <initialized>
   140001566:   85 c0                   test   %eax,%eax
   140001568:   74 06                   je     140001570 <__main+0x10>
   14000156a:   c3                      ret
   14000156b:   0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)
   140001570:   c7 05 b6 5a 00 00 01    movl   $0x1,0x5ab6(%rip)        # 140007030 <initialized>
   140001577:   00 00 00
   14000157a:   e9 61 ff ff ff          jmp    1400014e0 <__do_global_ctors>
   14000157f:   90                      nop

0000000140001580 <_setargv>:
   140001580:   31 c0                   xor    %eax,%eax
   140001582:   c3                      ret
   140001583:   90                      nop
   140001584:   90                      nop
   140001585:   90                      nop
   140001586:   90                      nop
   140001587:   90                      nop
   140001588:   90                      nop
   140001589:   90                      nop

```
## 5. Intel Syntax: 
```bash
objdump -M intel -D a.exe | grep -A20 main.:
```
**OUTPUT**:
```bash
0000000140001450 <main>:
   140001450:   55                      push   rbp
   140001451:   48 89 e5                mov    rbp,rsp
   140001454:   48 83 ec 30             sub    rsp,0x30
   140001458:   e8 03 01 00 00          call   140001560 <__main>
   14000145d:   c7 45 fc 00 00 00 00    mov    DWORD PTR [rbp-0x4],0x0
   140001464:   eb 13                   jmp    140001479 <main+0x29>
   140001466:   48 8d 05 93 2b 00 00    lea    rax,[rip+0x2b93]        # 140004000 <.rdata>
   14000146d:   48 89 c1                mov    rcx,rax
   140001470:   e8 9b 12 00 00          call   140002710 <puts>
   140001475:   83 45 fc 01             add    DWORD PTR [rbp-0x4],0x1
   140001479:   83 7d fc 09             cmp    DWORD PTR [rbp-0x4],0x9
   14000147d:   7e e7                   jle    140001466 <main+0x16>
   14000147f:   b8 00 00 00 00          mov    eax,0x0
   140001484:   48 83 c4 30             add    rsp,0x30
   140001488:   5d                      pop    rbp
   140001489:   c3                      ret
   14000148a:   90                      nop
   14000148b:   90                      nop
   14000148c:   90                      nop
   14000148d:   90                      nop
--
0000000140001560 <__main>:
   140001560:   8b 05 ca 5a 00 00       mov    eax,DWORD PTR [rip+0x5aca]        # 140007030 <initialized>
   140001566:   85 c0                   test   eax,eax
   140001568:   74 06                   je     140001570 <__main+0x10>
   14000156a:   c3                      ret
   14000156b:   0f 1f 44 00 00          nop    DWORD PTR [rax+rax*1+0x0]
   140001570:   c7 05 b6 5a 00 00 01    mov    DWORD PTR [rip+0x5ab6],0x1        # 140007030 <initialized>
   140001577:   00 00 00
   14000157a:   e9 61 ff ff ff          jmp    1400014e0 <__do_global_ctors>
   14000157f:   90                      nop

0000000140001580 <_setargv>:
   140001580:   31 c0                   xor    eax,eax
   140001582:   c3                      ret
   140001583:   90                      nop
   140001584:   90                      nop
   140001585:   90                      nop
   140001586:   90                      nop
   140001587:   90                      nop
   140001588:   90                      nop
   140001589:   90                      nop
```
