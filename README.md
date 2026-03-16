# Correlation-Power-Analysis
This repository demonstrates a Chosen-Plaintext Side-Channel Attack targeting an unmasked AES-128 implementation. The project showcases how tiny fluctuations in power consumption—leaked during the hardware's S-Box operation—can be correlated with a Hamming Weight power model to reveal the secret key.

AES-128 Correlation Power Analysis (CPA) AttackThis repository contains a Python-based implementation of a Correlation Power Analysis (CPA) attack. This is a type of Side-Channel Attack used to extract the secret cryptographic key from a hardware device (like an FPGA or Microcontroller) by analyzing its physical power consumption during the encryption process.

📖 Overview : 
Standard digital security assumes that an attacker only has access to inputs and outputs. However, physical hardware leaks information through "side channels" such as power consumption, electromagnetic radiation, and timing.This project demonstrates how a Chosen-Plaintext Attack can bypass AES-128 security by correlating a mathematical power model (Hamming Weight) with real-world power measurements using the Pearson Correlation Coefficient.

🚀 How It Works :
The attack follows these logical steps:
Data Acquisition: We collect power traces ($t_i$) while the device encrypts known plaintexts.
Power Modeling: We use the Hamming Weight model to predict the power used during the first S-Box operation.
Hypothesis Testing: We calculate the predicted power for every possible key byte value (0–255).
Statistical Analysis: We use the Pearson Correlation Coefficient ($\rho$) to compare our predictions ($h_i$) against the measured traces ($t_i$).
Key Extraction: The key guess that produces the highest correlation (the "spike") is the correct secret key.

📊 Results : 
When the attack is successful, the resulting plot shows a clear distinction between the correct key and the 255 incorrect guesses. The Spike indicates the exact moment in time the secret data leaked from the hardware.
Correct Key: Identified as 0xab (Decimal: 171).
Correlation Margin: A distinct peak significantly higher than the background noise.

🛠️ Installation & SetupPrerequisites :
Python 3.xVS Code (recommended) or any Python IDEDependenciesInstall the required mathematical and plotting libraries via pip:Bashpip install numpy matplotlib
Repository Structurecpa_attack.py: The main Python script execution logic.plaintext.csv: Input data used during the encryption simulation.traces.csv: Recorded power consumption traces.

💻 Usage :
Clone the repository: Bashgit clone [https://github.com/YOUR_USERNAME/AES-128-CPA-Attack.git](https://github.com/kunalofficial687/Correlation-Power-Analysis.git)
Navigate to the project folder:Bashcd AES-128-CPA-Attack
Run the attack:Bashpython cpa_attack.py

🛡️ Countermeasures This project highlights the importance of hardware security. To prevent such attacks, developers implement:
Masking: Adding random values to intermediate data.
Hiding: Adding noise or random delays to the power consumption to flatten the spikes.
