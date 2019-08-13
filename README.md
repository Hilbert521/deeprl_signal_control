# Deep RL for traffic signal control

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This repo implements start-of-the-art mutli-agent (decentralized) deep RL algorithms for large-scale traffic signal control in SUMO-simulated environments.

Available cooperation levels:
* Centralized: a global agent that makes global control w/ global observation, reward.
* Decentralized: multiple local agents that make local control independently w/ neighborhood information sharing.

Available NN layers:
Fully-connected, LSTM.

Available algorithms:
IQL, IA2C, IA2C with stabilization (called MA2C).

Available environments:
* A 6-intersection benchmark traffic network. [Ye, Bao-Lin, et al. "A hierarchical model predictive control approach for signal splits optimization in large-scale urban road networks." IEEE Transactions on Intelligent Transportation Systems 17.8 (2016): 2182-2192.](https://ieeexplore.ieee.org/abstract/document/7406703/)
* A 5X5 traffic grid. [Chu, Tianshu, Shuhui Qu, and Jie Wang. "Large-scale traffic grid signal control with regional reinforcement learning." American Control Conference (ACC), 2016. IEEE, 2016.](https://ieeexplore.ieee.org/abstract/document/7525014/)
* A modified Monaco traffic network with 30 signalized intersections. [L. Codeca, J. Härri, "Monaco SUMO Traffic (MoST) Scenario: A 3D Mobility Scenario for Cooperative ITS" SUMO 2018, SUMO User Conference, Simulating Autonomous and Intermodal Transport Systems May 14-16, 2018, Berlin, Germany.](http://www.eurecom.fr/en/publication/5527/download/comsys-publi-5527.pdf) ([code](https://github.com/lcodeca/MoSTScenario))


## Requirements
* Python3
* [Tensorflow](http://www.tensorflow.org/install)
* [SUMO](http://sumo.dlr.de/wiki/Installing) 

Attention: the code on master branch is for SUMO version >= 1.1.0. Please go to branch [sumo-0.32.0](https://github.com/cts198859/deeprl_signal_control/tree/sumo-0.32.0) if you are using the old SUMO version.

## Usages
First define all hyperparameters in a config file under `[config_dir]`, and create the base directory of experiements `[base_dir]`. Before training, please call `build_file.py` under `[environment_dir]/data/` to generate SUMO network files for `small_grid` and `large_grid` environments.

To train a new agent, run
~~~
python3 main.py --base-dir [base_dir] train --config-dir [config_dir] --test-mode no_test
~~~
`no_test` is suggested, since tests will significantly slow down the training speed.

To access tensorboard during training, run
~~~
tensorboard --logdir=[base_dir]/log
~~~

To evaluate and compare trained agents, run
~~~
python3 main.py --base-dir [base_dir] evaluate --agents [agent names] --evaluate-seeds [seeds]
~~~
Evaluation data will be output to `[base_dir]/eva_data`, and make sure evaluation seeds are different from those used in training.

## Citation
If you find this useful in your research, please cite our paper "Multi-Agent Deep Reinforcement Learning for Large-Scale Traffic Signal Control" ([early access version](https://ieeexplore.ieee.org/document/8667868), [preprint version](https://arxiv.org/pdf/1903.04527.pdf)):
~~~
@article{chu2019multi,
  title={Multi-Agent Deep Reinforcement Learning for Large-Scale Traffic Signal Control},
  author={Chu, Tianshu and Wang, Jie and Codec{\`a}, Lara and Li, Zhaojian},
  journal={IEEE Transactions on Intelligent Transportation Systems},
  year={2019},
  publisher={IEEE}
}
~~~
