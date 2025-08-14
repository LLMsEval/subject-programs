# Subject programs for the Paper: “Evaluating Reasoning Capabilities of Large Language Models for Arduino Code Generation”

## Overview
Large Language Models (LLMs) are increasingly used to turn natural-language prompts into executable code. This repository accompanies the paper **“Evaluating Reasoning Capabilities of Large Language Models for Arduino Code Generation”** and provides the artifacts used to assess LLMs on **resource-constrained** microcontrollers. We compare **reasoning-capable** LLMs (GPT-o4-mini, DeepThink R1) with **standard** LLMs (GPT-4o, DeepSeek-V3) on correctness, efficiency, complexity, and similarity for **Arduino Uno Rev3** tasks.

---

## Subject Program Design
- **Programs:** 31 Arduino tasks, each with **two optimized reference solutions** (to reflect developer variation).
- **Coverage:** Data types, control structures, functions, arrays, loops, sensors, and more.
- **Platform:** Arduino Uno Rev3; **Arduino IDE 2.3.5** for compilation & memory usage readouts.
- **Reference Solutions:** Crafted for performance and reliability; some favor memory use, others speed.

Each task is paired with a consistent **zero-shot prompt** to ensure fair model comparison.

---

## Purpose of the Study
We evaluate four LLMs across **five** dimensions:  
1) Functional Correctness, 2) Runtime Efficiency, 3) Flash/SRAM Usage, 4) Code Complexity (Cyclomatic Complexity, NCLOC), 5) Code Similarity (CodeBLEU).

### Key Findings (Short)
- **Speed & Similarity:** Standard LLMs (GPT-4o, DeepSeek-V3) generally run **faster** and are **closer to human code**.  
- **Memory:** Reasoning LLMs (GPT-o4-mini, DeepThink R1) are **more memory-efficient** (flash & SRAM).  
- **Complexity:** Reasoning LLMs tend to produce **more complex and verbose** code (higher CC and NCLOC).  
- **Trade-off:** Clear trade-off between **execution speed** and **memory savings**; consider a **hybrid** workflow.

---

## Hardware & Software Setup
- **Board:** Arduino Uno Rev3 (all tests run on the same board).  
- **IDE:** Arduino IDE **2.3.5** (default configurations).  
- **Complexity:** [Lizard] for **Cyclomatic Complexity (CC)** and **NCLOC**.  
- **Similarity:** **CodeBLEU** via CodeXGLUE evaluation scripts.

---

## Evaluation Metrics & How We Measure
- **Execution Time:** Measured by inserting a timer into each test program and computing elapsed = end - start.  
- **Flash/SRAM:** Read from Arduino IDE compile output (sketch size & global variables).  
- **Complexity:** **Cyclomatic Complexity (CC)** and **NCLOC** computed with **Lizard**.  
- **Similarity:** **CodeBLEU** (n-gram, syntax, data-flow, semantic components).

---

## Reproducing the Experiments

### 1) Generate Code from Prompts
Use the provided prompt for each task. Prompts follow a fixed, model-friendly format (see **Prompt Structure** below). Store model outputs.

### 2) Compile & Measure
- Compile with **Arduino IDE 2.3.5** for memory stats (flash & SRAM).  
- Upload to the **same Uno board** and run time-measurement builds to capture runtime.

### 3) Check Correctness
- **Syntactic correctness:** successful compile.  
- **Functional correctness:** behavior matches. Failed runs enter a **feedback loop** (compiler messages + manual hints) before re-prompting the model. Record attempts until a correct solution is obtained.

### 4) Compute Complexity & Similarity
- Run **Lizard** to capture **CC** and **NCLOC**.  
- Run **CodeBLEU** against the corresponding **reference solutions**.

---

## Results Snapshot (from the Paper)
- **Execution Time:** Standard LLMs (e.g., GPT-4o, DeepSeek-V3) most often match or beat the reference speed; reasoning LLMs frequently run **longer**.  
- **Flash/SRAM:** Reasoning LLMs (especially **DeepThink R1**) consistently produce **smaller** flash and **lower** SRAM usage across many tasks.  
- **Complexity (CC/NCLOC):** Reasoning LLMs tend toward **higher CC** and **longer code**; standard LLMs are typically **simpler** and more concise.  
- **Similarity (CodeBLEU):** Standard LLMs show **higher** similarity to reference code; reasoning LLMs diverge more in structure/semantics.

> **Takeaway:** Choose **standard LLMs** for performance-critical work and **reasoning LLMs** for memory-constrained scenarios—or combine them: generate with a reasoning model, then **refactor/tune** for speed and readability.


