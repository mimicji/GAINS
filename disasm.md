# Disassembly, Assembly, Decompilation (Reversing) and Debugging
## Table of contents
- [Disassemble](#disassemble)
- [Decompilation](#decompilation)
- [Tools](#tools)
	- [Disassemblers](#disassemblers)
	- [Assemblers](#assemblers)
	- [Decompilers](#decompilers)
	- [Debuggers](#debuggers)
		- [Memory Debuggers](#memory-debuggers)
## Disassemble
- Andriesse, Dennis, et al. "[An in-depth analysis of disassembly on full-scale x86/x64 binaries.](https://www.usenix.org/system/files/conference/usenixsecurity16/sec16_paper_andriesse.pdf)" _25th USENIX Security Symposium (USENIX Security 16)_. 2016.
## Decompilation
- Liu, Zhibo, and Shuai Wang. "[How far we have come: testing decompilation correctness of C decompilers.](https://dl.acm.org/doi/pdf/10.1145/3395363.3397370)" Proceedings of the 29th ACM SIGSOFT International Symposium on Software Testing and Analysis. 2020.
- Gussoni, Andrea, et al. "[A Comb for Decompiled C Code.](https://dl.acm.org/doi/pdf/10.1145/3320269.3384766)" Proceedings of the 15th ACM Asia Conference on Computer and Communications Security. 2020.
## Tools
### Disassemblers
- [IDA Pro](https://www.hex-rays.com/products/ida/)
- [Ghidra](https://ghidra-sre.org/)
- [Binary Ninja](https://binary.ninja/)
- [Medusa](https://github.com/wisk/medusa)
- [Radare2](http://radare.org/y/)
- [Hopper](http://www.hopperapp.com/)
- [angr](http://angr.io/)
- `Online` [ODA](http://www.onlinedisassembler.com/)
- [llvm-mc](http://blog.llvm.org/2010/01/x86-disassembler.html)
- `lib` `Encoder&Decoder` [Intel® XED](https://software.intel.com/en-us/articles/xed-x86-encoder-decoder-software-library)
- `lib` `Multi-arch` [Capstone](http://www.capstone-engine.org/)
- `lib` `Only support X86` [Zydis](https://zydis.re/)
### Assemblers
- [keystone](http://www.keystone-engine.org/)
### Decompilers
- [IDA Pro: Hex-Rays Decompiler](http://www.hex-rays.com/products/decompiler/index.shtml)
- [JEB3](https://www.pnfsoftware.com/)
- [Radare/Ghidra](https://ghidra-sre.org/) (the native ghidra decompiler)
- [Radare: r2dec](https://rada.re/n/radare2.html)
- [RetDec](https://retdec.com/)
- [Hopper](http://www.hopperapp.com/)
### Debuggers
- [GNU Debugger](https://www.gnu.org/software/gdb/)
- [OllyDbg](http://www.ollydbg.de/)
- [LLDB](https://lldb.llvm.org/)
#### Memory Debuggers
- [AddressSanitizer](https://github.com/google/sanitizers/wiki/AddressSanitizer)
- [Valgrind Memcheck](https://valgrind.org/)
- [DynamoRIO Dr. Memory](https://github.com/DynamoRIO/drmemory)
