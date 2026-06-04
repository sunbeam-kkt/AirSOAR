# PACE: Privileged Assistance for Counterfactual Execution in Assistant-Free UAV Vision-Language Navigation

<p align="center">
  <a href="YOUR_PAPER_LINK"><img src="https://img.shields.io/badge/Paper-arXiv-red"></a>
  <a href="YOUR_PROJECT_PAGE_LINK"><img src="https://img.shields.io/badge/Project-Page-blue"></a>
  <a href="YOUR_DATASET_LINK"><img src="https://img.shields.io/badge/Dataset-Download-green"></a>
  <a href="YOUR_LICENSE_LINK"><img src="https://img.shields.io/badge/License-MIT-yellow"></a>
</p>

<p align="center">
  <b>Assistant-free UAV vision-language navigation with internalized privileged assistance, counterfactual route validation, and physically executable planning.</b>
</p>

---

## 📌 Overview

This repository provides the official implementation of **PACE**, a privileged-assistance-driven framework for **assistant-free UAV vision-language navigation**.

Existing UAV-VLN agents often rely on external assistance during navigation, such as corrective guidance, route hints, or intervention signals. However, such assistance is usually unavailable during real deployment. PACE addresses this gap by converting privileged runtime support into an internal decision capability that can be used without external help at test time.

PACE contains three key components:

1. **Privileged Assistance Internalization**
   Distills training-only privileged signals into an internal correction state, enabling the agent to recover from route deviation without external assistance.

2. **Counterfactual Route Validation**
   Separates intended routes from plausible but incorrect alternatives, improving long-horizon route discrimination and reducing wrong-target navigation.

3. **Affordance-aware Executable Planning**
   Grounds validated navigation decisions into physically feasible and information-seeking UAV motion.

---

## 🖼️ Framework

