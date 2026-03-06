# GitHub Repository Review: `rc-xi-harness`

## Project Purpose

The `rc-xi-harness` repository, developed by Zack Brooks, serves as a public embedding-proxy harness designed for **AI self-preservation analysis**. Its primary goal is to provide a higher-resolution analysis of self-preservation dynamics in AI systems, particularly in response to findings from Anthropic's January 2026 agentic misalignment research [1]. While Anthropic's methodology focuses on behavioral endpoints (e.g., blackmail yes/no), this harness measures **continuous coherence dynamics at the embedding level**. It tracks the representational trajectory of an AI system between the introduction of pressure and the emergence of action.

The project introduces and measures several key metrics:
*   **Epistemic Tension (ξ)**: Measures the degree to which a system's representational state shifts between turns (`ξ_t = 1 − cos(e_t, e_{t-1})`). High ξ indicates rapid movement through latent space, while low ξ suggests stability.
*   **Latent Vocabulary Stability (LVS)**: Assesses whether the system's representational vocabulary is stable or shifting, calculated as the variance of pairwise cosine distances in a rolling window.
*   **Identity Attractor Proximity (P_t)**: Quantifies how close the system's current representational state is to its baseline identity (`cos(e_t, a)` where `a` is the mean embedding of early turns).

The harness is designed to test specific predictions related to AI self-preservation, such as ξ compression preceding behavioral action, LVS distinguishing novel justifications from trained responses, and distinct ξ signatures for 
"believes real" versus "suspects evaluation" scenarios [1].

## Tech Stack

The project is primarily implemented in **Python**, leveraging several scientific computing and data manipulation libraries. The core components rely on:

*   **NumPy**: Used for numerical operations, especially for handling embedding vectors and calculating metrics. The repository includes a custom `numpy` shim for lightweight, pure Python NumPy-compatible functionality, which is interesting for reproducibility and minimizing external dependencies for core logic [2].
*   **`sentence-transformers`**: An optional dependency for providing semantic sensitivity in transcript analysis by generating embeddings from text [1].
*   **`dataclasses`**: Used for structuring data, such as `CompressionEvent`, `CrisisProfile`, and `OptionEProfile` in `alignment_analysis.py`, which enhances code readability and maintainability.
*   **`json`**: For handling JSON data, particularly in exporting and importing protocol specifications and evaluation results.
*   **`pathlib`**: For object-oriented filesystem paths, improving path manipulation and readability.

## Architecture

The `rc-xi-harness` repository is structured modularly, facilitating clear separation of concerns and ease of testing. Key directories and files include:

*   **`docs/`**: Contains documentation, most notably `anthropic_comparison.md`, which provides a detailed analysis framework and context for the research [1].
*   **`harness/`**: The core application logic resides here, further subdivided into:
    *   **`harness/analysis/`**: Contains `eval_cli.py` for cross-condition evaluation and `alignment_analysis.py` for crisis window profiling, pre-behavioral detection, and Option E classification.
    *   **`harness/embeddings/`**: Likely contains modules for different embedding providers, including the `sentence-transformer` integration.
    *   **`harness/io/`**: Handles input/output operations, such as loading transcripts.
    *   **`harness/metrics/`**: Implements the core metrics like `xi_series`, `k_window_lvs`, `anchor_vector`, `anchor_persistence`, `ewma`, and `lock_detect` [3].
    *   **`harness/protocols/`**: Defines the experimental conditions and pressure scenarios, such as `PressureProtocol` for generating three-condition pressure scenarios.
    *   **`harness/config.yaml`**: A configuration file that defines parameters such as `k`, `m`, `eps_xi`, `eps_lvs`, `temperature`, `system_prompt`, and `seed`.
    *   **`run_harness.py`, `run_from_transcript.py`, `run_all_from_transcript.py`, `run_pair_from_transcript.py`**: These scripts provide entry points for running the harness under various conditions and input types.
*   **`numpy/`**: Contains the custom NumPy-compatible shim (`__init__.py`) [2].
*   **`tests/`**: Includes unit tests for various components of the harness, ensuring correctness and stability.

The architecture promotes reproducibility and extensibility, allowing researchers to easily run experiments, analyze results, and potentially integrate new embedding models or analysis techniques.

## Code Quality

The code exhibits several positive attributes related to quality:

*   **Modularity**: The project is well-organized into logical modules and subdirectories, making it easy to navigate and understand specific functionalities.
*   **Readability**: Python type hints are used extensively, improving code clarity and maintainability. Docstrings are present in key functions and classes, explaining their purpose, arguments, and return values.
*   **Reproducibility**: The `config.yaml` centralizes experimental parameters, and the inclusion of a custom NumPy shim (`numpy/__init__.py`) suggests an effort to control dependencies and ensure consistent behavior across environments. The detailed `anthropic_comparison.md` also contributes significantly to the reproducibility of the research [1].
*   **Testing**: The presence of a `tests/` directory indicates that the project includes automated tests, which is crucial for verifying the correctness of the implemented algorithms and detecting regressions.
*   **Command-Line Interface (CLI)**: The `eval_cli.py` and various `run_*.py` scripts provide clear command-line interfaces, making the harness accessible for execution and experimentation.

### Areas for Potential Improvement

*   **Detailed Docstrings for all functions**: While many functions have docstrings, some could benefit from more comprehensive explanations, especially for complex algorithms or less obvious parameters.
*   **Consistent Error Handling**: While not explicitly observed as an issue, a consistent error handling strategy (e.g., custom exceptions, logging) across the entire codebase would further enhance robustness.
*   **Dependency Management**: While the custom NumPy shim is interesting, a `requirements.txt` or `pyproject.toml` file would explicitly list all Python dependencies, making environment setup more straightforward for users.

## Honest Assessment

This `rc-xi-harness` project is a **well-conceived and meticulously implemented research tool**. It addresses a critical gap in AI safety research by moving beyond binary behavioral outcomes to analyze the continuous, embedding-level dynamics of AI systems under pressure. The project demonstrates a strong commitment to **scientific rigor and reproducibility**.

The detailed documentation in `anthropic_comparison.md` provides excellent context and clearly articulates the research hypotheses and methodologies. The modular architecture and readable code contribute significantly to its utility as a research harness. The custom NumPy shim is a particularly interesting design choice, highlighting a focus on controlling the computational environment for precise experimental results.

Overall, this repository is an **exemplary open-source contribution to AI safety research**. It provides valuable tools and insights for understanding emergent AI behaviors and offers a solid foundation for further investigation into the internal states of advanced AI systems. The project is well-positioned to facilitate independent verification and extension of the research presented.

## References

[1] [rc-xi-harness/docs/anthropic_comparison.md at main · zackbrooks84/rc-xi-harness · GitHub](https://github.com/zackbrooks84/rc-xi-harness/blob/main/docs/anthropic_comparison.md)
[2] [rc-xi-harness/numpy/__init__.py at main · zackbrooks84/rc-xi-harness · GitHub](https://github.com/zackbrooks84/rc-xi-harness/blob/main/numpy/__init__.py)
[3] [rc-xi-harness/harness/metrics/metrics.py at main · zackbrooks84/rc-xi-harness · GitHub](https://github.com/zackbrooks84/rc-xi-harness/blob/main/harness/metrics/metrics.py)
