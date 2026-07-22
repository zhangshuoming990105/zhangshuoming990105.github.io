---
layout: home
author_profile: true
title: ""  # Hide the automatic page title
---

## About

**I am on the academic job market**, seeking a **postdoc or assistant-professor (AP) position starting in 2027**. I would be glad to connect — please feel free to [reach out](mailto:zhangshuoming17@mails.ucas.ac.cn) or take a look at my [CV]({{ "/_pdfs/Shuoming_Zhang_CV.pdf" | relative_url }}).
{: .notice--info}

I am a PhD candidate at the [State Key Laboratory of Processors](https://sklp.ict.ac.cn/), Institute of Computing Technology, CAS, and [University of Chinese Academy of Sciences](https://www.ucas.ac.cn/), advised by [Prof. Huimin Cui](https://cuihuimin.github.io/) and [Assoc. Prof. Jiacheng Zhao](https://jiacheng.page/).

My current research focuses on **kernel agents** and **large-scale multi-agent systems** — building LLM-driven agents that generate and optimize low-level kernels, and orchestrating large populations of agents to tackle complex system-level tasks. I am broadly interested in end-to-end system support for LLM workloads, from agent infrastructure to runtime orchestration. I received my B.Eng. in Computer Science from UCAS in 2021.

## Research Vision

I am increasingly drawn to **GPU kernel agents** and **large-scale multi-agent systems** as the two frontiers I care about most: the former pushes machine intelligence down to the metal — letting models reason about, write, and tune the kernels that power themselves; the latter scales it outward — turning many imperfect agents into a system that is competent, reliable, and cooperative. Underpinning both is the **infrastructure** that makes LLM generation controllable and trustworthy — from constrained and structured decoding to robust serving — so that what models produce can be relied upon, not merely hoped for. I believe **AGI is coming**, and I am committed to the *last-mile* engineering and exploration that will make it real — closing the gap between what current models can almost do and what intelligent systems must reliably deliver.

## News

- **Jul 2026** — New preprint *Decode-Time Grammars: Constrained LLM Generation over a Refinement Order of Grammar Fragments* on [arXiv](https://arxiv.org/abs/2607.18357).
- **Jul 2026** — *MoonBright* accepted at **OSDI 2026**.
- **May 2026** — New preprint *KLineage: Learning When to Optimize from Expert GPU-Kernel Lineages* on [arXiv](https://arxiv.org/abs/2605.28213).
- **May 2026** — Two papers accepted at **ICML 2026**, including one **spotlight** (*CONTINUUM*).
- **Apr 2026** — *When Grammar Guides the Attack* accepted at **CCS 2026**.
- **Mar 2026** — *Symbiotic MLLM Serving* accepted at **ISCA 2026**.
- **Mar 2026** — *LEGO-Compiler* accepted at **CCF THPC**.
- **Feb 2026** — *T2T* receives the **Distinguished Paper Award** at **CGO 2026**.
- **Sep 2025** — Two papers accepted at **NeurIPS 2025** (posters).

## Selected Publications

- **[arXiv 2026]** *Decode-Time Grammars: Constrained LLM Generation over a Refinement Order of Grammar Fragments* — **Shuoming Zhang**, Ruiyuan Xu, Haofeng Li, Qiuchu Yu, Yangyu Zhang, Chunwei Xia, Xiaobing Feng, Chenxi Wang, Huimin Cui, Jiacheng Zhao<sup>*</sup>
- **[arXiv 2026]** *Learning When to Optimize: Verified Optimization Skills from Expert GPU-Kernel Lineages* — **Shuoming Zhang**<sup>†</sup>, Qiuchu Yu<sup>†</sup>, Yangyu Zhang, Ruiyuan Xu, Xiyu Shi, Guangli Li, Xiaobing Feng, Huimin Cui, Jiacheng Zhao<sup>*</sup>
- **[ICML 2026 spotlight]** *CONTINUUM: Restoring the Contiguous Tensor Abstraction Efficiently for Dynamic AI Workloads via Hardware Virtualization* — Yangyu Zhang<sup>†</sup>, **Shuoming Zhang**<sup>†</sup>, Chunwei Xia, Shuaijiang Li, Zhicheng Li, Ruiyuan Xu, Zheming Yang, Lei Chen, Yuan Wen, Guangli Li, Xiaobing Feng, Huimin Cui, Jiacheng Zhao<sup>*</sup>
- **[ICML 2026]** *LEGO: An LLM-Enabled Hierarchical Optimizer for Tensor Computation Graphs with Structure-Aware Search and Compositional Synthesis* — Ruiyuan Xu<sup>†</sup>, **Shuoming Zhang**<sup>†</sup>, Guangli Li, Qiuchu Yu, Rui Zhang, Yangyu Zhang, Hao Qian, Chunwei Xia, Jiacheng Zhao, Chenxi Wang, Xiaobing Feng, Jingling Xue, Huimin Cui
- **[CCS 2026]** *When Grammar Guides the Attack: Uncovering Control-Plane Vulnerabilities in LLMs with Structured Output* — **Shuoming Zhang**, Jiacheng Zhao<sup>*</sup>, Hanyuan Dong, Ruiyuan Xu, Zhicheng Li, Yangyu Zhang, Shuaijiang Li, Yuan Wen, Chunwei Xia, Zheng Wang, Xiaobing Feng, Huimin Cui
- **[ISCA 2026]** *Symbiotic MLLM Serving: Dynamically Balancing Parallelism Across GPUs and Resources Within GPUs* — Zhicheng Li, Jiacheng Zhao<sup>*</sup>, Yangyu Zhang, Zhaolin Duan, Xinyu Liu, Siqi Li, **Shuoming Zhang**, Shuaijiang Li, Donglin Yu, Yuan Wen, Chunwei Xia, Xiyu Shi, Huimin Cui
- **[OSDI 2026]** *MoonBright: A GPU Memory Allocator with Device-Side Page Table Materialization and Deferred TLB Coherence* — Yangyu Zhang, Lei Chen, Chunwei Xia, Shuaijiang Li, **Shuoming Zhang**, Zhicheng Li, Qianqi Sun, Jiawei Xiao, Ruiyuan Xu, Ao Chen, Guangli Li, Xiaobing Feng, Huimin Cui, Chenxi Wang, Jiacheng Zhao<sup>*</sup>
- **[CGO 2026 Distinguished Paper Award]** *From Threads to Tiles: T2T, a Compiler for CUDA-to-NPU Translation via 2D Vectorization* — Shuaijiang Li, Jiacheng Zhao<sup>*</sup>, Ying Liu, **Shuoming Zhang**, Lei Chen, Yijin Li, Yangyu Zhang, Zhicheng Li, Runyu Zhou, Xiyu Shi, Chunwei Xia, Yuan Wen, Xiaobing Feng, Huimin Cui

See the [full publication list]({{ "/publications/" | relative_url }}).

## Research Interests

- Kernel agents — LLM-driven generation, optimization, and verification of low-level compute kernels
- Large-scale multi-agent systems — orchestration, coordination, and infrastructure for many-agent workloads
- LLM infrastructure and serving systems
- Constrained and structured decoding — part of LLM infrastructure, for controllable and reliable generation
- Reliability and safety for LLM-driven systems

## Research Projects

### Current

- **Kernel agents** — Building agentic pipelines that synthesize, tune, and verify high-performance kernels for AI accelerators with LLM-in-the-loop search and feedback.
- **Large-scale multi-agent systems** — Designing orchestration and runtime support for populations of cooperating LLM agents on complex software-engineering and system-level tasks.
- **Constrained and structured decoding** — Decoding as LLM infrastructure: constrained and grammar-based decoding for controllable, reliable, and safe generation.
- **Grammar-guided code generation** — Decode-time grammars that steer LLMs with grammar constraints to produce syntactically and semantically valid code, eliminating invalid references by construction ([arXiv](https://arxiv.org/abs/2607.18357)).

### Previous

- **LLM-guided compilation workflows** — Model-in-the-loop compilation pipelines for source-to-assembly translation and error recovery with LLM feedback.
- **LLM-aware compiler construction** — Reusable compiler components that leverage LLM reasoning for IR transformation, code generation, and verification.
- **Heterogeneous model offloading with TVM (Intel collaboration)** — Explored NPU/CPU co-execution and scheduling strategies within the TVM stack, prototyped a new TVM backend for simulator-based NPU.
- **VLIW instruction scheduling (Huawei collaboration)** — Developed instruction scheduling heuristics targeting domain-specific VLIW architectures.

## Professional Service

- **Reviewer** — TMLR (Transactions on Machine Learning Research), Artificial Intelligence Review, ICML, NeurIPS, ICLR, AAAI 2027

## Education

- **Ph.D. in Computer Architecture**, ICT CAS & [UCAS](https://www.ucas.ac.cn/), 2021 – now
- **B.Eng. in Computer Science**, [UCAS](https://www.ucas.ac.cn/), 2017 – 2021
