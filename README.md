\# Translational Bioinformatics: Automated NGS Engineering & Deep Learning Pipelines

graph TD  
    %% Node Styling Defs  
    classDef stepStyle fill:\#f9fafb,stroke:\#d1d5db,stroke-width:2px,color:\#111827;  
    classDef fileStyle fill:\#ecfdf5,stroke:\#10b981,stroke-width:2px,color:\#065f46;  
    classDef dfStyle fill:\#eff6ff,stroke:\#3b82f6,stroke-width:2px,color:\#1e40af;

    %% Workflow Connections  
    C1\[\<b\>Cell 1: SRA Download\</b\>\<br\>Downloads raw genomic data using Python subprocess utilities\] \--\>|Outputs raw data| F1(\<b\>SRR11454681\_1.fastq\</b\>\<br\>Unfiltered Sequence Archive Strings)  
     
    F1 \--\> C2\[\<b\>Cell 2: Trimming Step\</b\>\<br\>Parses Phred-33 quality metrics to isolate signal from noise\]  
     
    C2 \--\>|Saves clean fragments| F2(\<b\>SRR11454681\_trimmed.fastq\</b\>\<br\>Verified high-confidence sequences)  
     
    F2 \--\> C3\[\<b\>Cell 3: Alignment Step\</b\>\<br\>Executes a BWA-modeled seed-and-extend coordinate lookup\]  
     
    C3 \--\>|Outputs tracking metrics| D1\[\[\<b\>df\_sam\_mock\</b\>\<br\>Pandas Alignment Dataframe Matrix\]\]  
     
    D1 \--\> C4\[\<b\>Cell 4: Final Variant Caller Step\</b\>\<br\>Audits coordinate clusters to identify true biological mutations\]  
     
    C4 \--\>|Generates clinical results| D2\[\[\<b\>final\_vcf\_output\</b\>\<br\>Final VCF Variant Calling Table\]\]

    %% Assign Styles  
    class C1,C2,C3,C4 stepStyle;  
    class F1,F2 fileStyle;  
    class D1,D2 dfStyle;

An advanced, end-to-end computational biology architecture engineered purely in Python. This project demonstrates production-grade dry lab workflows for cloud data ingestion, quality filtering, genome alignment coordinates mapping, variant identification, and data compilation for deep learning neural network ingestion.

