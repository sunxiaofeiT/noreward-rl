## Curiosity-driven Exploration by Self-supervised Prediction / 好奇心驱动的探索自我监督预测

#### In ICML 2017 [[Project Website]](http://pathak22.github.io/noreward-rl/) [[Demo Video]](http://pathak22.github.io/noreward-rl/index.html#demoVideo)

#### 发表在2017年的机器学习大会上， [项目地址](http://pathak22.github.io/noreward-rl/)  [例子视频](http://pathak22.github.io/noreward-rl/index.html#demoVideo)

[Deepak Pathak](https://people.eecs.berkeley.edu/~pathak/), [Pulkit Agrawal](https://people.eecs.berkeley.edu/~pulkitag/), [Alexei A. Efros](https://people.eecs.berkeley.edu/~efros/), [Trevor Darrell](https://people.eecs.berkeley.edu/~trevor/)<br/>
University of California, Berkeley<br/>
加利福尼亚大学，伯克利

<img src="images/mario1.gif" width="300">    <img src="images/vizdoom.gif" width="351">

This is a tensorflow based implementation for our [ICML 2017 paper on curiosity-driven exploration for reinforcement learning](http://pathak22.github.io/noreward-rl/).   
这是一个实现我们发表在2017机器学习大会上的《由好奇心驱动的自我监督预测》文章的tensorflow。 
   
Idea is to train agent with intrinsic curiosity-based motivation (ICM) when external rewards from environment are sparse.  
思想是在外部环境奖励稀疏的情况下培养具有内在好奇心的动机。  
  
Surprisingly, you can use ICM even when there are no rewards available from the environment,   
令人激动的是，即使在环境中没有回报的情况下，也可以使用ICM，  
  
in which case, agent learns to explore only out of curiosity: 'RL without rewards'. If you find this work useful in your research, please cite:  
在这种没有回报奖励的情况下，agent学习只是出于好奇：“没有奖励的RL”。如果你觉得这项工作对你的研究有用，请注明：

    @inproceedings{pathakICMl17curiosity,
        Author = {Pathak, Deepak and Agrawal, Pulkit and
                  Efros, Alexei A. and Darrell, Trevor},
        Title = {Curiosity-driven Exploration by Self-supervised Prediction},
        Booktitle = {International Conference on Machine Learning ({ICML})},
        Year = {2017}
    }

### 1) Installation and Usage / 安装和使用
1.  This code is based on [TensorFlow](https://www.tensorflow.org/)。  
    这些代码是基于 [TensorFlow](https://www.tensorflow.org/)  
      
To install, run these commands:  
用这些命令安装：  
  ```Shell
  # you might not need many of these, e.g., fceux is only for mario
  sudo apt-get install -y python-numpy python-dev cmake zlib1g-dev libjpeg-dev xvfb \
  libav-tools xorg-dev python-opengl libboost-all-dev libsdl2-dev swig python3-dev \
  python3-venv make golang libjpeg-turbo8-dev gcc wget unzip git fceux virtualenv

  # install the code
  git clone -b master --single-branch https://github.com/pathak22/noreward-rl.git
  cd noreward-rl/
  virtualenv curiosity
  source $PWD/curiosity/bin/activate
  pip install numpy
  pip install -r src/requirements.txt
  python curiosity/src/go-vncdriver/build.py

  # download models
  bash models/download_models.sh

  # setup customized doom environment
  cd doomFiles/
  # then follow commands in doomFiles/README.md
  ```

2. Running demo / 运行demo
  ```Shell
  cd noreward-rl/src/
  python demo.py --ckpt ../models/doom/doom_ICM
  python demo.py --env-id SuperMarioBros-1-1-v0 --ckpt ../models/mario/mario_ICM
  ```

3. Training code / 训练
  ```Shell
  cd noreward-rl/src/
  # For Doom: doom or doomSparse or doomVerySparse
  python train.py --default --env-id doom

  # For Mario, change src/constants.py as follows:
  # PREDICTION_BETA = 0.2
  # ENTROPY_BETA = 0.0005
  python train.py --default --env-id mario --noReward

  xvfb-run -s "-screen 0 1400x900x24" bash  # only for remote desktops
  # useful xvfb link: http://stackoverflow.com/a/30336424
  python inference.py --default --env-id doom --record
  ```

### 2) Other helpful pointers / 其他相关的帮助信息
- [Paper](https://pathak22.github.io/noreward-rl/resources/icml17.pdf)
- [Project Website](http://pathak22.github.io/noreward-rl/)
- [Demo Video](http://pathak22.github.io/noreward-rl/index.html#demoVideo)
- [Reddit Discussion](https://redd.it/6bc8ul)
- [Media Articles (New Scientist, MIT Tech Review and others)](http://pathak22.github.io/noreward-rl/index.html#media)

### 3) Acknowledgement / 鸣谢
Vanilla A3C code is based on the open source implementation of [universe-starter-agent](https://github.com/openai/universe-starter-agent).
