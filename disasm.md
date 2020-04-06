# Disassembly, Assembly, Decompilation and Debugging
## Table of contents
- [Guide](#guide)
- [Tools](#tools)
	- [Disassemblers](#disassemblers)
	- [Assemblers](#assemblers)
	- [Decompilers](#decompilers)
	- [Debuggers](#debuggers)
		- [Memory Debuggers](#memory-debuggers)
## Guide
- Andriesse, Dennis, et al. "[An in-depth analysis of disassembly on full-scale x86/x64 binaries.](https://www.usenix.org/system/files/conference/usenixsecurity16/sec16_paper_andriesse.pdf)" _25th USENIX Security Symposium (USENIX Security 16)_. 2016.
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
- [Hex-Rays Decompiler](http://www.hex-rays.com/products/decompiler/index.shtml)
- [Ghidra](https://ghidra-sre.org/)
- [Hopper](http://www.hopperapp.com/)
### Debuggers
- [GNU Debugger](https://www.gnu.org/software/gdb/)
- [OllyDbg](http://www.ollydbg.de/)
- [LLDB](https://lldb.llvm.org/)
#### Memory Debuggers
- [AddressSanitizer](https://github.com/google/sanitizers/wiki/AddressSanitizer)
- [Valgrind Memcheck](https://valgrind.org/)
- [DynamoRIO Dr. Memory](https://github.com/DynamoRIO/drmemory)
