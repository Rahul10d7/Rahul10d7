<h1 align="center">Rahul Cheruku</h1>

<p align="center">
  <b>Systems &amp; Computer Engineer · MS in Artificial Intelligence @ UT Austin</b><br>
  I came from embedded systems and FPGAs, so I care less about how big a model is than whether it runs.
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/rahul-cheruku-25b2b6209/">
    <img src="https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn">
  </a>
  <a href="mailto:rahulcheruku10d7@gmail.com">
    <img src="https://img.shields.io/badge/Email-Reach%20out-EA4335?style=for-the-badge&logo=gmail&logoColor=white" alt="Email">
  </a>
  <a href="https://github.com/Rahul10d7/Portfolio-Website">
    <img src="https://img.shields.io/badge/Portfolio-Visit-2ea44f?style=for-the-badge&logo=github&logoColor=white" alt="Portfolio">
  </a>
</p>

---

## About me

I spent my undergraduate degree working on the layers underneath the model.
Systems and Computer Engineering at Carleton University meant Verilog on a Zynq
FPGA, STM32 firmware talking over I2C and SPI, RTOS task scheduling, and cache
memory design. My projects were an autonomous vehicle control system where an
STM32, an Arduino and a Raspberry Pi had to agree with each other over CAN, and
an autonomous snow plough that had to detect obstacles in real time on a
microcontroller's budget.

That background is the reason I approach machine learning the way I do. When I
read a paper my first question is what it costs to run, because I have spent
enough time fitting things into 64 KB of RAM to distrust any result that ignores
its own footprint.

I am now doing an MS in Artificial Intelligence at UT Austin, and the work has
converged on three questions:

**Can I make it small enough to matter?** This is where the hardware background
pays for itself directly. I took a 72 MB network down to 7.98 MB using 4-bit
block quantization and then a hand-rolled 3-bit scheme, packing eight 3-bit
values into three bytes with vectorised bit shifts because three bits do not
divide into a byte. Nine times smaller, still accurate, trained through LoRA and
QLoRA adapters rather than full fine-tuning. It is the same instinct as embedded
optimisation applied to a different substrate.

**Can I explain what the model learned?** Predicting ICU mortality from
intensive care records, my random forest hit 0.837 AUC and I almost stopped
there. SHAP showed the most influential feature was ICU length of stay, which is
not available at admission and is partly a *consequence* of the outcome I was
predicting. The model was reading the answer off the back of the page. Catching
that mattered more than the AUC, and no accuracy metric would ever have shown it.

**Can better training beat a bigger model?** Instead of reaching for more
parameters, I took a 360M parameter language model from 54% to 83% on a reasoning
task using chain-of-thought prompting, then supervised fine-tuning, then
rejection sampling to build a training set from the model's own successful
attempts. Same weights, better teaching.

I also try to report the results that did not go my way. Linear regression beat
gradient boosting on my volatility forecasting project. A CNN beat my transformer
planner. My LSTM lost to a decision tree on the same data. Those are in the
write-ups too, because the explanation is usually the interesting part.

---

## What I am working on now

- **Vision-language models** — fine-tuning SmolVLM for visual question answering and building a CLIP-style contrastive model from scratch. Actively in progress.
- **Preference optimization** — moving beyond rejection sampling, which throws away every failed rollout, toward methods that learn from both sides.
- **Sub-4-bit inference** — where quantization quality actually breaks down, and how to measure that honestly rather than quoting compression ratios without an error budget.
- **Clinical ML** — calibration and fairness auditing for models that carry real consequences.

---

## Projects

### Public