\#\# ![🚀][image1] Key Frameworks & Technical Stack  
\* \*\*Languages & Core Environments:\*\* Python, Jupyter Notebook.  
\* \*\*Bioinformatics Domain Software Tools:\*\* NCBI SRA Toolkit (\`fasterq-dump\`), BioPython (Memory-optimized file streaming architecture).  
\* \*\*Machine Learning Infrastructure:\*\* PyTorch (Dual-Tower Regressor MLP), NumPy, Pandas, SciPy.  
\* \*\*Data Visualization & Auditing:\*\* Seaborn, Matplotlib.

\---

\#\# ![🏗️][image2] Multi-Stage Pipeline Architecture

\`\`\`text  
\[NCBI SRA Cloud\] ➔ Ingestion (Subprocess fasterq-dump) ➔ Quality Control (BioPython Q30 filter)  
                      ➔ Seed-and-Extend Alignment ➔ Downstream Variant Call / Deep Learning Embedding  
\`\`\`

\#\#\# 1\. Cloud Data Ingestion (SRA Ingestion Module)  
\* \*\*Objective:\*\* Automatically downloads and streams raw paired-end next-generation sequencing data fragments from public clinical databases.  
\* \*\*Engineering Logic:\*\* Interfaces with the command-line \*\*NCBI SRA Toolkit\*\* using a managed Python \`subprocess\` routine. Implements string formatting filters and a selective \`--maxReads 10000\` down-sampling parameter to optimize memory storage constraints during computational testing.

\#\#\# 2\. Quality Control & Adapter Trimming Module  
\* \*\*Objective:\*\* Cleans raw text string sequencing datasets (\`FASTQ\`), isolating real genetic mutations from instrument-generated machine error artifacts.  
\* \*\*Engineering Logic:\*\* Streams multi-gigabyte data files via a space-efficient \`BioPython\` generator loop. Parses positional \*\*Phred-33 quality attributes\*\* to compute geometric mean scores across reading frames, systematically purging sequences that fall below strict high-confidence benchmarks (Q30 thresholds).

\#\#\# 3\. Coordinate Reference Genome Alignment Module  
\* \*\*Objective:\*\* Re-assembles fragmented sequence text blocks back onto a standard human reference genome backbone template.  
\* \*\*Engineering Logic:\*\* Simulates industrial \*\*BWA-MEM\*\* software alignment logic by executing a \*\*Seed-and-Extend dictionary mapping lookup\*\*. Isolates a specific 20-character sequence string seed at the reading head to rapidly identify candidate anchor coordinates, recording outputs in a tabular layout modeled on standard structural \*\*SAM/BAM file specifications\*\*.

\#\#\# 4\. Downstream Variant Calling & Feature Compilations  
\* \*\*Objective:\*\* Scans structural coordinate arrays to identify Single-Nucleotide Variants (SNVs/SNPs) and formats data tensors for AI models.  
\* \*\*Engineering Logic:\*\* Iterates across mapping coordinate matrices to calculate absolute positional depth. Applies filtering rules (Depth $\geq$ 10, Alternate Allele Frequency $\geq$ 70%) to call variants. Transforms rows using dictionary bit-mapping and \`np.pad\` zero-padding to create \*\*128-dimensional vectors\*\* that feed into a \*\*Dual-Tower PyTorch Regressor Neural Network\*\* for drug-target binding affinity forecasting.

\---

\#\# ![🛠️][image3] Step-by-Step Installation and Reproduction  
To download and run these pipeline notebooks on your local terminal environment:

\`\`\`bash  
\# Clone the repository  
git clone [https://github.com](https://github.com/)  
cd [ngs-analysis-deep-learning](https://github.com/kritingautam/ngs-analysis-deep-learning)

\# Install project dependencies automatically via requirements text architecture  
pip install \-r requirements.txt  
\`\`\`

Open your Python interactive space or launch \`jupyter notebook\` to execute the structural cells in sequence.

\#\#\# ![🧬][image4] Upstream Data Ingestion via SRA Toolkit  
To validate this variant pipeline using real-world clinical contexts, raw sequence text strings were fetched directly from the NCBI Sequence Read Archive (Accession: \`SRR11454681\`):

\`\`\`bash  
\# Configure local cache systems  
vdb-config \--interactive

\# Extract a 10,000 read paired-end sample array directly from the cloud  
fasterq-dump \--split-files \--maxReads 10000 SRR11454681  
\`\`\`

[image1]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABEAAAARCAYAAAA7bUf6AAABkElEQVR4XmNgIBPcsFdyAOIGdHEM8P////tAbIAsBtT4/21W6v877vr/QewFKkr7keUxANCA8zB27/r9Bg+D7MEGgDSD8EUbsCHzkfXgBEAD3m9++O7/jvO34AZAXfEfXS0cAF2gAGMDDfgPMgBEg/DK1ha4ARiGADUKoAgwIAx4+PDhf/uQeDAGiU1buBrTAGwgY9rS/6uuPgJrQjZk+4kL/53L2kH4ProehlM6hgZA/B+EF7RN/g8yBOaFuTuO/q/pnPD/7PmL/wtnrQIbgq4fbMAuTW24P2FhgGwQCHes3oPTgPcwzTAM03RIWx9uUHz3HOwGwAAorqEGOLS2tv7fHhoLNmDi1EVgA0Bh4ZhciNsAZPD9uu//vbaOYAPm6+mBDYAGIvEG/P6w5f9xHYP/C1RV/oNc1G5lC/bqYlVlwoYADVCAGXBzSd3/X68X/geJHQW6CBRbq9XUiDIE7IqfTxr//363DmQAKHzew6OcmIQF1NQAxA4gzUAMT7kgA0BRj6yWZAAOHxUljOyADgDerFhR/dB+qQAAAABJRU5ErkJggg==>

[image2]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABEAAAARCAYAAAA7bUf6AAABHklEQVR4XmNgGLSgp63u/+eJMv9bW1thuABdDU4A1aAAMgDEB9LvkeT6kQxVgGuCAZAmIHZAomEY7CI0fgCIDdOHbgjMdhSNULH3SPIGUAx2JdwgIKP/Rp/ZfxB+UiZ5/1aixH8YRjJ0Pwzf6DP//7hf+z6SWAPYoAkTJvzfsGHD/4uBYgKvGqTeA2mH143SYAOWX7iGcDYDKHzaUfhwADJk6dKlcEkk2/8/WOi9H1kt0BAUPlYA1FjwGRqQ6HIg8HGCNFZxFAB1BTzw0MG1XjOiDBGAeQddDgSA3sFqOAqAGtCAyzv/A/n/A3EAujgKgBpyHtkld3i1/oMwyAAsbEwXQw1A8Q4WjbgNgXqjH+YdEI2igBgAsh0do6vBBgBU/xnALsUjOQAAAABJRU5ErkJggg==>

[image3]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABEAAAARCAMAAAAMs7fIAAADAFBMVEUAAACCrsCCrsCCrsCCrsCCrsCCrsCCrsCCrsCCrsCCrsCCrsCCrsCCrsCCrsCCrsCGssNAg5QveIkveIkveIkveIkveIkveIkveIlEhpcveIkveIltobJqn7BzpLYveIkveIkveImArr99UTN9UTMveImgaEE4fo98qryAhIBBhJUveImgaEF9UTOgaEGIoKd9UTN9UTN9UTN9UTN9UTOHWDegaEGgaEGRakuYaUagaEFimaugaEFJdHgveImgaEF0pbegaEGgaEGgaEGgaEGgaEGgaEGgaEGCrsCTv82k0Nqr1+C55Oqv2uKMuMiFscOQvMueydWaxtKy3eWJtcWo092hzNi24edtobKXwtAveIl4p7k5f5BZk6U0e4xelqhEhpd9q70/gpNOjJ5ypLZjmqtJiZqCqLd+Yk1oobCBnaZ9Vzx9UTOAkZR/UjSAi4uGVzegaEF/dGiPXTpTkKGXYj6IWDeTXzyebEmIoahona+BVDWccVGEqriadVk7eog2d4WZaUZEdXxZcm5ocGV2blyLa08AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA7qDuVAAAASHRSTlMAEEBgn7/PgDBQj3Ag3++v75/fEEAgn7+AQHDvv3Cvz69gz5+AMGCP76/fjzDP7+8Q3zDvUHCfEO/fz8+Pz1CvYEAgv99QcIBFqgoOAAAA5ElEQVR4XmNggAImJgYGZlYggxnMZfVSevmDIVxa6fFfBkaQgN+/PzsYGCI+MABJBhYg5vsF0QcixJhBIj7vgKKfQHwPiRcHmRh8fBjkGFTjQPIMDC8YvjOqmr5juPs4hYH1OoMQAyPTYqDJUQzvgAYWMrBfuHsbpJOFYZn2XSDN//HnR7AAxHagkQwWHxkY+kFMsJUMvgwMsxlAWmEiPr8ZGJ6CFOgwgH3B4fGHAeTaE5YMyv+fAkU8FP6BBcBCsv+eMjOoHLmmAhYAC8lxMjO8slbZCRFgYPimxLAcxoYCZwYGAMKcOjB8XfLuAAAAAElFTkSuQmCC>

[image4]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABEAAAARCAYAAAA7bUf6AAABJklEQVR4XmNgIAd0Vu8HY1LAu57//7FhdHU4AbpGLBi/i541f/+/2n3Pf734Z2AMEpt3w/L/5u57+4k2BGTAgr1B/4EaBYCGJMAMcjjy/7/GunP/geFC2EsgQ0AYZDvIIL/0VwmwsLA58B2PIfuXJgCxA4gJMgBkK4hdfbEZxBYAGgIxCGTA/qVohuxfuh4siAVHnjz1HqQEZCDIoPv9PxHySAYooGskEisgDNmzCOw8mNOBzj0P87vIwYPoGiEYHeTu94MHEsygdbXfwbEBC1xUHdgA0ABoDCgADTFIPrMVrAloCChqiTNEYMYcsEtABoH4QNoAxibKJaAUB0t9x3pe7ofGwHyQHMggmBy6PhSAbAgujK4HJ0DXiIQF0NXiBuSUEVAAAEI0fDimMQqzAAAAAElFTkSuQmCC>