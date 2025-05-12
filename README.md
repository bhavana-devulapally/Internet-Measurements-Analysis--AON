
# Internet Measurements Analysis

A traceroute-based study of internet path stability at both router and AS levels, with delay metrics.

## 🔍 Project Overview
This project automates end-to-end traceroute measurements to five major domains over five days, then analyzes:
- **Router-level paths**: dominant routes, path similarity and change frequency  
- **AS-level paths**: common AS sequences and their stability  
- **Delay metrics**: hop-by-hop RTT, end-to-end delay, packet loss rate  
- **Stability index**: combines path consistency and delay variance into a single metric

## 🛠 Tech Stack
- **Shell**: `bash` traceroute loops  
- **Python 3**: data parsing & AS lookup  
  - `subprocess`, `os`, `pandas`  
- **Data storage**: CSV files  
- **Visualization**: Matplotlib (latency vs. hop plots)  
- **AS lookup**: Team Cymru WHOIS API  

## 📁 Repository Structure
```

/traceroute-scripts
├── run\_traceroutes.sh       # Bash script to collect raw traceroute outputs
├── compile\_traceroutes.py   # Python: parse traceroute text → combined CSV
└── enrich\_as\_info.py        # Python: append AS Number & AS Name via whois
/data
├── raw/                     # Daily folders of traceroute text files
└── processed/               # Final CSVs for analysis
/plots
└── hop\_latency.png          # Example latency vs. hop number plot
README.md                      # (this file)

````

## ⚙️ Getting Started

1. **Clone the repo**  
   
   git clone https://github.com/yourusername/internet-measurements.git
   cd internet-measurements


2. **Install dependencies**


   pip install pandas matplotlib
  

3. **Run traceroutes**

 
   bash traceroute-scripts/run_traceroutes.sh
   

   * Adjust `destinations` and `measurements_per_destination` in the script as needed.

4. **Compile raw outputs**

   ```bash
   python traceroute-scripts/compile_traceroutes.py \
     --input-dir data/raw/2023-11-28 \
     --output data/processed/traceroute_all.csv
   ```

5. **Enrich with AS info**

   ```bash
   python traceroute-scripts/enrich_as_info.py \
     --input data/processed/traceroute_all.csv \
     --output data/processed/traceroute_all_with_as.csv
   ```

6. **Generate plots & analysis**
   Open a Jupyter notebook or run your own analysis script to read the final CSV, compute:

   * Path similarity & change frequency
   * AS-level stability
   * RTT statistics (mean, max, std) per hop
   * Path Stability Index
   * And visualize latency vs. hop number

## 🎯 Key Findings

* A single dominant IP path accounted for \~50% of runs to **amazon.com**
* Higher hop counts show both increased average latency and greater variance
* AS stability was high (most runs traversed AS 7018 for AT\&T)