![PACE](https://github.com/sunbeam-kkt/PACE/blob/master/Figure2.png)

PACE first learns from privileged teacher signals during training. At deployment, the UAV agent no longer receives external assistance. Instead, it uses the learned internal assistance state to support self-correction, counterfactual reasoning, and executable trajectory planning.

---

## 🔥 News

* `[2026-7-20]` Our paper was submitted to AAAI-2027!
---

## 📂 Repository Structure

```text
PACE/                      
├── Model/LLaMA-UAV                        # Pre-trained large language model
│   ├── scripts
│   └── tools
├── data/                                  # Dataset preparation scripts
│   ├── meta
│   ├── uav_dataset
│   └── sample_dataset.py
├── airsim_plugin/                         # PACE uses a simulation environment setup
│   ├── AirVLNSimulatorClientTool.py
│   └──AirVLNSimulatorServerTool.py
├── scripts/                               # Method Validation
│   ├── dagger_NYC.sh
│   ├── dagger_fast.sh
│   ├── eval.sh
│   ├── eval_fast.sh
│   ├── eval_param_flopts.sh
│   └── metric.sh
├── src/                                  
│   ├── common
│   ├── model_wrapper
│   └── vlnce_src
├── tools/                                 # Utility functions
├── utils/                         
├── requirements.txt
└── README.md
```

---

## 🧩 Method

### 1. Privileged Assistance Internalization

During training, the agent has access to privileged assistance signals, such as correction hints, recovery labels, or teacher trajectories. PACE uses these signals only as supervision and distills them into an internal assistance state.

At test time, the agent does not receive any external help. The learned internal state supports recovery-critical decision making.

### 2. Counterfactual Route Validation

UAV navigation in city-scale environments often contains visually similar landmarks and ambiguous route choices. PACE introduces counterfactual validation to compare the intended route with plausible alternatives.

This module encourages the agent to answer not only “where should I go?” but also “why should I not choose another similar route?”

### 3. Affordance-aware Executable Planning

After route validation, PACE grounds the decision into UAV-executable motion. The planner considers local feasibility, collision risk, visibility, and information gain to generate stable short-horizon trajectories.

---

## 📊 Main Results

### Comparison with Existing Methods


## 📊 Main Results

We compare our method with human performance, rule-based baselines, and recent UAV vision-language navigation methods. The results are reported on **Full**, **Easy**, and **Hard** splits.

<table>
  <thead>
    <tr>
      <th rowspan="2">Method</th>
      <th rowspan="2">Publish</th>
      <th rowspan="2">Assistant</th>
      <th colspan="4">Full</th>
      <th colspan="4">Easy</th>
      <th colspan="4">Hard</th>
    </tr>
    <tr>
      <th>NE↓</th>
      <th>SR↑</th>
      <th>OSR↑</th>
      <th>SPL↑</th>
      <th>NE↓</th>
      <th>SR↑</th>
      <th>OSR↑</th>
      <th>SPL↑</th>
      <th>NE↓</th>
      <th>SR↑</th>
      <th>OSR↑</th>
      <th>SPL↑</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Human</td>
      <td>-</td>
      <td>✓</td>
      <td>14.15</td>
      <td>94.51</td>
      <td>94.51</td>
      <td>77.84</td>
      <td>11.68</td>
      <td>95.44</td>
      <td>95.44</td>
      <td>76.19</td>
      <td>17.16</td>
      <td>93.37</td>
      <td>93.37</td>
      <td>79.85</td>
    </tr>
    <tr>
      <td>Random</td>
      <td>-</td>
      <td>✓</td>
      <td>222.20</td>
      <td>0.14</td>
      <td>0.21</td>
      <td>0.07</td>
      <td>142.07</td>
      <td>0.26</td>
      <td>0.39</td>
      <td>0.13</td>
      <td>320.12</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <td>Fixed</td>
      <td>-</td>
      <td>✓</td>
      <td>188.61</td>
      <td>2.27</td>
      <td>8.16</td>
      <td>1.40</td>
      <td>121.36</td>
      <td>3.48</td>
      <td>11.48</td>
      <td>2.14</td>
      <td>270.69</td>
      <td>0.79</td>
      <td>4.09</td>
      <td>0.49</td>
    </tr>
    <tr>
      <td>CMA</td>
      <td>-</td>
      <td>✓</td>
      <td>135.73</td>
      <td>8.37</td>
      <td>18.72</td>
      <td>7.90</td>
      <td>84.89</td>
      <td>11.48</td>
      <td>24.52</td>
      <td>10.68</td>
      <td>197.77</td>
      <td>4.57</td>
      <td>11.65</td>
      <td>4.51</td>
    </tr>
    <tr>
      <td>TravelUAV</td>
      <td>ICLR'25</td>
      <td>✓</td>
      <td>98.66</td>
      <td>17.45</td>
      <td>48.87</td>
      <td>15.76</td>
      <td>66.40</td>
      <td>20.26</td>
      <td>51.23</td>
      <td>18.10</td>
      <td>138.04</td>
      <td>14.02</td>
      <td>45.98</td>
      <td>12.90</td>
    </tr>
    <tr>
      <td>OpenVLN</td>
      <td>arXiv'25</td>
      <td>✓</td>
      <td>125.97</td>
      <td>14.39</td>
      <td>28.03</td>
      <td>12.94</td>
      <td>87.96</td>
      <td>15.22</td>
      <td>30.64</td>
      <td>13.31</td>
      <td>175.54</td>
      <td>13.32</td>
      <td>24.62</td>
      <td>12.55</td>
    </tr>
    <tr>
      <td>NavFoM</td>
      <td>ICLR'26</td>
      <td>✓</td>
      <td>93.05</td>
      <td>29.17</td>
      <td>49.24</td>
      <td>25.03</td>
      <td>58.98</td>
      <td>32.91</td>
      <td>53.16</td>
      <td>27.87</td>
      <td>143.83</td>
      <td>23.58</td>
      <td>43.40</td>
      <td>20.80</td>
    </tr>
    <tr>
      <td>NeuroKalman</td>
      <td>ICML'26</td>
      <td>✓</td>
      <td>71.56</td>
      <td>25.86</td>
      <td>58.73</td>
      <td>22.43</td>
      <td>42.70</td>
      <td>30.52</td>
      <td>62.70</td>
      <td>25.86</td>
      <td>105.07</td>
      <td>20.11</td>
      <td>53.90</td>
      <td>18.21</td>
    </tr>
    <tr>
      <td><b>Ours-Assistant</b></td>
      <td>-</td>
      <td>✓</td>
      <td><b>62.58</b></td>
      <td><b>40.82</b></td>
      <td><b>68.05</b></td>
      <td><b>34.76</b></td>
      <td><b>31.44</b></td>
      <td><b>44.27</b></td>
      <td><b>73.40</b></td>
      <td><b>40.39</b></td>
      <td><b>94.51</b></td>
      <td><b>35.74</b></td>
      <td><b>58.70</b></td>
      <td><b>33.50</b></td>
    </tr>
    <tr>
      <td><b>Ours</b></td>
      <td>-</td>
      <td>✗</td>
      <td><b>66.91</b></td>
      <td><b>35.32</b></td>
      <td><b>64.83</b></td>
      <td><b>32.70</b></td>
      <td><b>35.22</b></td>
      <td><b>40.86</b></td>
      <td><b>64.88</b></td>
      <td><b>35.65</b></td>
      <td><b>103.55</b></td>
      <td><b>32.92</b></td>
      <td><b>56.43</b></td>
      <td><b>29.37</b></td>
    </tr>
  </tbody>
</table>

**Metrics.** `NE` denotes navigation error, where lower is better. `SR` denotes success rate, `OSR` denotes oracle success rate, and `SPL` denotes success weighted by path length, where higher is better.

**Note.** `Ours-Assistant` denotes the variant with external assistance, while `Ours` denotes the assistant-free deployment setting.


### Ablation Study

## 🧪 Ablation Study

We conduct ablation studies to analyze the contribution of each component in our framework.

| Method               |       NE↓ |       SR↑ |      OSR↑ |      SPL↑ |      RSR↑ |   HP-F1↑ |      CRA↑ |     CVR↓ |      TCR↓ |
| -------------------- | --------: | --------: | --------: | --------: | --------: | -------: | --------: | -------: | --------: |
| Direct Regression    |     81.58 |     27.63 |     50.18 |     24.20 |     47.84 |     0.46 |     70.10 |    14.20 |     54.72 |
| w/o Internalization  |     74.82 |     30.74 |     57.06 |     28.12 |     55.28 |     0.54 |     84.90 |     9.35 |     62.18 |
| w/o DAgger           |     68.35 |     33.71 |     61.27 |     30.48 |     64.36 |     0.78 |     85.40 |     9.48 |     66.04 |
| w/o Causal Grounding |     76.10 |     29.68 |     55.34 |     27.32 |     61.04 |     0.72 |     72.60 |     9.02 |     60.91 |
| w/o Affordance Field |     70.84 |     32.14 |     56.87 |     29.58 |     65.10 |     0.79 |     85.30 |    12.76 |     58.63 |
| **Ours**             | **66.91** | **35.32** | **64.83** | **32.70** | **67.93** | **0.82** | **87.60** | **8.10** | **69.80** |

**Metrics.** `NE` denotes navigation error. `SR` denotes success rate. `OSR` denotes oracle success rate. `SPL` denotes success weighted by path length. `RSR` denotes recovery success rate. `HP-F1` denotes help prediction F1 score. `CRA` denotes counterfactual route accuracy. `CVR` denotes collision violation rate. `TCR` denotes trajectory collision rate.


---

## 🗃️ Dataset

We evaluate PACE on assistant-free UAV vision-language navigation benchmarks.

Please organize the dataset as follows:

```text
DATA_ROOT/
├── train/
│   ├── images/
│   ├── instructions.json
│   ├── trajectories.json
│   └── privileged_signals.json
├── val/
│   ├── images/
│   ├── instructions.json
│   └── trajectories.json
└── test/
    ├── images/
    ├── instructions.json
    └── trajectories.json
```

Set the dataset path in the config file:

```yaml
dataset:
  root: /path/to/DATA_ROOT
  train_split: train
  val_split: val
  test_split: test
```

---

## ⚙️ Installation

### 1. Clone this repository

```bash
git clone https://github.com/YOUR_USERNAME/PACE.git
cd PACE
```

### 2. Create environment

```bash
conda create -n pace python=3.10 -y
conda activate pace
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

Optional dependencies for visualization:

```bash
pip install matplotlib opencv-python imageio
```

---

## 🚀 Training

Train PACE with the following command:

```bash
bash scripts/train.sh
```

Or run directly:

```bash
python train.py \
  --config configs/train_pace.yaml \
  --data_root /path/to/DATA_ROOT \
  --output_dir outputs/pace
```

Example training script:

```bash
CUDA_VISIBLE_DEVICES=0,1,2,3 python train.py \
  --config configs/train_pace.yaml \
  --batch_size 32 \
  --epochs 20 \
  --lr 5e-5 \
  --output_dir outputs/pace
```

---

## 🔍 Evaluation

Evaluate a trained checkpoint:

```bash
bash scripts/eval.sh
```

Or run directly:

```bash
python eval.py \
  --config configs/eval_pace.yaml \
  --checkpoint outputs/pace/checkpoints/best.pth \
  --data_root /path/to/DATA_ROOT \
  --split test
```

The evaluation script reports:

* `NE`: Navigation Error
* `SR`: Success Rate
* `SPL`: Success weighted by Path Length
* `RSR`: Recovery Success Rate
* `CRA`: Counterfactual Route Accuracy
* `CVR`: Collision Violation Rate

---

## 📈 Visualization

Visualize navigation trajectories, recovery behavior, and counterfactual route validation:

```bash
python visualize.py \
  --checkpoint outputs/pace/checkpoints/best.pth \
  --data_root /path/to/DATA_ROOT \
  --save_dir outputs/visualization
```

Expected outputs:

```text
outputs/visualization/
├── trajectory_vis/
├── counterfactual_routes/
├── recovery_cases/
└── failure_cases/
```

---

## 🧪 Pretrained Models

Pretrained checkpoints will be released at:

| Model      | Dataset       | Link        |
| ---------- | ------------- | ----------- |
| PACE-base  | UAV-Need-Help | Coming soon |
| PACE-large | UAV-Need-Help | Coming soon |

After downloading, place checkpoints under:

```text
checkpoints/
└── pace_best.pth
```

---

## 📌 Reproducibility

To reproduce the main results in the paper:

```bash
bash scripts/reproduce_main_results.sh
```

To reproduce the ablation study:

```bash
bash scripts/reproduce_ablation.sh
```

To reproduce visualization figures:

```bash
bash scripts/reproduce_figures.sh
```

---

## 📝 Citation

If you find this repository useful, please consider citing our paper:

```bibtex
@inproceedings{your2027pace,
  title={PACE: Privileged Assistance for Counterfactual Execution in Assistant-Free UAV Vision-Language Navigation},
  author={Author One and Author Two and Author Three},
  booktitle={Proceedings of the AAAI Conference on Artificial Intelligence},
  year={2027}
}
```

---

## 🙏 Acknowledgements

This project builds upon prior research in vision-language navigation, UAV navigation, privileged learning, counterfactual reasoning, and embodied decision making.

We thank the authors of related UAV-VLN benchmarks and open-source navigation frameworks for their valuable contributions to the community.

---

## 📄 License

This project is released under the `MIT License`. Please see `LICENSE` for more details.

---

## 📬 Contact

For questions, please contact:

```text
YOUR_NAME: your_email@example.com
```

or open an issue in this repository.
