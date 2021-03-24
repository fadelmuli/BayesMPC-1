# Artifact Appendix for (Paper ID: 10) Uncertainty-Aware Robust Adaptive Video Streaming with Bayesian Neural Network and Model Predictive Control

## Abstract
This document illustrates how to obtain the results shown in the paper "Uncertainty-Aware Robust Adaptive Video Streaming with Bayesian Neural Network and Model Predictive Control" which is also enclosed in the attachments. Following the instructions detailed below, the results in Figures 2, 3, 4, 5, 6 can be replicated. _Note that the badge we want to apply is the Results Replicated badge._

## The comparison algorithms
There are 5 baseline algorithms for comparison, which were detailed in Section 3.1.3 in the paper. 

These baseline algorithms correspond to 5 execution files in the "source codes'':
1. Rate-based: `rb.py`
2. Buffer-based: `bb.py`
3. BOLA: `Bola_v1.py`
4. RobustMPC: `mpc_v2.py`
5. Pensieve: `rl_no_training.py`
6. Our proposed algorithm-_BayesMPC_: `bbp_mpc_v3.py`

## The environment setup
To run the codes, some softwares and packages should be installed for replicating the results successfully. In addition, it is suggested to run the codes with Ubuntu 16.04/18.04.

### Intall anaconda to manage the test environments.
- Download the anaconda installers from the [official website](https://www.anaconda.com/products/individual#Downloads), generally choose the 64-Bit (x86) Installer.
- Open Terminal, install anaconda

    ```
    cd Downloads
    bash Anaconda3-2020.11-Linux-x86_64.sh
    ```
- Type `yes` when there are questions in the installation procedure.
- Update `.bashrc`

    ```
    source ~/.bashrc
    ```

- Type `python` in Terminal, the installation is successful if the Anaconda logo shows in the terminal.

### Intall prerequisities for _BayesMPC_
The _BayesMPC_ should be tested with python 3.6, pytorch 1.6.0, numpy, matplotlib, and pandas.
- Create a new virtual environment named _bayes_ for testing _BayesMPC_

    ```
    conda create --name bayes python=3.6
    ```
- Activate the virtual environment and intall the packages in it.

    ```
    conda activate bayes
    conda install -n bayes numpy pandas matplotlib
    ```
- Install PyTorch. Note that the command of PyTorch intallation depends on the actual compute platform of your own computer, and you can choose appropriate version following the [guide page](https://pytorch.org/get-started/locally/). For example, if you have intalled `CUDA 10.2`, you can intall PyTorch with the latest version by running this Command:

    ```
    conda install pytorch torchvision torchaudio cudatoolkit=10.2 -c pytorch
    ```

- You can deactivate the current virtual environment by running

    ```
    conda deactivate
    ```

### Intall prerequisities for Pensieve
The Pensieve should be tested with python 2.7, Tensorflow (version <= 1.11.0), TFLearn (version <= 0.3.2), numpy, matplotlib, and pandas.
- Create a new virtual environment named _pensieve_ for testing Pensieve

    ```
    conda create --name pensieve python=2.7
    ```
- Activate the virtual environment and intall the packages in it.

    ```
    conda activate pensieve
    conda install -n bayes numpy pandas matplotlib
    ```
- Install Tensorflow.

    ```
    conda install tensorflow==1.11.0
    ```
- Install TFLearn.

    ```
    pip install tflearn==0.3.2
    ```
- You can deactivate the current virtual environment by running

    ```
    conda deactivate
    ```

### Intall prerequisities for other baseline algorithms
The other baseline algorithms can be tested in _pensieve_.

## Evaluation
### Results of Fig.2
To replicate the results in Fig.2, you should follow the steps below:
1. create two results folders

    ```
    mkdir ./results_lin
    mkdir ./results_lin/cb_fcc ./results_lin/cb_HSDPA
    ```
2. Generate the results of _BayesMPC_ and RobustMPC in Fig.2(a) and (b).

    ```python
    conda activate bayes
    ## for fig.2(a)
    python bbp_mpc_v3.py -- cb --HSDPA
    python mpc_v2.py --cb --HSDPA
    ## for fig.2(b)
    python bbp_mpc_v3.py -- cb --FCC
    python mpc_v2.py --cb --FCC
    ```
3. Plot the results in Fig.2(a).

    ```python
    ## for fig.2(a)
    python plot_results_fig2.py --a
    ## for fig.2(b)
    python plot_results_fig2.py --b
    ```

![fig2a](./pic/random_traces_prediction_norway.pdf)

### Results of Figs. 3, 4, 5
The operations for replicating the results shown in Figures 3, 4, 5 in Section.3 of the paper are similar. You can obtain the results by following steps:
1. There are two QoE metrics $QoE_{lin}$/$QoE_{log}$ and two network throughput datasets HSDPA/FCC for comparison. Hence, there are four folders for storing the results of each algorithms, evaluated with different QoE metrics and datasets: `results\_lin/fcc', `results\_lin/HSDPA', `results\_log/fcc', `results\_log/HSDPA'
2. For figure 3(a) and figure 4(a), you can obtain the results of each algorithm by setting ``QOE\_METRIC $=$ results\_lin'' and ``DATASET$=$ HSDPA'' in the corresponding files. For instance, if you want to obtain the results of BayesMPC with QoE metrics $QoE_{lin}$ and datasets HSDPA, just set the above instructions in line 47 and 49, in file ``bbp\_mpc\_v3.py''. Then, the results can be generated by running it in Terminal: ``python bbp\_mpc\_v3.py''.
3. To obtain the results of other algorithms over different settings, just simply change the settings about the QOE\_METRIC and DATASET in each corresponding files. 
4. _Plot the results_: all results that had been gotten from the above mentioned operations can be plotted by running ``python plot\_results\_fig34.py''. You can choose different settings in lines $6-12$ to plot different figures. For example, you can plot the results of figure 3(b) and figure 4(c) just by setting ``RESULTS\_FOLDER = ./results\_lin/fcc/'' and then running ``python plot\_results\_fig34.py'' in the Terminal.

### Results of Fig.6
The procedure for plotting Figure 6 is similar to the procedure for Figure 3, 4, 5. The only difference is that the the setting about the dataset for each algorithms should be changed as ``DATASET$=$ oboe'' in corresponding files if you want to test the performance of algorithms in Oboe dataset.