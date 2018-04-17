# Notes and Files for UC Berkeley CS 294 DRL Fall 2017
Some notes that record the issues and solutions for this class

Assuming we already setup Python 3.5 environment using Anaconda (I use Linux Ubuntu 16.04)
`conda create --prefix dir/name_env python=3.5 numpy scipy matplotlib theano keras ipython jupyter`

1 To properly install Mujoco
  1.1 Download executible, activate using license and setup path
  
  1.2 Install package mujoco-py in name_env site-packages
  
  1.1.1 Download Mujoco Pro mjpro131 linux from: https://www.roboti.us/index.html
  
  1.1.2 Apply for license from: https://www.roboti.us/license.html (student using it for personal project without fianncial support could use it for free). After receiving account number in email, use the account number in the same webpage to apply for key (mjkey.txt file). This might take 1-2 days to receive those emails.
  
  1.1.3 Assuming the downloaded mjpro131 is unzipped to /home/<username>/Downloads/mjpro131 folder, now we should copy/paste the mjkey.txt file to /home/<username>/Downloads/mjpro131/bin
  
  1.1.4 In terminal, `nano ~/.bashrc`, and add these text to the file 
    export LD_LIBRARY_PATH=/home/<username>/Downloads/mjpro131/bin
    export PATH="$LD_LIBRARY_PATH:$PATH"
    Then save it using Ctr+X
  
  1.1.5 Now we could use terminal cd into the folder /home/<username>/Downloads/mjpro131; to test it, issue the command
    `./simulate ../model/humanoid.xml` and the simulation should run properly.
  
  1.1.6 Issue:  
    File "/home/.../lib/python3.5/site-packages/mujoco_py/config.py", line 33, in init_config

   raise error.MujocoDependencyError('To use MuJoCo, you need to either populate ~/.mujoco/mjkey.txt and ~/.mujoco/mjpro131, or set the MUJOCO_PY_MJKEY_PATH and MUJOCO_PY_MJPRO_PATH environment variables appropriately. Follow the instructions on https://github.com/openai/mujoco-py for where to obtain these.') mujoco_py.error.MujocoDependencyError: To use MuJoCo, you need to either populate ~/.mujoco/mjkey.txt and ~/.mujoco/mjpro131, or set the MUJOCO_PY_MJKEY_PATH and MUJOCO_PY_MJPRO_PATH environment variables appropriately.
  
   Solution: open the config.py file:
   The default path is set to be `~/.mujoco/mjkey.txt` and `~/.mujoco/mjpro131`, which is not the same as the location of our mjpro131 folder. What I did is to change the locations where my mjpro131 folder and mjkey.txt are; comment out the default directories.
   default__key_path = os.path.expanduser('/home/username/Documents/DRL/mjpro131/bin/mjkey.txt')#('~/.mujoco/mjkey.txt')
   default_mjpro_path = os.path.expanduser('/home/username/Documents/DRL/mjpro131')#('~/.mujoco/mjpro131')
      
  
  1.2.1 Activate the environment we create earlier. `conda info --envs` then `source activate dir/name_env`
  
  1.2.2 Once the environment is activated, we could run `pip3 install mujoco==0.5.7` to install mujoco-py (note that since we use Mujoco 1.3.1, the compatible version for mujoco-py is 0.5.7 instead of 1.5.0, according to https://zhuoyangdu.github.io/2018/01/20/install-mujoco/)
  
2 Others would be just following the instruction pdf for the first hw.

3 Other Issues and Solutions

  3.1 Issue:
    File "/home/zhixunhe/Documents/DRL/hw1_env/lib/python3.5/site-packages/gym/envs/mujoco/mujoco_env.py", line 27, in __init__
    self.model = mujoco_py.load_model_from_path(fullpath)
AttributeError: module 'mujoco_py' has no attribute 'load_model_from_path'

  Solution: this solution works for me: https://github.com/openai/mujoco-py/issues/188
    Basically, we need to `pip3 uninstall gym` then to reinstall lower version of gym `pip3 install gym==0.7.3`
