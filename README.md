**AdmixCorC: Admixture Inference via Kinship-Informed Ancestral Coancestry**

AdmixCorC is a high-performance C++ implementation for admixture and population history inference that leverages the genetic covariance structure derived from unbiased kinship estimates. This tool provides a computationally lightweight and highly interpretable alternative to traditional likelihood-based methods in population genetics.

**AdmixCorC's Innovation:**

    • Avoids Massive Matrices: Unlike existing methods that handle large P matrices or full individual coancestry overlays, AdmixCorC introduces a streamlined parameterization.
    • Direct Ancestral Modeling: We directly model the ancestral population history by calculating a compact K x K ancestral coancestry matrix Psi, leveraging the absolute IBD probabilities from the popkin kinship estimates.
    • Enhanced Performance and Interpretability: This approach significantly reduces computational load, allows for quick inferences even with sparse SNP data, and provides clear biological interpretability by connecting estimated parameters directly to IBD processes.
AdmixCorC serves as a scalable and interpretable alternative to traditional likelihood-based, PCA-based, and individual-level coancestry methods.

**AdmixCorC: Key Innovation**

    • Directly Modeling Ancestral Coancestry Psi: We estimate a compact K x K ancestral coancestry matrix Psi based on absolute Identity By Descent (IBD) probabilities derived from popkin-informed kinship estimates.
    • Avoiding Large Matrices: By parameterizing the problem around Psi rather than the massive allele frequency matrix P or full individual coancestry matrices, we significantly reduce computational requirements and memory overhead.
    • Enhancing Biological Interpretability: Our direct estimation of Psi offers a clear, interpretable connection to fundamental IBD processes and coalescence times (Slatkin, 1991).

**Installation and Compilation (C++)**

AdmixCorC is written in C++ for optimal speed and efficiency in processing large genomic datasets.

Prerequisites

You will need a C++ compiler supporting at least C++11 and the make utility. Dependencies are typically managed within the project's lib directory or linked during compilation.

Building the Executable

    1. Clone the Repository:
       Bash
       git clone https://github.com/amikasood/AdmixCorC.git
       cd AdmixCorC
    2. Compile the Project:
       Navigate to the project root and run make. This process will compile the source files located in main/ and lib/ to produce the main executable, typically named AdmixCorC.
       Bash
       # (Assuming a Makefile is present in the root or build directory)
       make
    3. Check for Executable:
       The resulting executable should be placed in a designated location (e.g., the root directory or the build/ directory).
       Bash
       # Example to confirm compilation
       ./AdmixCorC --help

**Usage**

The AdmixCorC program requires pre-calculated kinship data, typically a kinship matrix produced by the popkin software (or an equivalent tool that outputs kinship/coancestry estimates Theta.

Command Line Structure (Example)

The executable is likely run with command-line arguments specifying the input matrix, the target number of ancestral populations K, and output file paths.

Bash

./AdmixCorC \
    --input-kinship <path/to/kinship_matrix.txt> \
    --K <number_of_ancestral_populations> \
    --output-Q <path/to/output_Q.txt> \
    --output-Psi <path/to/output_Psi.txt> \
    [--max-iterations <N>] \
    [--tolerance <value>]

Input Data Format

The primary input is expected to be a square matrix of individual coancestry/kinship coefficients Theta, derived from the popkin framework, which ensures the coefficients are on the absolute IBD probability scale. This matrix should be formatted as a standard delimited text file (e.g., space or tab-separated).

Output Files

The program outputs the two main matrices:

    1. output_Q.txt: The estimated admixture proportions Q matrix (Individuals x Ancestors).
    2. output_Psi.txt: The estimated ancestral coancestry matrix (Psi) (K x K matrix).
