# Translational Bioinformatics: Automated NGS Engineering & Deep Learning Pipelines

```mermaid
graph TD
    %% Node Styling Defs
    classDef stepStyle fill:#f9fafb,stroke:#d1d5db,stroke-width:2px,color:#111827;
    classDef fileStyle fill:#ecfdf5,stroke:#10b981,stroke-width:2px,color:#065f46;
    classDef dfStyle fill:#eff6ff,stroke:#3b82f6,stroke-width:2px,color:#1e40af;

    %% Workflow Connections
    C1[<b>Cell 1: SRA Download</b><br>Downloads raw genomic data using Python subprocess utilities] -->|Outputs raw data| F1(<b>SRR11454681_1.fastq</b><br>Unfiltered Sequence Archive Strings)
   
    F1 --> C2[<b>Cell 2: Trimming Step</b><br>Parses Phred-33 quality metrics to isolate signal from noise]
   
    C2 -->|Saves clean fragments| F2(<b>SRR11454681_trimmed.fastq</b><br>Verified high-confidence sequences)
   
    F2 --> C3[<b>Cell 3: Alignment Step</b><br>Executes a BWA-modeled seed-and-extend coordinate lookup]
   
    C3 -->|Outputs tracking metrics| D1[[<b>df_sam_mock</b><br>Pandas Alignment Dataframe Matrix]]
   
    D1 --> C4[<b>Cell 4: Final Variant Caller Step</b><br>Audits coordinate clusters to identify true biological mutations]
   
    C4 -->|Generates clinical results| D2[[<b>final_vcf_output</b><br>Final VCF Variant Calling Table]]

    %% Assign Styles
    class C1,C2,C3,C4 stepStyle;
    class F1,F2 fileStyle;
    class D1,D2 dfStyle;
```

An advanced, end-to-end computational biology architecture engineered purely in Python. This project demonstrates production-grade dry lab workflows for cloud data ingestion, quality filtering, genome alignment coordinates mapping, variant identification, and data compilation for deep learning neural network ingestion.

---

## 🚀 Key Frameworks & Technical Stack

* **Languages & Core Environments:** Python, Jupyter Notebook.
* **Bioinformatics Domain Software Tools:** NCBI SRA Toolkit (`fasterq-dump`), BioPython (Memory-optimized file streaming architecture).
* **Machine Learning Infrastructure:** PyTorch (Dual-Tower Regressor MLP), NumPy, Pandas, SciPy.
* **Data Visualization & Auditing:** Seaborn, Matplotlib.

---

## 🏗️ Multi-Stage Pipeline Architecture

```text
[NCBI SRA Cloud] ➔ Ingestion (Subprocess fasterq-dump) ➔ Quality Control (BioPython Q30 filter)
                      ➔ Seed-and-Extend Alignment ➔ Downstream Variant Call / Deep Learning Embedding
```

### 1. Cloud Data Ingestion (SRA Ingestion Module)
* **Objective:** Automatically downloads and streams raw paired-end next-generation sequencing data fragments from public clinical databases.
* **Engineering Logic:** Interfaces with the command-line **NCBI SRA Toolkit** using a managed Python `subprocess` routine. Implements string formatting filters and a selective `--maxReads 10000` down-sampling parameter to optimize memory storage constraints during computational testing.

### 2. Quality Control & Adapter Trimming Module
* **Objective:** Cleans raw text string sequencing datasets (`FASTQ`), isolating real genetic mutations from instrument-generated machine error artifacts.
* **Engineering Logic:** Streams multi-gigabyte data files via a space-efficient `BioPython` generator loop. Parses positional **Phred-33 quality attributes** to compute geometric mean scores across reading frames, systematically purging sequences that fall below strict high-confidence benchmarks (Q30 thresholds).

### 3. Coordinate Reference Genome Alignment Module
* **Objective:** Re-assembles fragmented sequence text blocks back onto a standard human reference genome backbone template.
* **Engineering Logic:** Simulates industrial **BWA-MEM** software alignment logic by executing a **Seed-and-Extend dictionary mapping lookup**. Isolates a specific 20-character sequence string seed at the reading head to rapidly identify candidate anchor coordinates, recording outputs in a tabular layout modeled on standard structural **SAM/BAM file specifications**.

### 4. Downstream Variant Calling & Feature Compilations
* **Objective:** Scans structural coordinate arrays to identify Single-Nucleotide Variants (SNVs/SNPs) and formats data tensors for AI models.
* **Engineering Logic:** Iterates across mapping coordinate matrices to calculate absolute positional depth. Applies filtering rules (Depth ≥ 10, Alternate Allele Frequency ≥ 70%) to call variants. Transforms rows using dictionary bit-mapping and `np.pad` zero-padding to create **128-dimensional vectors** that feed into a **Dual-Tower PyTorch Regressor Neural Network** for drug-target binding affinity forecasting.

---

## 🛠️ Step-by-Step Installation and Reproduction

To download and run these pipeline notebooks on your local terminal environment:

```bash
# Clone the repository
git clone https://github.com
cd translational-bioinformatics-pipelines

# Install project dependencies automatically via requirements text architecture
pip install -r requirements.txt
```

Open your Python interactive space or launch `jupyter notebook` to execute the structural cells in sequence.

---

### 🧬 Upstream Data Ingestion via SRA Toolkit

To validate this variant pipeline using real-world clinical contexts, raw sequence text strings were fetched directly from the NCBI Sequence Read Archive (Accession: `SRR11454681`):

```bash
# Configure local cache systems
vdb-config --interactive

# Extract a 10,000 read paired-end sample array directly from the cloud
fasterq-dump --split-files --maxReads 10000 SRR11454681
```
## 🔗 Downstream Modular Extensions
This pipeline operates as a modular upstream data engineering workspace. To see how these structured genomic variants and multi-omics arrays are tokenized into 128-dimensional tensors to train deep learning models, explore the downstream [Dual-Tower PyTorch Geometric Repository](https://github.com).
