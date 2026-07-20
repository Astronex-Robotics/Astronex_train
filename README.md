# astronex_train

[![IsaacSim](https://img.shields.io/badge/IsaacSim-5.1.0-silver.svg)](https://docs.omniverse.nvidia.com/isaacsim/latest/overview.html)
[![Isaac Lab](https://img.shields.io/badge/IsaacLab-2.3.2-silver)](https://isaac-sim.github.io/IsaacLab)
[![RSL_RL](https://img.shields.io/badge/RSL_RL-3.3.0-silver)](https://github.com/leggedrobotics/rsl_rl)
[![Python](https://img.shields.io/badge/python-3.11-blue.svg)](https://docs.python.org/3/whatsnew/3.11.html)
[![Linux platform](https://img.shields.io/badge/platform-linux--64-orange.svg)](https://releases.ubuntu.com/22.04/)
[![Windows platform](https://img.shields.io/badge/platform-windows--64-orange.svg)](https://www.microsoft.com/en-us/)
[![License](https://img.shields.io/badge/license-BSD--3-yellow.svg)](https://opensource.org/licenses/BSD-3-Clause)
[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white)](https://pre-commit.com/)

## Overview

`astronex_train` is the training workspace for Astronex locomotion policies. It keeps Astronex task definitions, motion-retargeting tools, and RSL-RL training entry points outside the upstream Isaac Lab tree.

The repository is organized as a thin workspace with two Git submodules:

- `robolab`: Astronex Isaac Lab extension, environments, scripts, and robot assets.
- `rsl_rl`: Astronex-compatible RSL-RL dependency snapshot.

**Maintainer**: Astronex
**Support**: GitHub Issues

## Features

- Astronex training environments built on Isaac Lab.
- RSL-RL training, evaluation, and policy export entry points.
- AMP workflow for locomotion training.

## Requirements

- Python 3.11.
- Isaac Sim 5.1.0 and Isaac Lab 2.3.2.
- Ubuntu 22.04 x64 or Windows x64.

Install Isaac Lab by following the [official installation guide](https://isaac-sim.github.io/IsaacLab/main/source/setup/installation/index.html). Run the commands below in the Python environment used by Isaac Lab.

## Clone

Clone this repository outside the Isaac Lab source tree. Use `--recursive` so that `robolab` and `rsl_rl` are populated immediately:

```bash
git clone --recursive https://github.com/Astronex-Robotics/Astronex_train.git
cd astronex_train
```

If you already cloned the repository and `robolab` or `rsl_rl` is empty, initialize the submodules manually:

```bash
cd astronex_train
git submodule update --init --recursive
```

## Install

```bash
pip install -e ./robolab
pip install -e ./rsl_rl
```

Verify that the extension is installed by listing the available environments:

```bash
python robolab/scripts/tools/list_envs.py
```

## Usage

### Train

```bash
python robolab/scripts/rsl_rl/train.py --task=Astronex-AMP --headless --logger=tensorboard --num_envs=8192
```

### Play

```bash
python robolab/scripts/rsl_rl/play.py --task=Astronex-Play --num_envs=1
```

### Play AMP

```bash
python robolab/scripts/rsl_rl/play_astronex_amp.py --checkpoint /path/to/model.pt
```

To export an ONNX model, set `num_envs=1` and add `--exportonnx`:

```bash
python robolab/scripts/rsl_rl/play_astronex_amp.py --checkpoint /path/to/model.pt --exportonnx
```

## Troubleshooting

- Empty `robolab` or `rsl_rl` directory: run `git submodule update --init --recursive`.
- Missing Isaac Lab imports: activate the Python environment used by Isaac Lab before installing or running scripts.
- Missing Astronex task name: run `python robolab/scripts/tools/list_envs.py` and copy the exact task id.

## References and Thanks

This project builds on the following open-source projects:

- [IsaacLab](https://github.com/isaac-sim/IsaacLab)
- [rsl_rl](https://github.com/leggedrobotics/rsl_rl)
- [legged_gym](https://github.com/leggedrobotics/legged_gym)
- [legged_lab](https://github.com/zitongbai/legged_lab)
- [robot_lab](https://github.com/fan-ziqi/robot_lab)
- [InstinctLab](https://github.com/project-instinct/InstinctLab)
