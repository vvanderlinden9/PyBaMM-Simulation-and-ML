ABSTRACT: As space travel becomes increasingly complex and sought after with the prospects brought about by international and national space missions such as NASA’s Artemis II and Europa missions, monitoring battery safety and health in spacecraft has become even more critical. Under space conditions and stresses, electrical systems and components such as batteries face exposure to high energy particle radiation, thermal fluctuations, and operational autonomy in remote environments. The industry standard for satellite, probe, and rover batteries has been favorable in regards to Lithium-ion batteries (LiBs), which, despite their high energy density, long life cycle, and wide operating temperature range, are still vulnerable to solid electrolyte interphase (SEI) degradation, capacity fade, thermal runaway, and impedance shifts caused by these harsh conditions, significantly impacting mission success. Current spacecraft battery monitoring methods rely heavily on human oversight and telemetry data, resulting in delays or inaccuracies. This study aims to address this limitation by employing machine learning (ML) methods, such as linear (LR) and random forest (RF) regression. Utilizing the nascent PyBaMM library to artificially synthesize LiB radiation and thermal data, the ML model will be trained on labeled data to improve anomaly detection accuracy and reduce false positives in battery systems monitoring, offering future potential for real-time autonomous responses to battery health deterioration in space without human intervention. 

1. Installation Instructions
• Python version 3.11 is recommended. The project specifically requires a version lower than the most recent releases to ensure compatibility with the PyBaMM version used during development.
• The following packages were used in the stable environment:
   ◦ pybamm==25.6.0
   ◦ numpy==1.26.4 (Note: Higher versions of NumPy may cause dependency conflicts with PyBaMM)
   ◦ pandas>=1.5.0
   ◦ scikit-learn
   ◦ matplotlib
   ◦ cycler
• It is highly recommended to use a virtual environment to manage specific dependency versions:
  python3.11 -m venv venv
  source venv/bin/activate  # On Windows: venv\Scripts\activate
  pip install -r requirements.txt
2. How to Run the Code
• Notebook: Open PyBaMM_Simulation.ipynb.
• Execution Order: Cells must be run sequentially.
    1. Environment Setup: Mount Google Drive and install dependencies.
    2. Data Synthesis: Run the generate_space_battery_data function to simulate 20 temperature steps (273 K to 313 K).
    3. Visualization: Generate comparative plots for LLI, Capacity Fade, and SOH.
    4. ML Training: Execute the Linear Regression and Random Forest cells to evaluate model performance.
• Expected Runtime: Approximately 5–10 minutes for a full simulation sweep of 20 temperature steps.
• Hardware Requirements: Standard laptop CPU; no GPU acceleration is required for these specific simulations.
3. Data Description
• Type: 100% Synthetic Data generated using physics-based electrochemical modeling.
• Generation: Data is produced via the PyBaMM DFN model using the O’Kane et al. parameter set for LG M50 batteries, scaled to a 25 Ah capacity.
• Units:
    ◦ Temperature: Kelvin (K)
    ◦ Discharge Capacity: Ampere-hours (Ah)
    ◦ Radiation Dose: Gray (Gy)
    ◦ Activation Energy: kJ/mol
• Preprocessing: Data is split into 10 training steps (273-293 K) and 10 testing steps (293-313 K) to evaluate extrapolation capabilities.
4. Reproducibility Statement
• Random Seeds: The Random Forest model uses a fixed random_state=0 for the 75%/25% train-test split to ensure results remain consistent across runs.
• Determinism: The Linear Regression data split is entirely deterministic, isolating the upper temperature range for testing.
• External Datasets: No external datasets are required; all data is generated at runtime based on the physics parameters defined in the code.
5. Limitations
• DFN Model Assumptions: The model assumes maximum power transfer conditions and represents internal transport and degradation as reaction-limited.
• Radiation Modeling: Radiation impact is simplified as a linear modifier based on cumulative dose literature, which may oversimplify complex particle interactions.
• Temperature Modifiers: Degradation rates are based on empirical linear modifiers (1% deviation per Kelvin) rather than purely random data.
• Stochasticity: The synthetic dataset is ranged and deterministic, which may contribute to reduced extrapolation accuracy when compared to real-world battery behavior.
6. Citation
If you reference this work in an academic context, please use the following citation:
Vera A. van der Linden. 2025. Spacecraft Anomaly Detection: Machine Learning Based Detection of Lithium-Ion Battery Degradation in Space Conditions. In Proceedings of International Journal of Secondary Computing and Applications Research (IJSCAR VOL. 2, ISSUE 2). ACM, New York, NY, USA, 7 pages. https://doi.org/10.5281/zenodo.17107814
