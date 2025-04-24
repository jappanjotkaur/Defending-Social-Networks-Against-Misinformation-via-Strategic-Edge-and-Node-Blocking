# Defending-Social-Networks-Against-Misinformation-via-Strategic-Edge-and-Node-Blocking

## Overview

This project focuses on simulating misinformation spread in social networks and using edge and node blocking techniques to mitigate the propagation. The Independent Cascade Model (ICM) is applied to simulate the spread of misinformation, and various strategies are implemented to block edges and nodes, reducing the spread.

### Features:
- Implements ICM to simulate misinformation spread in social networks.
- **Edge and Node Blocking** techniques like:
  - Random blocking
  - Blocking based on centrality (betweenness, closeness, etc.)
  - Hybrid techniques (e.g., IEED + community detection)
- Various **blocking methods** are applied to identify and remove critical connections in the network to minimize infection spread.
- Results from blocking methods show **up to 95% reduction in misinformation spread**.

## Code

Contains implementations for different edge-blocking methods, node-blocking strategies, and the Independent Cascade Model (ICM) used to simulate the spread of misinformation.

## Data

This project uses the **OGBN-Proteins dataset** from Open Graph Benchmark (OGB). It is used to create the graph and simulate misinformation propagation based on various edge-blocking strategies.

Make sure to generate the edge weights using `prob_generator.py` before running the simulations.

## Simulation

This project includes Jupyter Notebooks for simulating the edge blocking strategies and observing the results. The notebooks are designed for ease of use and visualization.

## Installation

1. **Clone repository**:
   ```bash
   git clone https://github.com/yourusername/Mitigating-Misinformation-Spreading-in-Social-Networks-Via-Edge-Blocking.git
   cd Mitigating-Misinformation-Spreading-in-Social-Networks-Via-Edge-Blocking
   ```

2. **Create & activate a virtual environment**:
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

3. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Download the dataset**:
   The OGB loader will automatically fetch the `ogbn-proteins` dataset.

## Usage

### 1. Generate Edge Weights:
```bash
python prob_generator.py \
  --dataset ogbn-proteins \
  --output data/edges.txt \
  --max-edges 4000
```

### 2. Run ICM Simulation:
```bash
python run_icm.py \
  --edges data/edges.txt \
  --init-rate 0.01 \
  --iters 50
```

### 3. Evaluate Blocking Strategies:
```bash
python evaluate_blocking.py \
  --edges data/edges.txt \
  --methods random,betweenness,entropy,PageRank,ieed,hybrid \
  --k 0.01
```

## Methodology

1. **Load Data**: Fetch the `ogbn-proteins` dataset and extract `edge_index` and `edge_feat` as edge weights.
2. **Graph Construction**: Build the graph using `networkx`, adding weights and distances.
3. **ICM Simulation**: Seed 1% of nodes and simulate the infection process over 50 iterations.
4. **Blocking Methods**: Apply blocking strategies such as random removal, centrality-based blocking, and entropy-based blocking.
5. **Evaluation**: Compare the infection percentages before and after edge/node removal.

## Results

- **Baseline Infection Rate**: ~29.9%
- **Random Removal**: ~25.7%
- **Betweenness Centrality**: ~25.6%
- **Highest Weight Blocking (HWGT)**: ~27.7%
- **Hybrid Blocking (IEED + Community Detection)**: **~1.4%**

The hybrid techniques consistently demonstrated the greatest reduction in infection spread.

## Project Structure
```
├── data/                   # Raw & generated edge files
├── scripts/                # Scripts to convert, simulate, evaluate
│   ├── prob_generator.py
│   ├── run_icm.py
│   └── evaluate_blocking.py
├── code/                   # Core modules (data.py, influence.py, block_edges.py, communities.py)
├── notebooks/              # Jupyter notebooks for interactive simulation
├── requirements.txt
└── README.md
```

## Contributing

1. Fork the repo
2. Create a branch (`git checkout -b feature/YourFeature`)
3. Commit changes (`git commit -m "feat: add new blocking method"`)
4. Push (`git push origin feature/YourFeature`)
5. Open a Pull Request

Please follow the existing code style and include tests for new methods.

## License
This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

```

This README includes a clean and structured overview, setup instructions, usage guidelines, methodology, and results, along with the project structure and contribution instructions. Feel free to modify the sections as needed.
