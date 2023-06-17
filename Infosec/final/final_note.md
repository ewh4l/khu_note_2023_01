# 8(main)
- **.text section**
	- code section, executable code
- PE header contains "entry point" for the instructions
	- **AddressOfEntryPoint**
- **Packing**
	- Zipping real `.text` section making it harder to analyze statically.
	- Only unpacked when executing (정적분석 방해)
	- Tools
		- **UPX**
			- for **compressing** rather than security
		- **Themida**
			- for security, 바이너리 분석방해
			- 가상화기반 난독화 tool
- 난독화
	- 기능은 동일하게, 형태를 복잡하게
	- ex) **그 사실을 인정합니다 -> 그 사실을 부정하지 않을 수 없지 않습니다.**
	- Types
		- 소스코드 난독화
			- 생소한 문법 이용
			- ex) `x = ( 5 == 5 )`
			- 간단한 수식 일부러 복잡하게
			- 가독성 저하
		- 바이너리 난독화
			- **Basic Block**
				- A chunk of code that is run together
			- **Control Flow Flattening
				- 베이직 블록 간 종속관계 직접적으로 보이지 않게 만듦
			- 명령어를 더 복잡한 버전으로
			- Bogus Control Flow (가짜 분기문)
		- 가상화 기반 난독화
			- 가상화 cpu용 코드, 독자적  ISA(Instruction Set Architecture)
			- 일반 cpu에서 동작 불가, 일반 reversing 불가
	- Tools
		- LLVM Obfuscator
			- 소스코드를 컴파일하는 과정에서 난독화
- 가상화
	- JVM style 가상화
	- VMware style 가상화
	-  가상화 기반 난독화
- 안티디버깅
	- types
		- API based
			- FindWindow API (using class name)
			- Registry value
			- IsDebuggerPresent API - flag
		- Exception handling based - 🧨RE
			- INT 3 (CC) scanning - pg.28
			- INT 3 : breakpoint
			- TRAP flag
		- data structure based - 🧨RE
		- anti-virtualization
			- e.g. virtial box, vmware
			- the criteria is vague now
			- 안티 디버깅 vs 안티 가상화
				- 안티 가상화 : 가상화 like vmware
		- Direct structure access
		- anti emulation
			- emulation 방해
			- emulation : hardware의 software적 구현
			- 가상화 vs emulation
				- 가상화 : 하나의 하드웨어에 여러 하드웨어 효과
				- emulation : 없는 하드웨어 소프트웨어로 흉내
			- **DBI**
				- Dynamic Binary Instrumentation
				- emulation 기반 기술
				- 명령어 레벨에서 분석 및 수정 가능
	- Examples
		- 가상화
			- Intel-VT
			- virtualbox
			- vmware
		- emulation
			- Qemu
- flag registers
	- To store status and control info
	- Main ones
		- 0 CF : carry flag
		- 2 PF : Parity flag
		- 6 ZF : zero flag
		- 7 SF : Sign flag
		- 11 OF : Overflow flag

---

# 9
- 정적분석 vs 동적분석
- decompiler
	- binary to source
- disassembler
	- binary to assembly
- debugging
	- 대표적 동적분석 방법
	- **breakpoint**
		- single **step** : exec 1 instruction
		- **next** instruction : exec, call is 1 instruction
	- debugger > disassembler
	- Tools
		- GDB
		- IDA
- 실습(pwndbg)
	- args : %edi, %esi, %edx, %ecx
	- `b main`, `b *[address]`(exact)
	- `ni`
	- `i r` : info register
	- `x/[repeat][format, size]`
		- `x/10wx`
- 실습(IDA Pro)
	- disassemble
		- basic
	- breakpoint
		- click on instruction & F2
	- single step
	- Check register
	- memory dump
	- Jump to address
		- type "g" & enter address in hex

---

# 10
- Anti debugging - ptrace
	- How it works?
		- `PTRACE_TRACEME` requests that OS traces the current process.
		- Since debugger is already attatched, another ptrace will fail.
- AntiAnti debugging - LD_PRELOAD
	- How it works?
		- LD_PRELOAD is an env variable that allows a user to specify a `.so` file to be loaded before other shared libraries
		- Commonly used for function hooking and overriding library functions.