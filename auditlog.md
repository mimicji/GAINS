# Audit Log Analysis
## Table of contents
- [Definition](#definition)
- [Survey](#survey)
- [Generation](#generation)
- [SIEM](#siem)
	- [Forensic Analysis](#forensic-analysis)
	- [Attack Detection](#attack-detection)
- [Limitations](#limitations)
	- [Space Overhead](#space-overhead)
	- [Dependency Explosion](#dependency-explosion)
- [Query](#query)
- [Integrity](#integrity)

## Survey
- Threat Detection and Investigation with System-level Provenance Graphs: A Survey. Zhenyuan, et al. arxiv'2020

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
- Forensix: A robust, high-performance reconstruction system, A. Goel, et al. Distributed computing systems workshops 2005
- PASS: Provenance-aware storage systems. K. Muniswamy-Reddy, et al. ATC'2006
- Layering in provenance systems. K.-K. Muniswamy-Reddy, et al. Security'2009
- Trail of bytes: efficient support for forensic analysis. S. Krishnan, K. Z. Snow, and F. Monrose. CCS'2010
- Hi-fi: collecting high-fidelity whole-system provenance. D. J. Pohly, et al. CCS'2012
- Spade: support for provenance auditing in distributed environments. A. Gehani and D. Tariq. International Middleware Conference 2012
- LPM: Trustworthy whole-system provenance for the linux kernel. A. Bates. et al. Security'2015
- Transparent Web Service Auditing via Network Provenance Functions. A. Bates, et al. WWW'2017
- Fear and logging in the internet of things. Q. Wang, et al. NDSS'2018
- Kernel-Supported Cost-Effective Audit Logging for Causality Tracking。 S. Ma, et al. ATC'2018

## SIEM
#### Forensic Analysis
- Backtracking intrusions. King, et al. SOSP'2003
- Enriching intrusion alerts through multi-host causality. S. T. King, et al. NDSS'2005
- The taser intrusion recovery system. A. Goel, et al. ASPLOS'2005
- Provenance-aware tracing ofworm break-in and contaminations: A process coloring approach. X. Jiang et al. ICDCS'2006
- Intrusion recovery using selective re-execution. T. Kim, et al. OSDI'2010
- Integrating ids alert correlation and os-level dependency tracking. Y. Zhai, et al. Intelligence and Security Informatics 2016
- CamFlow: Practical whole-system provenance capture. Pasquier, et al. Cloud Computing 2017
- SLEUTH: Real-time attack scenario reconstruction from COTS audit data. M. N. Hossain, et al. Security'2017
- Towards a timely causality analysis for enterprise security. Y. Liu, et al. NDSS'2018
- LPROV: Practical Library-aware Provenance Tracing. F. Wang, et al. ACSAC'2018

#### Attack Detection
- Detecting intrusions using system calls: Alternative data models. C. Warrender, et al. SP'1999
- Provenance-Aware Tracing of Worm Break-in and Contaminations: A Process Coloring Approach. X. Jiang, et al. ICDCS'2006
- On the learning of system call attributes for host-based anomaly detection. G. Tandon and P. K. Chan. IJCAI'2006
- Detecting insider threats in a real corporate database of computer usage activity. E. Ted, et al. KDD'2013
- Malicious behavior detection using Windows audit logs. K. Berlin, et al. AISec'2015
- Detection of early-stage enterprise infection by mining large-scale log data. A. Oprea, et al. SDN'2015
- Entity embedding-based anomaly detection for heterogeneous categorical events. T. Chen, et al. IJCAI'2016
- Hercule: Attack story reconstruction via community discovery on correlated log graph, K. Pei, et al. ACSAC'2016
- Fast Memory-efficient Anomaly Detection in Streaming Heterogeneous Graphs. E. Manzoor, et al. KDD'2016
- Efficient Discovery of Abnormal Event Sequences in Enterprise Secur. B. Dong, et al. CIKM'2017
- Collaborative Alert Ranking for Anomaly Detection. Y. Lin, et al. CIKM'2018
- Holmes: real-time apt detection through correlation of suspicious information flows, S. M. Milajerdi, et al. SP'2019
- Nodoze: Combatting threat alert fatigue with automated provenance triage. W. U. Hassan, et al. NDSS'2019
- UNICORN: Runtime Provenance-Based Detector for Advanced Persistent Threats. Han, Xueyuan, et al. NDSS'2020
- You are what you do: Hunting stealthy malware via data provenance analysis. Wang, Qi, et al. NDSS'2020
- Tactical Provenance Analysis for Endpoint Detection and Response Systems. W. U. Hassan, et al. SP'2020

## Limitations
#### Space Overhead
- Loggc: garbage collecting audit log. K. H. Lee, et al. CCS'2013
- High fidelity data reduction for big data security dependency analyses. Z. Xu, et al. CCS'2016
- Protracer: Towards practical provenance tracing by alternating between logging and tainting. S. Ma, X. Zhang, and D. Xu. NDSS 2016
- Towards scalable cluster auditing through grammatical inference over provenance graphs. W. U. Hassan, et al. NDSS'2018
- Dependence-preserving data compaction for scalable forensic analysis. M. N. Hossain, et al. Security'2018
- NodeMerge: Template Based Efficient Data Reduction For Big-Data Causality Analysis. Y. Tang, et al. CCS'2018
- APTrace: A Responsive System for Agile Enterprise Level Causality Analysis. Gui, et, al. ICDE'2020

#### Dependency Explosion
- Forensic analysis of file system intrusions using improved backtracking, S. Sitaraman and S. Venkatesan. IWIA'2005
- Panorama: capturing system-wide information flow for malware detection and analysis. H.Yin, et al. CCS'2007
- High accuracy attack provenance via binary-based execution partition. K. H. Lee, X. Zhang, and D. Xu. NDSS'2013
- Accurate, low cost and instrumentation-free security audit logging for windows. S. Ma, et al. ACSAC'2015
- Protracer: Towards practical provenance tracing by alternating between logging and tainting. S. Ma, X. Zhang, and D. Xu. NDSS 2016
- LDX: Causality inference by lightweight dual execution, Y. Kwon, et al. ASPLOS'2016
- MPI: Multiple perspective attack investigation with semantic aware execution partitioning. S. Ma, et al. Security'2017
- Rain: Refinable attack investigation with on-demand inter-process information flow tracking. Y. Ji, et al. CCS'2017
- Enabling refinable cross-host attack investigation with efficient data flow tagging and tracking. Y. Ji, et al. Security'2018
- MCI: Modeling-based causality inference in audit logging for attack investigation. Y. Kwon, et al. NDSS'2018
- Propatrol: Attack investigation via extracted high-level tasks. S. M Milajerdi, et al. Information Systems Security 2018
- Omega-Log: High-fidelity attack investigation via transparent multi-layer log analysis. Hassan, Wajih Ul, et al. NDSS'2020
- Combating Dependence Explosion in Forensic Analysis Using Alternative Tag Propagation Semantics. M. N. Hossain, et al. SP'2020

## Query
- Behavior query discovery in system-generated temporal graphs. B. Zong, et al. VLDB'2015
- AIQL: Enabling efficient attack investigation from system monitoring data. P.Gao, et al. ATC'2018
- SAQL: A stream-based query system for real-time abnormal system behavior detection. P.Gao, et al. Security'2018
- Threat intelligence computing. X. Shu, et al. CCS'2018
- Runtime Analysis of Whole-System Provenance. T. Pasquier, et al. CCS'2018
- Graalf: Supporting graphical analysis of audit logs for forensics. O. Setayeshfar, et al. arXiv'2019
- Poirot: Aligning attack behavior with kernel audit records for cyber threat hunting. S. M Milajerdi. CCS'2019

## Integrity
- Forward integrity for secure audit logs. M. Bellare and B. Yee. Tech. Rep. 1997
- A new approach to secure logging. D. Ma and G. Tsudik. TOS'2009
- Efficient data structures for tamper-evident logging. S. A. Crosby and D. S. Wallach. Security'2009
- BAF: An efficient publicly verifiable secure audit logging scheme for distributed systems. A. A. Yavuz and P. Ning. ACSAC'2009
- Efficient, compromise resilient and append-only cryptographic schemes for secure audit logging. FC'2012
- Sgx-log: Securing system logs with sgx. Karande, Vishal, et al. AsiaCCS'2017
- Practical and robust secure logging from fault-tolerant sequential aggregate signatures. G. Hartung, et al. ProvSec'2017
- Custos: Practical tamper-evident auditing of operating systems using trusted execution. Paccagnella, Riccardo, et al. NDSS'2020

