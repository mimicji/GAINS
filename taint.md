# Taint Analysis
## Table of contents
- [Dynamic Taint Analysis](#dynamic-taint-analysis)
	- [Guide](#guide)
	- [Efficiency](#efficiency)
		- [Common](#common)
		- [Commodity Hardware](#commodity-hardware)
	- [Offline Tainting](#offline-tainting)
- [Static Taint Analysis](#static-taint-analysis)
- [Taint Policy](#taint-policy)
- [Taint Rule](#taint-rule)
- [Tools](#tools)
## Dynamic Taint Analysis
`DTA`. Also known as Dynamic information flow tracking (`DIFT`)
### Guide
- `TaintCheck` Newsome, James, and Dawn Xiaodong Song. "[Dynamic Taint Analysis for Automatic Detection, Analysis, and SignatureGeneration of Exploits on Commodity Software.](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.307.8389&rep=rep1&type=pdf)" _NDSS_. Vol. 5. 2005.
- Schwartz, Edward J., Thanassis Avgerinos, and David Brumley. "[All you ever wanted to know about dynamic taint analysis and forward symbolic execution (but might have been afraid to ask).](https://users.ece.cmu.edu/~aavgerin/papers/Oakland10.pdf)"  _2010 IEEE symposium on Security and privacy_. IEEE, 2010.]
### Efficiency
#### Common
- Saxena, Prateek, R. Sekar, and Varun Puranik. "[Efficient fine-grained binary instrumentationwith applications to taint-tracking.](https://dl.acm.org/doi/abs/10.1145/1356058.1356069)" _Proceedings of the 6th annual IEEE/ACM international symposium on Code generation and optimization_. 2008.
- Ruwase, Olatunji, et al. "[Decoupled lifeguards: enabling path optimizations for dynamic correctness checking tools.](https://dl.acm.org/doi/pdf/10.1145/1809028.1806600)" _ACM Sigplan Notices_ 45.6 (2010): 25-35.
- Bosman, Erik, Asia Slowinska, and Herbert Bos. "[Minemu: The world’s fastest taint tracker.](https://link.springer.com/chapter/10.1007/978-3-642-23644-0_1)" _International Workshop on Recent Advances in Intrusion Detection_. Springer, Berlin, Heidelberg, 2011.
- Kemerlis, Vasileios P., et al. "[libdft: Practical dynamic data flow tracking for commodity systems.](https://dl.acm.org/doi/abs/10.1145/2151024.2151042)" _Proceedings of the 8th ACM SIGPLAN/SIGOPS conference on Virtual Execution Environments_. 2012.
- Ming, Jiang, et al. "[Taintpipe: Pipelined symbolic taint analysis.](https://www.usenix.org/conference/usenixsecurity15/technical-sessions/presentation/ming)" _24th USENIX Security Symposium (USENIX Security 15)_. 2015.
- Quinn, Andrew, et al. "[JetStream: Cluster-scale parallelization of information flow queries.](https://www.usenix.org/conference/osdi16/technical-sessions/presentation/quinn))" _12th USENIX Symposium on Operating Systems Design and Implementation (OSDI 16)_. 2016.
- Banerjee, Subarno, et al. "[Iodine: fast dynamic taint tracking using rollback-free optimistic hybrid analysis.](https://web.eecs.umich.edu/~pmchen/papers/banerjee19.pdf)" _2019 IEEE Symposium on Security and Privacy (SP)_. IEEE, 2019.

#### Commodity Hardware
- `Speck` Nightingale, Edmund B., et al. "[Parallelizing security checks on commodity hardware.](https://dl.acm.org/doi/pdf/10.1145/1353534.1346321)" _ACM SIGARCH Computer Architecture News_ 36.1 (2008): 308-318.
- Zhu, David, et al. "[TaintEraser: Protecting sensitive data leaks using application-level taint tracking.](https://dl.acm.org/doi/pdf/10.1145/1945023.1945039)" _ACM SIGOPS Operating Systems Review_ 45.1 (2011): 142-154.
- Jee, Kangkook, et al. "[A General Approach for Efficiently Accelerating Software-based Dynamic Data Flow Tracking on Commodity Hardware.](https://angelosk.github.io/Papers/2012/dta.pdf)" _NDSS_. 2012.Offline Tainting
#### Neural Network
- She, Dongdong, et al. "[Neutaint: Efficient Dynamic Taint Analysis with Neural Networks.](https://arxiv.org/pdf/1907.03756.pdf)" _2020 IEEE Symposium on Security and Privacy (SP)_. IEEE, 2020.
## Offline Tainting
- Ming, Jiang, et al. "[Straighttaint: Decoupled offline symbolic taint analysis.](https://dl.acm.org/doi/pdf/10.1145/2970276.2970299)" _2016 31st IEEE/ACM International Conference on Automated Software Engineering (ASE)_. IEEE, 2016.
## Static Taint Analysis
- Wang, Xinran, et al. "[Still: Exploit code detection via static taint and initialization analyses.](http://www.cse.psu.edu/~sxz16/papers/still.pdf)" _2008 Annual Computer Security Applications Conference (ACSAC)_. IEEE, 2008.
- Biondi, Philippe, et al. "[BinCAT: purrfecting binary static analysis.](https://www.sstic.org/media/SSTIC2017/SSTIC-actes/bincat_purrfecting_binary_static_analysis/SSTIC2017-Article-bincat_purrfecting_binary_static_analysis-biondi_rigo_zennou_mehrenberger.pdf)" _Symposium sur la sécurité des technologies de l’information et des communications_. 2017.
## Taint Policy
- Xu, Wei, Sandeep Bhatkar, and Ramachandran Sekar. "[Taint-Enhanced Policy Enforcement: A Practical Approach to Defeat a Wide Range of Attacks.](https://www.usenix.org/event/sec06/tech/full_papers/xu/xu_html/)" _USENIX Security Symposium_. 2006.
## Taint Rule
- `TaintInduce` Chua, Zheng Leong, et al. "[One Engine To Serve'em All: Inferring Taint Rules Without Architectural Semantics.](https://pdfs.semanticscholar.org/2f04/e6bc5bbf2df6d0df15593f2e648681591173.pdf)" _NDSS_. 2019.
## Tools
- `Pin` [Dytan](https://github.com/behzad-a/Dytan): Dytan Taint Analysis Framework on Linux 64-bit [`Paper`](https://dl.acm.org/doi/pdf/10.1145/1273463.1273490)
- `Pin` [libdft](https://github.com/vusec/vuzzer/tree/master/support/libdft): Practical Dynamic Data Flow Tracking. [libdft64](https://github.com/AngoraFuzzer/libdft64)
- `llvm` `Python bindings` `Pin (Optional)` [Triton](https://github.com/JonathanSalwan/Triton): a Dynamic Binary Analysis (DBA) framework
- `llvm` [BAP](https://github.com/BinaryAnalysisPlatform/bap): Binary Analysis Platform [`Paper`](https://link.springer.com/content/pdf/10.1007/978-3-642-22110-1_37.pdf)
- `whole-system` `BitBlaze`  `QEMU` `TCG`[TEMU](http://bitblaze.cs.berkeley.edu/temu.html): The BitBlaze Dynamic Analysis Component [`Paper`](https://www.researchgate.net/profile/Heng_Yin/publication/228935091_Temu_Binary_code_analysis_via_whole-system_layered_annotative_execution/links/541c5f710cf203f155b5df76.pdf)
- `whole-system` `Panda`  `QEMU` `LLVM` [PIRATE](https://github.com/panda-re/panda/tree/38f5795726d0c37432d848707d1a9443956e0ace/panda/plugins/taint2): Platform for IR-based Analyses of Tainted Execution
- `whole-system` `QEMU` `TCG`[DECAF](https://github.com/decaf-project/DECAF): Dynamic Executable Code Analysis Framework [`Paper`](http://www.jmlr.org/proceedings/papers/v32/donahue14.pdf)
- `whole-system` `SWIFT` `QEMU` [MBA](https://github.com/GlacierW/MBA): Malware Behavior Analyzer [`Paper`](http://www.iis.sinica.edu.tw/page/jise/2015/201507_15.pdf)
- `static` `IDA` `Python` [BinCAT](https://github.com/airbus-seclab/bincat): a static Binary Code Analysis Toolkit [`Paper`](https://www.sstic.org/media/SSTIC2017/SSTIC-actes/bincat_purrfecting_binary_static_analysis/SSTIC2017-Article-bincat_purrfecting_binary_static_analysis-biondi_rigo_zennou_mehrenberger.pdf)
- `KLEE` [KLEE-TAINT](https://github.com/feliam/klee-taint)

## 'To-read' list
- Kang, Min Gyung, et al. "[Dta++: dynamic taint analysis with targeted control-flow propagation.](https://people.eecs.berkeley.edu/~dawnsong/papers/2011%20dta++-ndss11.pdf)" _NDSS_. 2011.