| Project | What it is |
| --- | --- |
| **[AI Meal Planner](https://github.com/Rahul10d7/AI-Meal-Planner)** | Streamlit app turning your fridge contents into a recipe, running LLaMA 3.2 locally through Ollama. No API keys, no fees, and your data never leaves the machine. |
| **[Facial Recognition Attendance](https://github.com/Rahul10d7/Facial-Recognition-Project)** | Real-time face recognition attendance logging with OpenCV, including confidence-threshold tuning and duplicate-entry prevention across varying lighting. |
| **[market-volatility-ml](https://github.com/Rahul10d7/market-volatility-ml)** | Forecasting S&P 500 volatility. Linear regression beat both ensemble methods, and the write-up explains why that is close to what theory predicts. |
| **[deep-learning-portfolio](https://github.com/Rahul10d7/deep-learning-portfolio)** | A written tour of my graduate deep learning work: architectures, results, and what broke along the way. |
| **[Portfolio Website](https://github.com/Rahul10d7/Portfolio-Website)** | Personal site, hand-built in HTML, CSS and JavaScript. |

### Machine learning for healthcare

Open-ended research projects on intensive care data, with full code. No patient
data is redistributed in any of these, per the PhysioNet data use agreement.

| Project | What it is |
| --- | --- |
| **[icu-mortality-xai](https://github.com/Rahul10d7/icu-mortality-xai)** | 0.837 AUC predicting ICU mortality, then SHAP revealed the top feature leaked the outcome. The interpretability pass invalidated the model, and that finding mattered more than the score. |
| **[sepsis-sql-analytics](https://github.com/Rahul10d7/sepsis-sql-analytics)** | Ten escalating BigQuery analyses tracing sepsis through the ICU, from cohort building to window functions and set operations. |
| **[clinical-notes-nlp](https://github.com/Rahul10d7/clinical-notes-nlp)** | Named entity recognition over discharge summaries, comparing spaCy, scispaCy and medspaCy, then Word2Vec and ClinicalBERT embeddings. |
| **[icu-risk-ml-dl](https://github.com/Rahul10d7/icu-risk-ml-dl)** | Three modelling lenses on the same cohort: gradient boosting at 0.846 AUC, PCA and k-means phenotyping, and a bidirectional LSTM that lost to the tree model. |
| **[llm-clinical-prompting](https://github.com/Rahul10d7/llm-clinical-prompting)** | Zero-shot, few-shot, chain-of-thought and tree-of-thought prompting for diabetes screening. A TF-IDF baseline beat all of them. |
| **[mimic-visual-explorer](https://github.com/Rahul10d7/mimic-visual-explorer)** | Six visual perspectives on ICU care, each chosen because the question demanded that specific chart type. |
| **[icu-mortality-tutorial](https://github.com/Rahul10d7/icu-mortality-tutorial)** | A peer-reviewed teaching notebook with a synthetic demo mode, so it runs without credentialed access. |

### Graduate deep learning

These are graded assignments with course autograders, so the solution code stays
private. The [portfolio](https://github.com/Rahul10d7/deep-learning-portfolio)
covers each in detail, and I am glad to walk through any implementation.

| Project | Highlight |
| --- | --- |
| Model compression and LoRA | 72 MB → 7.98 MB via 4-bit and custom 3-bit block quantization |
| Autoregressive image generation | Patch autoencoder → binary spherical quantization → causal transformer, with arithmetic coding at 19.5x |
| LLM reasoning | 54% → 83% on unit conversion through rejection fine-tuning |
| Road segmentation | Dual-head U-Net, 0.794 mIoU with simultaneous depth regression |
| Neural driving planners | MLP, Perceiver-style transformer and CNN waypoint planners compared head to head |

---

## Experience

**Infrastructure Design Technician** · Planview Utility Services · May 2024 – May 2025
Engineering design and simulation for city utility expansion using AutoCAD and
SpidaCalc, validating pole-line and grid calculations before field installation
and cutting design revisions by 35%.

**Technical Standards Engineering** · Hydro Ottawa · Jan 2023 – Dec 2023
Standards validation and compliance support for electrical distribution
infrastructure. Automated document workflows on Google Cloud Platform, reducing
retrieval time by 60%.

---

## Education

**MS, Artificial Intelligence** · University of Texas at Austin · Jan 2026 – Present

**BEng, Systems and Computer Engineering** · Carleton University · Graduated June 2025
Dean's List, 2023–2025

---

## Tools I reach for

**AI and ML**

<p>
  <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white" alt="PyTorch">
  <img src="https://img.shields.io/badge/Hugging%20Face-FFD21E?style=flat-square&logo=huggingface&logoColor=black" alt="Hugging Face">
  <img src="https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikitlearn&logoColor=white" alt="scikit-learn">
  <img src="https://img.shields.io/badge/OpenCV-5C3EE8?style=flat-square&logo=opencv&logoColor=white" alt="OpenCV">
  <img src="https://img.shields.io/badge/pandas-150458?style=flat-square&logo=pandas&logoColor=white" alt="pandas">
  <img src="https://img.shields.io/badge/NumPy-013243?style=flat-square&logo=numpy&logoColor=white" alt="NumPy">
  <img src="https://img.shields.io/badge/Streamlit-FF4B4B?style=flat-square&logo=streamlit&logoColor=white" alt="Streamlit">
</p>

**Embedded and hardware**

<p>
  <img src="https://img.shields.io/badge/C%2FC%2B%2B-00599C?style=flat-square&logo=cplusplus&logoColor=white" alt="C/C++">
  <img src="https://img.shields.io/badge/STM32-03234B?style=flat-square&logo=stmicroelectronics&logoColor=white" alt="STM32">
  <img src="https://img.shields.io/badge/Arduino-00878F?style=flat-square&logo=arduino&logoColor=white" alt="Arduino">
  <img src="https://img.shields.io/badge/Raspberry%20Pi-A22846?style=flat-square&logo=raspberrypi&logoColor=white" alt="Raspberry Pi">
  <img src="https://img.shields.io/badge/Verilog%20%2F%20VHDL-1A1A1A?style=flat-square" alt="Verilog and VHDL">
  <img src="https://img.shields.io/badge/Xilinx%20Vivado-E01F27?style=flat-square&logo=amd&logoColor=white" alt="Xilinx Vivado">
  <img src="https://img.shields.io/badge/ROS-22314E?style=flat-square&logo=ros&logoColor=white" alt="ROS">
</p>

**Cloud, data and tooling**

<p>
  <img src="https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazonwebservices&logoColor=white" alt="AWS">
  <img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white" alt="Docker">
  <img src="https://img.shields.io/badge/SQL-4479A1?style=flat-square&logo=postgresql&logoColor=white" alt="SQL">
  <img src="https://img.shields.io/badge/BigQuery-669DF6?style=flat-square&logo=googlebigquery&logoColor=white" alt="BigQuery">
  <img src="https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black" alt="Linux">
  <img src="https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white" alt="Git">
  <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black" alt="JavaScript">
</p>

**Specifically:** LoRA and QLoRA adapters, post-training quantization, SHAP and
LIME, U-Net segmentation, causal transformers, vector quantization,
chain-of-thought prompting, rejection sampling, UART/SPI/I2C, RTOS scheduling,
and FPGA digital design.

---

## Activity

<p align="center">
  <img src="https://github-readme-stats.vercel.app/api?username=Rahul10d7&show_icons=true&hide_border=true&include_all_commits=true&count_private=true&theme=default" alt="GitHub stats" height="165">
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=Rahul10d7&layout=compact&hide_border=true&langs_count=8&theme=default" alt="Top languages" height="165">
</p>

---

<p align="center">
  <i>Open to internships and research collaborations in efficient deep learning,<br>
  interpretability, embedded ML, and machine learning for healthcare.</i>
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/rahul-cheruku-25b2b6209/"><b>Connect with me on LinkedIn →</b></a>
</p>
