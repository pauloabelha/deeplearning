
This is a mini tutorial to get you started in deep learning for computer vision with a complete developer environment. 
This tutorial is tailored for Ubuntu users. Ubuntu is nice. https://www.ubuntu.com/about

By following this README file you are going to get your computer up and running for deep learning!
We are going to have to install:
+ Anaconda for managing Python virtual environments
+ PyCharm for managing your deep learning project and coding

Install Anaconda: https://conda.io/docs/user-guide/install/linux.html

Install PyCharm: https://www.jetbrains.com/pycharm/download/#section=linux

Clone this repository: ``git clone https://github.com/pauloabelha/deeplearning``

Go to the repository directory: ``cd deeplearning``

After installing both, open a terminal and run: ``conda create --name keras_mnist_env python=3.6``

Now, activate your environment: ``source activate keras_mnist_env``

You should see something like: (keras_mnist_env) user@computer:~/$

Install required python packages for the MNIST tutorial:

``pip install tensorflow numpy matplotlib keras``

