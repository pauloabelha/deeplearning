
This is a mini tutorial to get you started in deep learning for computer vision with a complete developer environment. 

This tutorial is tailored for Ubuntu users. Ubuntu is nice. https://www.ubuntu.com/about

After following the steps below to set up your environment, please go to https://github.com/wxs/keras-mnist-tutorial for code explanation

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

Open PyCharm

Go to File/New Project and give your project a name, e.g., keras-mnist-tutorial

On the Create project window, select Existing interpreter and click to add a local environment. We are going to associate our recently created Anaconda enviornment interpreter to this project.

![Step 1](https://github.com/pauloabelha/deeplearning/blob/master/tutorials/keras-mnist-pycharm-tutorial/images/keras-mnist-tutorial-pycharm1.png?raw=true)

Add the Python interpreter from the Anaconda virtual environment we created. Your enviroment should be under ~/anaconda3/envs/
[![Step 2](https://github.com/pauloabelha/deeplearning/blob/master/tutorials/keras-mnist-pycharm-tutorial/images/keras-mnist-tutorial-pycharm2.png?raw=true)]

Check everything is okay and click create on the lower right corner.
[![Step 3](https://github.com/pauloabelha/deeplearning/blob/master/tutorials/keras-mnist-pycharm-tutorial/images/keras-mnist-tutorial-pycharm3.png?raw=true)]

Now go to File/New and create a new Python file named main
[![Step 4](https://github.com/pauloabelha/deeplearning/blob/master/tutorials/keras-mnist-pycharm-tutorial/images/keras-mnist-tutorial-pycharm4.png?raw=true)]

Paste the content from deeplearning/tutorials/keras-mnist-pycharm-tutorial/main.py on to your Python main file
[![Step 5](https://github.com/pauloabelha/deeplearning/blob/master/tutorials/keras-mnist-pycharm-tutorial/images/keras-mnist-tutorial-pycharm5.png?raw=true)]

Go to Run/Run... and select your main file to run
[![Step 6](https://github.com/pauloabelha/deeplearning/blob/master/tutorials/keras-mnist-pycharm-tutorial/images/keras-mnist-tutorial-pycharm6.png?raw=true)]

When your program finished, you should see the smething similar to these output plots:
[![Step 7](https://github.com/pauloabelha/deeplearning/blob/master/tutorials/keras-mnist-pycharm-tutorial/images/keras-mnist-tutorial-pycharm7.png?raw=true)]

And also your train and test accuracies on the console output:
Train score: 0.03838914178852768
Train accuracy: 0.9873
Test score: 0.07912812198924367
Test accuracy: 0.9782

Congratulations! You ran your first Deep Leaning program.
If you want to run your program again, you can just press Shift+F10.
