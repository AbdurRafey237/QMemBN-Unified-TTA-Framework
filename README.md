# Q-MemBN+: Memory-Robust Few-Shot Test-Time Adaptation for Small Vision Models

**Q-MemBN+** is my unified framework for **test-time adaptation (TTA)** designed for **small vision models** deployed in **dynamic, noisy, real-world environments** (edge devices, robotics, assistive systems, etc.).

It combines:
- **Quantile BatchNorm (Q-BN)**
- **Prototype-guided self-training**
- **Memory-augmented statistics**
- **Entropy-based filtering**
- **Drift detection + resets**

to deliver **robust, low-latency adaptation** without retraining or labels.

---

## 🙄 Why?

Small models deployed into the wild degrade under:
- Distribution shift  
- Environmental drift  
- Non-i.i.d. test streams  
- Noise / adversarial corruption  

Traditional solutions:
- Re-training → slow, expensive  
- Larger models → infeasible on edge  

**Q-MemBN+ adapts online, using only unlabeled test data, in real-time.**

---

## 🧪 Key Ideas

### 1. Support Initialization (Few-Shot, Offline)
Use **5-shot labeled support samples per class** to:
- Initialize prototypes  
- Warm-start Q-BN statistics  
- Fine-tune with augmentation  
- Stabilize initial deployment

---

### 2. Online Adaptation (Self-Supervised, Streaming)

For each batch in the incoming stream:

1. **Forward Pass**  
   Obtain predictions using Q-BN memory stats  

2. **Entropy Filter**  
   Skip low-confidence samples from adaptation  

3. **Prototype Check**  
   Verify pseudo-labels via prototype similarity  

4. **Update**  
   Apply selective gradient updates to BN parameters  

5. **Memory Update**  
   Update BN queues + prototypes (EMA)  

6. **Drift Reset**  
   Detect distribution shifts; reset memory when unstable  

**Goal:** adapt quickly, avoid catastrophic drift.

---

## 📊 Results (CIFAR-10-C Streaming)

**Objective 1: Accuracy Under Shift**  
- +0.87 pp over static  
- Consistent across metrics  

**Objective 2: Close the Oracle Gap**  
- Oracle gap: 4.09 pp  
- Q-MemBN+: reduces to 3.22 pp  

**Objective 3: Robustness to 20% Poisoned Inputs**  
- Outperforms naive adaptation marginally
- Naive, clean both significantly outperform standard ResNet-18.

**Objective 4: Efficiency**  
- Latency: **28.08 ms at b=1** (budget 30 ms)  
- Params: **11.17M** (budget ≤50M)  

---

## 🏗️ Architecture

- ResNet-18 backbone  
- Q-BN layers replace vanilla BN  
- Prototype memory & queues  
- Lightweight optimization loop

---

## 🗂️ Files

- aRafey_DL_Project_Complete.pdf -- The IEEE-standard report of my project.
- aRafey_DL_Project_Notebook.ipynb -- The Jupyter Notebook of my project. Contains in-depth explanations and commentation for stand-alone understanding.
- aRafey_DL_Project_Presentation.pdf -- The presentation of my project. I recommend viewing it on Gamma though! (https://gamma.app/docs/Memory-Robust-Few-Shot-Test-Time-Adaptation-for-Small-Vision-Mode-vzukrurqbinyq7a?mode=doc)
- aRafey_DL_Project_Flowchart.png -- The flowchart of the pipeline of my project.
- GPTZero AI Scan - aRafey_DL_Project_Complete.pdf.pdf -- The GPTZero AI and Plagiarism report of the report of my project.

---

## ☎️  Contact

**Questions? Email them at:**  
- arafey.bsds23seecs@seecs.edu.pk
