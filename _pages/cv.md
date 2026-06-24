---
layout: single
title: "Curriculum Vitae"
permalink: /cv/
author_profile: true
toc: true
toc_label: "Contents"
toc_sticky: true
---

<p style="margin-top:-0.4em;">
  <a href="{{ '/_pdfs/Shuoming_Zhang_CV.pdf' | relative_url }}" class="btn btn--primary" target="_blank" rel="noopener">
    <i class="fas fa-file-pdf"></i>&nbsp; Download CV (PDF)
  </a>
</p>

**Shuoming Zhang** (张朔铭) &nbsp;·&nbsp; Ph.D. Candidate in Computer Architecture<br>
State Key Laboratory of Processors, Institute of Computing Technology, CAS &nbsp;|&nbsp; University of Chinese Academy of Sciences<br>
<a href="mailto:zhangshuoming17@mails.ucas.ac.cn">zhangshuoming17@mails.ucas.ac.cn</a> &nbsp;·&nbsp; Beijing, China &nbsp;·&nbsp;
<a href="https://scholar.google.com/citations?user=mVkTXAoAAAAJ&hl=en">Google Scholar</a> &nbsp;·&nbsp;
<a href="https://orcid.org/0009-0004-4210-5123">ORCID</a> &nbsp;·&nbsp;
<a href="https://github.com/zhangshuoming990105">GitHub</a> &nbsp;·&nbsp;
<a href="https://openreview.net/profile?id=~Shuoming_Zhang1">OpenReview</a>

## Research Interests

Kernel agents (LLM-driven generation, optimization, and verification of low-level compute kernels); large-scale multi-agent systems; LLM infrastructure and serving systems; reliability and safety for LLM-driven systems; compiler design and code translation.

## Education

- **Ph.D. in Computer Architecture**, Institute of Computing Technology, CAS & [UCAS](https://www.ucas.ac.cn/) &nbsp;·&nbsp; *2021 – present*<br>
  State Key Laboratory of Processors (SKLP). Advisors: [Prof. Huimin Cui](https://cuihuimin.github.io/) and [Assoc. Prof. Jiacheng Zhao](https://jiacheng.page/).
- **B.Eng. in Computer Science**, [University of Chinese Academy of Sciences (UCAS)](https://www.ucas.ac.cn/) &nbsp;·&nbsp; *2017 – 2021*

## Honors & Awards

- **Distinguished Paper Award**, CGO 2026 — *From Threads to Tiles (T2T)*.
- **Spotlight**, ICML 2026 — *CONTINUUM*.

## Selected Publications

<sup>†</sup> equal contribution &nbsp;·&nbsp; <sup>*</sup> corresponding author &nbsp;·&nbsp; author name in **bold**.

- **[ICML 2026, spotlight]** *CONTINUUM: Restoring the Contiguous Tensor Abstraction Efficiently for Dynamic AI Workloads via Hardware Virtualization* — Yangyu Zhang<sup>†</sup>, **Shuoming Zhang**<sup>†</sup>, et al., Jiacheng Zhao<sup>*</sup>
- **[CGO 2026, Distinguished Paper Award]** *From Threads to Tiles: T2T, a Compiler for CUDA-to-NPU Translation via 2D Vectorization* — Shuaijiang Li, Jiacheng Zhao<sup>*</sup>, Ying Liu, **Shuoming Zhang**, et al.
- **[CCS 2026]** *When Grammar Guides the Attack: Uncovering Control-Plane Vulnerabilities in LLMs with Structured Output* — **Shuoming Zhang**, Jiacheng Zhao<sup>*</sup>, et al. [[arXiv]](https://arxiv.org/abs/2503.24191)
- **[ISCA 2026]** *Symbiotic MLLM Serving: Dynamically Balancing Parallelism Across GPUs and Resources Within GPUs* — Zhicheng Li, Jiacheng Zhao<sup>*</sup>, et al., **Shuoming Zhang**, et al.
- **[arXiv 2026]** *Learning When to Optimize: Verified Optimization Skills from Expert GPU-Kernel Lineages (KLineage)* — **Shuoming Zhang**<sup>†</sup>, Qiuchu Yu<sup>†</sup>, et al., Jiacheng Zhao<sup>*</sup> [[arXiv]](https://arxiv.org/abs/2605.28213)

See the [full publication list]({{ "/publications/" | relative_url }}) for all peer-reviewed papers and preprints.

## Research Experience

**Current projects**

- **Kernel agents** — Agentic pipelines that synthesize, tune, and verify high-performance kernels for AI accelerators with LLM-in-the-loop search and feedback.
- **Large-scale multi-agent systems** — Orchestration and runtime support for populations of cooperating LLM agents on complex software-engineering and system-level tasks.
- **Secure and robust LLM decoding** — Constrained-decoding strategies that mitigate LLM safety vulnerabilities while preserving task performance.

**Earlier projects**

- **LLM-guided compilation workflows** — Model-in-the-loop pipelines for source-to-assembly translation and error recovery with LLM feedback.
- **LLM-aware compiler construction** — Reusable compiler components that leverage LLM reasoning for IR transformation, code generation, and verification.
- **Heterogeneous model offloading with TVM** *(collaboration with Intel)* — NPU/CPU co-execution and scheduling within the TVM stack; prototyped a new TVM backend for a simulator-based NPU.
- **VLIW instruction scheduling** *(collaboration with Huawei)* — Instruction-scheduling heuristics targeting domain-specific VLIW architectures.

## Technical Skills

- **Languages:** C/C++, Python, CUDA
- **Systems & Tools:** LLVM/MLIR, TVM, PyTorch, LLM serving/inference stacks, Git, Linux
- **Areas:** compiler construction, code generation & translation, GPU/NPU kernel optimization, LLM agents and serving systems

<p style="margin-top:1.5em; font-size:0.85em; color:#777;">Last updated: June 2026.</p>
