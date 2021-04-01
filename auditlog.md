# Audit Log Analysis
## Table of contents
- [Audit Log Analysis](#audit-log-analysis)
	- [Table of contents](#table-of-contents)
	- [Survey](#survey)
	- [Definition](#definition)
	- [Generation](#generation)
			- [Tool](#tool)
			- [Literature](#literature)
	- [SIEM](#siem)
			- [Forensic Analysis](#forensic-analysis)
			- [Attack Detection](#attack-detection)
	- [Limitations](#limitations)
			- [Space Overhead](#space-overhead)
			- [Dependency Explosion](#dependency-explosion)
	- [Query](#query)
	- [Integrity](#integrity)
	- [CTI](#cti)

## Survey
- Threat Detection and Investigation with System-level Provenance Graphs: A Survey. Zhenyuan, et al. arxiv'2020 [paper](https://arxiv.org/pdf/2006.01722.pdf)

## Definition
Every event in audit logs represents an OS-level system activity such as process creation, file access, and network connection. Here, we use read and execve activities as examples to illustrate log events.
```
READ Event:
type=PROCTITLE msg=audit(08/26/19 20:34:53.383:98866813) : proctitle=bash 
type=SYSCALL msg=audit(08/26/19 20:34:53.383:98866813) : arch=x86_64 syscall=read success=yes exit=25 a0=0x3 a1=0x7ffedcf386a0 a2=0x80 a3=0x7fa5c53f19d0 items=0 ppid=15757 pid=30204 auid=junzeng uid=root gid=root euid=root suid=root fsuid=root egid=root sgid=root fsgid=root tty=pts21 ses=6309 comm=service exe=/bin/dash key=(null) 

EXECVE Event:
type=PROCTITLE msg=audit(16/05/2019 16:18:30.752:49036555) : proctitle=ls /etc/bash_completion.d 
type=PATH msg=audit(16/05/2019 16:18:30.752:49036555) : item=1 name=/lib64/ld-linux-x86-64.so.2 inode=135768 dev=08:05 mode=file,755 ouid=root ogid=root rdev=00:00 nametype=NORMAL cap_fp=none cap_fi=none cap_fe=0 cap_fver=0 
type=PATH msg=audit(16/05/2019 16:18:30.752:49036555) : item=0 name=/bin/ls inode=6815827 dev=08:05 mode=file,755 ouid=root ogid=root rdev=00:00 nametype=NORMAL cap_fp=none cap_fi=none cap_fe=0 cap_fver=0 
type=CWD msg=audit(16/05/2019 16:18:30.752:49036555) : cwd=/home/junzeng 
type=EXECVE msg=audit(16/05/2019 16:18:30.752:49036555) : argc=2 a0=ls a1=/etc/bash_completion.d 
type=SYSCALL msg=audit(16/05/2019 16:18:30.752:49036555) : arch=x86_64 syscall=execve success=yes exit=0 a0=0x170e168 a1=0x1847cc8 a2=0x1807008 a3=0x598 items=2 ppid=10738 pid=10739 auid=junzeng uid=junzeng gid=junzeng euid=junzeng suid=junzeng fsuid=junzeng egid=junzeng sgid=junzeng fsgid=junzeng tty=pts21 ses=287 comm=ls exe=/bin/ls key=(null)  
```

## Generation
#### Tool
- `Linux` [Auditd](https://github.com/linux-audit): kernel-level tracing facility for Linux
- `Windows` [ETW](https://docs.microsoft.com/en-us/windows/win32/etw/about-event-tracing): kernel-level tracing facility for Windows
- `FreeBSD` [Dtrace](https://wiki.freebsd.org/DTrace): kernel-level tracing facility for FreeBSD

#### Literature
- Forensix: A robust, high-performance reconstruction system. A. Goel, et al. Distributed computing systems workshops 2005 [paper](https://thefengs.com/wuchang/papers/sdcs05_forensix_full.pdf)
- PASS: Provenance-aware storage systems. K. Muniswamy-Reddy, et al. ATC'2006 [paper](https://syrah.eecs.harvard.edu/files/syrah/files/usenix06.pdf)
- Layering in provenance systems. K.-K. Muniswamy-Reddy, et al. Security'2009 [paper](https://www.usenix.org/legacy/events/usenix09/tech/full_papers/muniswamy-reddy/muniswamy-reddy.pdf)
- Trail of bytes: efficient support for forensic analysis. S. Krishnan, K. Z. Snow, and F. Monrose. CCS'2010 [paper](https://www.cs.unc.edu/~fabian/papers/trail10.pdf)
- Hi-fi: collecting high-fidelity whole-system provenance. D. J. Pohly, et al. CCS'2012 [paper](https://www.cise.ufl.edu/~butler/pubs/acsac12b.pdf)
- Spade: support for provenance auditing in distributed environments. A. Gehani and D. Tariq. International Middleware Conference 2012 [paper](http://www.csl.sri.com/users/gehani/papers/MW-2012.SPADE.pdf)
- LPM: Trustworthy whole-system provenance for the linux kernel. A. Bates. et al. Security'2015 [paper](https://www.usenix.org/system/files/conference/usenixsecurity15/sec15-paper-bates.pdf)
- Transparent Web Service Auditing via Network Provenance Functions. A. Bates, et al. WWW'2017 [paper](https://cise.ufl.edu/~butler/pubs/www17.pdf)
- Fear and logging in the internet of things. Q. Wang, et al. NDSS'2018 [paper](http://seclab.illinois.edu/wp-content/uploads/2017/12/wang2018fear.pdf)
- Kernel-Supported Cost-Effective Audit Logging for Causality Tracking. S. Ma, et al. ATC'2018 [paper](https://www.usenix.org/system/files/conference/atc18/atc18-ma-shiqing.pdf)
- Xanthus: Push-button Orchestration of Host Provenance Data Collection. Han Xueyuan, et al. P-RECS'2020 [paper](https://arxiv.org/pdf/2005.04717.pdf)


## SIEM
#### Forensic Analysis
- Backtracking intrusions. King, et al. SOSP'2003 [paper](https://web.eecs.umich.edu/virtual/papers/king05_2.pdf)
- Enriching intrusion alerts through multi-host causality. S. T. King, et al. NDSS'2005 [paper](https://web.eecs.umich.edu/virtual/papers/king05.pdf)
- The taser intrusion recovery system. A. Goel, et al. ASPLOS'2005 [paper](https://dl.acm.org/doi/pdf/10.1145/1095810.1095826)
- Provenance-aware tracing ofworm break-in and contaminations: A process coloring approach. X. Jiang et al. ICDCS'2006 [paper](https://www.cs.purdue.edu/homes/dxu/pubs/ICDCS06.pdf)
- Intrusion recovery using selective re-execution. T. Kim, et al. OSDI'2010 [paper](https://people.csail.mit.edu/nickolai/papers/kim-retro.pdf)
- Integrating ids alert correlation and os-level dependency tracking. Y. Zhai, et al. Intelligence and Security Informatics 2016 [paper](https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.227.5496&rep=rep1&type=pdf)
- CamFlow: Practical whole-system provenance capture. Pasquier, et al. Cloud Computing 2017 [paper](https://dl.acm.org/doi/pdf/10.1145/3127479.3129249)
- SLEUTH: Real-time attack scenario reconstruction from COTS audit data. M. N. Hossain, et al. Security'2017 [paper](https://www.usenix.org/system/files/conference/usenixsecurity17/sec17-hossain.pdf)
- Towards a timely causality analysis for enterprise security. Y. Liu, et al. NDSS'2018 [paper](https://www.princeton.edu/~pmittal/publications/priotracker-ndss18)
- LPROV: Practical Library-aware Provenance Tracing. F. Wang, et al. ACSAC'2018 [paper](https://yonghwi-kwon.github.io/data/lprov_acsac18.pdf)
- This is Why We Can't Cache Nice Things: Lightning-Fast Threat Hunting using Suspicion-Based Hierarchical Storage. W. U. Hassan, et al. ACSAC'2020 [paper](https://adambates.org/documents/Hassan_Acsac20.pdf)
- WATSON: Abstracting Behaviors from Audit Logs via Aggregation of Contextual Semantics. Jun Z, et al. NDSS'2021 [paper](https://www.ndss-symposium.org/wp-content/uploads/2021-549-paper.pdf)


#### Attack Detection
- Detecting intrusions using system calls: Alternative data models. C. Warrender, et al. SP'1999 [paper](http://wenke.gtisc.gatech.edu/ids-readings/system_call_models.pdf)
- Provenance-Aware Tracing of Worm Break-in and Contaminations: A Process Coloring Approach. X. Jiang, et al. ICDCS'2006 [paper](https://www.cs.purdue.edu/homes/dxu/pubs/ICDCS06.pdf)
- On the learning of system call attributes for host-based anomaly detection. G. Tandon and P. K. Chan. IJAIT'2006 [paper](https://pdfs.semanticscholar.org/1f05/969f6e72aad5e15e13df8019351085cc9683.pdf)
- Detecting insider threats in a real corporate database of computer usage activity. E. Ted, et al. KDD'2013 [paper](https://dl.acm.org/doi/pdf/10.1145/2487575.2488213)
- Malicious behavior detection using Windows audit logs. K. Berlin, et al. AISec'2015 [paper](https://arxiv.org/pdf/1506.04200.pdf)
- Detection of early-stage enterprise infection by mining large-scale log data. A. Oprea, et al. SDN'2015 [paper](https://arxiv.org/pdf/1411.5005.pdf)
- Entity embedding-based anomaly detection for heterogeneous categorical events. T. Chen, et al. IJCAI'2016 [paper](https://www.ijcai.org/Proceedings/16/Papers/201.pdf)
- Hercule: Attack story reconstruction via community discovery on correlated log graph, K. Pei, et al. ACSAC'2016 [paper](https://www.cs.purdue.edu/homes/dxu/pubs/HERCULE.pdf)
- Fast Memory-efficient Anomaly Detection in Streaming Heterogeneous Graphs. E. Manzoor, et al. KDD'2016 [paper](https://www.kdd.org/kdd2016/papers/files/rfp0693-manzoorA.pdf)
- Efficient Discovery of Abnormal Event Sequences in Enterprise Secur. B. Dong, et al. CIKM'2017 [paper](https://dl.acm.org/doi/pdf/10.1145/3132847.3132854)
- Collaborative Alert Ranking for Anomaly Detection. Y. Lin, et al. CIKM'2018 [paper](https://dl.acm.org/doi/pdf/10.1145/3269206.3272013)
- Heterogeneous Graph Matching Networks for Unknown Malware Detection. S. Wang, et al. IJCAI'2019 [paper](https://www.ijcai.org/Proceedings/2019/0522.pdf)
- Holmes: real-time apt detection through correlation of suspicious information flows, S. M. Milajerdi, et al. SP'2019 [paper](https://smomen2.people.uic.edu/publications/HOLMES.pdf)
- Nodoze: Combatting threat alert fatigue with automated provenance triage. W. U. Hassan, et al. NDSS'2019 [paper](https://www.ndss-symposium.org/wp-content/uploads/2019/02/ndss2019_03B-1-3_UlHassan_paper.pdf)
- UNICORN: Runtime Provenance-Based Detector for Advanced Persistent Threats. Han, Xueyuan, et al. NDSS'2020 [paper](https://www.ndss-symposium.org/wp-content/uploads/2020/02/24046-paper.pdf)
- You are what you do: Hunting stealthy malware via data provenance analysis. Wang, Qi, et al. NDSS'2020 [paper](https://www.ndss-symposium.org/wp-content/uploads/2020/02/24167-paper.pdf)
- Tactical Provenance Analysis for Endpoint Detection and Response Systems. W. U. Hassan, et al. SP'2020 [paper](https://adambates.org/documents/Hassan_Oakland20.pdf)
- ATLAS: A Sequence-based Learning Approach for Attack Investigation. A. Alsaheel, et al. Security'2021 [paper](https://www.usenix.org/system/files/sec21summer_alsaheel.pdf)
- SIGL: Securing Software Installations Through Deep Graph Learning. Han Xueyuan, et al. Security'2021 [paper](https://arxiv.org/pdf/2008.11533.pdf)

## Limitations
#### Space Overhead
- Loggc: garbage collecting audit log. K. H. Lee, et al. CCS'2013 [paper](https://friends.cs.purdue.edu/pubs/CCS13_LogGC.pdf)
- High fidelity data reduction for big data security dependency analyses. Z. Xu, et al. CCS'2016 [paper](https://kangkookjee.github.io/publications/xu-ccs2016.pdf)
- Protracer: Towards practical provenance tracing by alternating between logging and tainting. S. Ma, X. Zhang, and D. Xu. NDSS 2016 [paper](https://friends.cs.purdue.edu/pubs/NDSS16.pdf)
- Towards scalable cluster auditing through grammatical inference over provenance graphs. W. U. Hassan, et al. NDSS'2018 [paper](https://www.ndss-symposium.org/wp-content/uploads/2018/02/ndss2018_07B-1_Hassan_paper.pdf)
- Dependence-preserving data compaction for scalable forensic analysis. M. N. Hossain, et al. Security'2018 [paper](https://www.usenix.org/system/files/conference/usenixsecurity18/sec18-hossain.pdfs)
- NodeMerge: Template Based Efficient Data Reduction For Big-Data Causality Analysis. Y. Tang, et al. CCS'2018 [paper](https://kangkookjee.github.io/publications/nodemerge-ccs2018.pdf)
- APTrace: A Responsive System for Agile Enterprise Level Causality Analysis. Gui, et, al. ICDE'2020 [paper](https://ieeexplore.ieee.org/document/9101446/)
- On the Forensic Validity of Approximated Audit Logs. N. Michael, et al. ACSAC'2020. [paper](https://adambates.org/documents/Michael_Acsac20.pdf)

#### Dependency Explosion
- Forensic analysis of file system intrusions using improved backtracking, S. Sitaraman and S. Venkatesan. IWIA'2005 [paper](https://dl.acm.org/doi/10.1109/IWIA.2005.9)
- Panorama: capturing system-wide information flow for malware detection and analysis. H.Yin, et al. CCS'2007 [paper](http://bitblaze.cs.berkeley.edu/papers/panorama.pdf)
- High accuracy attack provenance via binary-based execution partition. K. H. Lee, X. Zhang, and D. Xu. NDSS'2013 [paper](https://www.ndss-symposium.org/wp-content/uploads/2017/09/03_1_0.pdf)
- Accurate, low cost and instrumentation-free security audit logging for windows. S. Ma, et al. ACSAC'2015 [paper](https://kyuhlee.github.io/publications/acsac15.pdf)
- Protracer: Towards practical provenance tracing by alternating between logging and tainting. S. Ma, X. Zhang, and D. Xu. NDSS 2016 [paper](https://friends.cs.purdue.edu/pubs/NDSS16.pdf)
- LDX: Causality inference by lightweight dual execution, Y. Kwon, et al. ASPLOS'2016 [paper](https://dl.acm.org/doi/pdf/10.1145/2954679.2872395)
- MPI: Multiple perspective attack investigation with semantic aware execution partitioning. S. Ma, et al. Security'2017 [paper](https://www.usenix.org/system/files/conference/usenixsecurity17/sec17-ma.pdf)
- Rain: Refinable attack investigation with on-demand inter-process information flow tracking. Y. Ji, et al. CCS'2017 [paper](https://iisp.gatech.edu/sites/default/files/images/rain.pdf)
- Enabling refinable cross-host attack investigation with efficient data flow tagging and tracking. Y. Ji, et al. Security'2018 [paper](https://www.usenix.org/system/files/conference/usenixsecurity18/sec18-ji.pdf)
- MCI: Modeling-based causality inference in audit logging for attack investigation. Y. Kwon, et al. NDSS'2018 [paper](https://weihang-wang.github.io/papers/mci_ndss18.pdf)
- Propatrol: Attack investigation via extracted high-level tasks. S. M Milajerdi, et al. Information Systems Security 2018 [paper](https://arxiv.org/pdf/1810.05711.pdf)
- UISCOPE: Accurate, Instrumentation-free, and Visible Attack Investigation for GUI Applications. Runqing Yang, et al. NDSS'2020 [paper](https://www.ndss-symposium.org/wp-content/uploads/2020/02/24329-paper.pdf)
- Omega-Log: High-fidelity attack investigation via transparent multi-layer log analysis. Hassan, Wajih Ul, et al. NDSS'2020 [paper](https://www.ndss-symposium.org/wp-content/uploads/2020/02/24270-paper.pdf)
- Combating Dependence Explosion in Forensic Analysis Using Alternative Tag Propagation Semantics. M. N. Hossain, et al. SP'2020 [paper](http://seclab.cs.sunysb.edu/seclab/pubs/morse20.pdf)
- ALchemist: Fusing Application and Audit Logs for Precise Attack Provenance without Instrumentation. Le Yu, et al. NDSS'2021 [paper](https://www.ndss-symposium.org/wp-content/uploads/2021-445-paper.pdf)

## Query
- Behavior query discovery in system-generated temporal graphs. B. Zong, et al. VLDB'2015 [paper](http://www.vldb.org/pvldb/vol9/p240-zong.pdf)
- AIQL: Enabling efficient attack investigation from system monitoring data. P.Gao, et al. ATC'2018 [paper](https://www.usenix.org/system/files/conference/atc18/atc18-gao.pdf)
- SAQL: A stream-based query system for real-time abnormal system behavior detection. P.Gao, et al. Security'2018 [paper](https://www.usenix.org/system/files/conference/usenixsecurity18/sec18-gao_0.pdf)
- Threat intelligence computing. X. Shu, et al. CCS'2018 [paper](https://dl.acm.org/doi/pdf/10.1145/3243734.3243829)
- Runtime Analysis of Whole-System Provenance. T. Pasquier, et al. CCS'2018 [paper](https://arxiv.org/pdf/1808.06049.pdf)
- Graalf: Supporting graphical analysis of audit logs for forensics. O. Setayeshfar, et al. arXiv'2019 [paper](https://arxiv.org/pdf/1909.00902.pdf)
- Poirot: Aligning attack behavior with kernel audit records for cyber threat hunting. S. M Milajerdi, et al. CCS'2019 [paper](https://smomen2.people.uic.edu/publications/POIROT.pdf)

## Integrity
- Forward integrity for secure audit logs. M. Bellare and B. Yee. Tech. Rep. 1997 [paper](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.28.7970)
- A new approach to secure logging. D. Ma and G. Tsudik. TOS'2009 [paper](https://dl.acm.org/doi/pdf/10.1145/1502777.1502779)
- Efficient data structures for tamper-evident logging. S. A. Crosby and D. S. Wallach. Security'2009 [paper](https://www.usenix.org/legacy/event/sec09/tech/full_papers/crosby.pdf)
- BAF: An efficient publicly verifiable secure audit logging scheme for distributed systems. A. A. Yavuz and P. Ning. ACSAC'2009 [paper](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.147.9496&rep=rep1&type=pdf)
- Efficient, compromise resilient and append-only cryptographic schemes for secure audit logging. FC'2012 [paper](https://link.springer.com/chapter/10.1007/978-3-642-32946-3_12)
- Sgx-log: Securing system logs with sgx. Karande, Vishal, et al. AsiaCCS'2017 [paper](https://dl.acm.org/doi/pdf/10.1145/3052973.3053034)
- Practical and robust secure logging from fault-tolerant sequential aggregate signatures. G. Hartung, et al. ProvSec'2017 [paper](https://eprint.iacr.org/2017/949.pdf)
- Custos: Practical tamper-evident auditing of operating systems using trusted execution. Paccagnella Riccardo, et al. NDSS'2020 [paper](https://www.ndss-symposium.org/wp-content/uploads/2020/02/24065-paper.pdf)
- Logging to the Danger Zone: Race Condition Attacks and Defenses on System Audit Frameworks. Paccagnella Riccardo, et al. CCS'2020 [paper](https://www.kevliao.com/publications/kennyloggings-ccs2020.pdf)

## CTI
- Poirot: Aligning attack behavior with kernel audit records for cyber threat hunting. S. M Milajerdi, et al. CCS'2019 [paper](https://smomen2.people.uic.edu/publications/POIROT.pdf)
- Cyber Threat Intelligence Modeling Based on Heterogeneous Graph Convolutional Network. Jun Zhao, et al. RAID'2020 [paper](https://seit.egr.msu.edu/paper/raid20_CTI.pdf)
- Enabling Efficient Cyber Threat Hunting With Cyber Threat Intelligence. Peng Gao, et al. arXiv'2020 [paper](https://arxiv.org/pdf/2010.13637.pdf)
