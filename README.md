# OD-CLF-CBF

This repository contains Jupyter notebooks and supporting files to implement the proposed methods and generate all figures from the paper:

>M.A. Shahraki and L. Lessard.
"Spacecraft attitude control under reaction wheel constraints using control Lyapunov and control barrier functions", American Control Conference, 2025 ([arXiv](https://arxiv.org/abs/2409.19936)) 

**Abstract:** This paper introduces a novel control strategy for agile spacecraft attitude control, addressing reaction wheel-related input and state constraints. An optimal-decay control Lyapunov function quadratic program stabilizes the system and mitigates chattering at low sampling frequencies, while control barrier functions enforce hard state constraints. Numerical simulations validate the method's practicality and efficiency for real-time agile spacecraft attitude control.


## Project Overview

This project develops a chatter-free, computationally efficient controller for agile spacecraft attitude stabilization under reaction wheel (RW) torque and angular momentum constraints. Key contributions include:
1. A CLF-CBF-QP controller encoding RW input and state constraints as hard constraints, offering an efficient alternative to Model Predictive Control (MPC).
2. A dynamic decay weight $\rho$ for the CLF to mitigate input chattering at low sampling frequencies (10 Hz).
3. A Pareto plot visualizing performance trade-offs between control effort and maneuver time, comparing the proposed OD-CLF-CBF-QP to a baseline family of optimal policies.

The code uses `Python` and `matplotlib` with `ipympl` for interactive visualizations.

## Installation Instructions

These instructions are for the [VS Code](https://code.visualstudio.com/) editor.

1. Clone the repository:
   ```
   git clone https://github.com/QCGroup/odclfcbf.git
   cd odclfcbf
   ```

2. Set up the Conda environment:
   - Install [Miniconda](https://docs.conda.io/en/latest/miniconda.html) or [Anaconda](https://www.anaconda.com/).
   - Create the environment:
     ```
     conda env create -f odclfcbf/spacecraft_env/spacecraft_env.yml
     ```
   - Activate the environment:
     ```
     conda activate spacecraft_env
     ```

3. Register the Jupyter kernel:
   ```
   python -m ipykernel install --user --name spacecraft_env --display-name "spacecraft_env"
   ```

4. Install VS Code and extensions:
   - Download [VS Code](https://code.visualstudio.com/).
   - Install the Jupyter extension:
     - Open VS Code, go to Extensions (Ctrl+Shift+X or Cmd+Shift+X on macOS).
     - Search for `@id:ms-toolsai.jupyter` and install.
   - Optional: Install the Python extension: `@id:ms-python.python`.

5. Verify setup:
   ```
   python -c "import matplotlib.pyplot, numpy, cvxpy, scipy.integrate, control, control.optimal, clarabel, proxsuite, ipympl; print('All good!')"
   ```

## Reproducing Paper Results

To reproduce the figures and results from the paper:
1. Open the project in VS Code:
   ```
   cd odclfcbf
   code .
   ```
2. Run the main notebook:
   - Open `odclfcbf/main_code.ipynb` in VS Code.
   - Select the `spacecraft_env` kernel (top-right kernel selector).
   - Simulation parameters (e.g., inertia matrix, RW limits, initial Euler angles [140°, 20°, 100°]) are set as in Table I of the paper.
   - Click "Run All" to generate all simulations and plots.
   - All figures will be saved as PDFs in the `odclfcbf/figs/` directory (e.g., `figs/pareto_front.pdf`).

Generated Paper Figures:
   - **Figure 1 (Pareto Curve):**
   Plots control effort vs. maneuver time (T_final) for OD-CLF-CBF-QP with varying nu and alpha, compared to the optimal control problem (OCP). Saved as `odclfcbf/figs/pareto_front.pdf`.
   - **Figure 2 (State/Input Trajectories):**
   Shows attitude MRPs, angular velocity, RW angular momentum, and control torque for five controllers. Saved as `odclfcbf/figs/trajectories_3.pdf`.
   - **Figure 3 (Decay Weights and Slack Variables):**
   Plots rho and delta for OD-CLF-QP and OD-CLF-CBF-QP. Saved as `odclfcbf/figs/rho_delta.pdf`.
   - **Figure 4 (Monte Carlo Simulations):**
   Shows state/input responses for OD-CLF-CBF-QP with 20 random initial orientations ($\alpha=1$). Saved as `odclfcbf/figs/monte_carlo_3.pdf`.


## Question/Comments

For questions regarding this work, please contact the authors:
- Milad Alipour Shahraki: alipourshahraki.m@northeastern.edu
- Laurent Lessard: l.lessard@northeastern.edu

To cite this work (bibtex):
```
@misc{odclfcbf,
    title={Spacecraft Attitude Control Under Reaction Wheel Constraints Using Control Lyapunov and Control Barrier Functions}, 
    author={Milad Alipour Shahraki and Laurent Lessard},
    year={2024},
    eprint={2409.19936},
    archivePrefix={arXiv},
    primaryClass={eess.SY},
    url={https://arxiv.org/abs/2409.19936}, 
}
```