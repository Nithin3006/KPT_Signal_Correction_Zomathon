# KPT_Signal_Correction_Zomathon
Statistical signal correction framework to improve Kitchen Prep Time (KPT) prediction by reducing merchant bias, detecting noisy labels, modeling kitchen congestion, and improving ETA stability.

📌 Problem Overview
Kitchen Prep Time (KPT) plays a critical role in Zomato’s delivery ecosystem. It directly impacts:

Rider dispatch timing

Customer ETA accuracy

Rider idle time

Order delays and cancellations

Currently, KPT labels rely heavily on merchant-marked Food Order Ready (FOR) timestamps. However, these timestamps may be influenced by rider arrival behavior, operational delays, and hidden kitchen congestion.

This introduces systematic bias and noise into the KPT signal.

🎯 Objective

Improve KPT prediction accuracy by strengthening and enriching input signals — without overhauling the existing ML model.
Instead of increasing model complexity, this solution focuses on statistical signal correction.

🧠 Core Insight

Observed_KPT ≠ True_KPT

Observed_KPT = True_KPT + Bias + Noise

If the input signal is contaminated, prediction accuracy is fundamentally limited.

Therefore, improving label quality yields higher impact than model tuning alone.

🏗 Solution Architecture

This project introduces a Statistical Signal Correction Layer consisting of:

1️⃣ Synthetic Dataset Generation

  200 heterogeneous merchants
  
  40,000+ simulated orders
  
  Merchant-level marking bias
  
  Rider arrival influence
  
  Peak-hour rush simulation
  
  Poisson-based kitchen load
  
2️⃣ Merchant-Level Bias Estimation

  Median-based estimation of marking bias
  
  Correction of systematic inflation
  
3️⃣ Robust Statistical Estimation

  Winsorization (5th–95th percentile clipping)
  
  Reduces heavy-tail distortion
  
4️⃣ Noisy Label Detection

  Hypothesis testing using Pearson correlation
  
  Detects rider-influenced marking behavior
5️⃣ Kitchen Rush Modeling (Queue Theory)

  Using Little’s Law:
  L = λW
  Kitchen Load Index approximates hidden congestion due to:
    Dine-in orders
    
    Competitor platform load
    
    Peak-hour demand
    
6️⃣ Dynamic Bayesian Updating

  Prep time dynamically adjusted using:
  
    Historical prior
    Current congestion likelihood
    
7️⃣ Merchant Reliability Scoring
  Variance-based reliability metric:
  
  Reliability Score = 1 / (1 + Variance)
  
  Higher variance → Lower reliability.
  
📊 Evaluation Metrics

  Model performance evaluated using:
  
    Mean Absolute Error (MAE)
    
    P90 Absolute Error
  The signal-corrected approach demonstrates improved stability and reduced peak-hour volatility compared to raw observed KPT.
📁 Repository Structure

├── zomathonproblemstatement1.ipynb

├── synthetic_kpt_dataset.csv

└── README.md

🚀 How to Run
  Install required libraries:
    pip install numpy pandas matplotlib scipy
    
    Run the script:
    
    zomathonproblemstatement1.ipynb
    
    Outputs generated:
    
    Synthetic dataset (CSV)
    
    Evaluation results (CSV)
    
    Visualizations
    
📈 Business Impact

  This approach improves:
  
      Rider wait time
      
      ETA P50 stability
      
      ETA P90 tail control
      
      Order delay reduction
      
By improving signal reliability, downstream dispatch decisions become more accurate and scalable across large merchant ecosystems.

⚠ Limitations

  Synthetic dataset used (no production data)
  
  Assumptions made for rider behavior modeling
  
  Further validation required on real merchant data

🏆 Key Takeaway
KPT inaccuracy is fundamentally a signal contamination problem.
Improving input signal quality delivers higher long-term ROI than increasing model complexity — especially at marketplace scale.
