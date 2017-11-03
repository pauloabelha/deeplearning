# deeplearning
Tutorial for setting up TensorFlow with GPU on your local computer

By Paulo Abelha

E-mail: pauloabelha@gmail.com

Thanks to Ahmed Hussein for all his tips and cheat sheet
Specially for the solution for the DNS problem!

DISCLAIMER:
TUTORIAL FOR SETTING UP TENSORFLOW ON LOCAL MACHINE (WITH GPU)
THIS TUTORIAL WILL MODIFY YOUR IMAGES AND CONTAINERS
IT IS INTENDED TO BE DONE FROM SCRATCH 
SO YOU END UP WITH YOUR OWN TENSORFLOW MODIFIED IMAGE

1) Installation
    - 1.1) Follow ALL installation steps in: https://www.tensorflow.org/install/install_linux#InstallingDocker
    - 1.2) Make sure you also follow the GPU support subsection

2) Getting images and creating containers
    - 2.1) List all images:
        - `sudo nvidia-docker images`
    - 2.2) You should see the image:
        `REPOSITORY                     TAG                 IMAGE ID            CREATED             SIZE`
	
	gcr.io/tensorflow/tensorflow   latest-gpu          8fa36e7840e4        11 days ago         2.78GB
    - 2.3) Enter the container:
        - `sudo nvidia-docker run -ti gcr.io/tensorflow/tensorflow:latest-gpu bash`
    - 2.4) Wait for the downloads to finish and you should be inside the container seeing something like:
        `root@11016584a711:/notebooks#` 
    - 2.5) Exit container (also done by pressing Ctrl+D):
    	`exit`
3) Modifying containers and creating your own image
    - 3.1) List your current containers:
        - `sudo nvidia-docker ps -a`
    - 3.2) You should see something like (container name: adoring_tesla)
CONTAINER ID        IMAGE                                     COMMAND             CREATED             STATUS                     PORTS               NAMES
5e1c9fed6f19        gcr.io/tensorflow/tensorflow:latest-gpu   "bash"              14 seconds ago      Exited (0) 7 seconds ago                       adoring_tesla
    - 3.3) The container name will be some random nice name - I got adoring_tesla :)
    - 3.4) Start your container by its name:
        - `sudo nvidia-docker start adoring_tesla`
    - 3.5) Connect to the container (and get a terminal with 'bash'):
        - `sudo nvidia-docker start adoring_tesla bash`

# 9 Once inside the container, modify it by installing something

	# 9.1 Update the packages to be able to install nano
	apt-get update

		# KNOWN ISSUE: your apt-get may not be able to connect 
		# IF that's the case, go through Ahmed's solution for DNS problems:

		-To resolve DNS

		SOLUTION:

		On the host (I'm using Ubuntu 16.04), find out the primary and secondary DNS server addresses:

		$ nmcli dev show | grep 'IP4.DNS'
		IP4.DNS[1]:              10.0.0.2
		IP4.DNS[2]:              10.0.0.3
		Using these addresses, create a file /etc/docker/daemon.json:

		$ sudo su root
		# cd /etc/docker
		# touch daemon.json
		Put this in /etc/docker/daemon.json:

		{                                                                          
			"dns": ["10.0.0.2", "10.0.0.3"]                                                                           
		}     
		Exit from root:

		# exit
		Now restart docker:

		$ sudo service docker restart
		VERIFICATION:

		Now check that adding the /etc/docker/daemon.json file allows you to resolve 'google.com' into an IP address:

		$ docker run busybox nslookup google.com
		Server:    10.0.0.2
		Address 1: 10.0.0.2
		Name:      google.com
		Address 1: 2a00:1450:4009:811::200e lhr26s02-in-x200e.1e100.net
		Address 2: 216.58.198.174 lhr25s10-in-f14.1e100.net


	# 9.2 Install nano
	apt-get install nano

	# 9.3 Create a file with and save:
	echo "Hello world" >> hello_world.txt

	# 9.4 Check that nano works and see the file:
	nano hello_world.txt

	# 9.5 To get out of nano, just Ctrl+X

	# 9.6 Exit the modified container:
	exit

# 10 Commit your modified container to a new image:
sudo nvidia-docker commit adoring_tesla my_tensorflow

# 11 Check that your new image was created:
sudo nvidia-docker images

# 12 Your image should be listed

REPOSITORY                     TAG                 IMAGE ID            CREATED             SIZE
my_tensorflow                  latest              6b84c5264acc        21 seconds ago      2.82GB
gcr.io/tensorflow/tensorflow   latest-gpu          8fa36e7840e4        12 days ago         2.78GB

# 13 Stop your container
sudo nvidia-docker stop adoring_tesla

# 14 Delete the container (keeping things clean)
sudo nvidia-docker rm adoring_tesla

# 15 Start a new container from your new image:
sudo nvidia-docker run -it my_tensorflow bash

	# 15.1 Run command to see all files (sorted by time):
	ll -rt

	# 15.2 Your hello_world.txt file should be listed
	total 420
	-rw-r--r--  1 root root    586 Apr 14 19:01 LICENSE
	-rw-r--r--  1 root root    333 Apr 14 19:01 BUILD
	-rw-r--r--  1 root root 209796 Apr 14 19:01 3_mnist_from_scratch.ipynb
	-rw-r--r--  1 root root 164559 Apr 14 19:01 2_getting_started.ipynb
	-rw-r--r--  1 root root  25231 Apr 14 19:01 1_hello_tensorflow.ipynb
	-rw-r--r--  1 root root     12 Apr 26 19:04 hello_world.txt
	drwxr-xr-x  2 root root   4096 Apr 26 19:05 ./
	drwxr-xr-x 69 root root   4096 Apr 26 19:10 ../

	# 15.3 Check that nano is installed:
	nano hello_world.txt

	# 15.4 Remember, to get out of nano, just Ctrl+X
	
	# 15.5 Get out of your container:
	exit

# COMMITING YOUR IMAGE TO DOCKERHUB

# 16 Create a DockerHub account
https://hub.docker.com/

# 17 On DockerHub, create a repository and name it:
my_tensorflow

# 18 On DockerHub, add yourself as collaborator

# 19 Back to your terminal, log in to docker with DockerHub credentials
sudo nvidia-docker login

# 19 Rename the image to have your DockerHub username and add a tag 
sudo nvidia-docker tag my_tensorflow pauloabelha/my_tensorflow:1

# 20 Push your image to the repository
sudo nvidia-docker push docker.io/pauloabelha/my_tensorflow:1

# 21 Go to DockerHub and check that your image is there

# PULLING YOUR IMAGE FROM DOCKERHUB

# 22 Clean ALL previous containers and images:
sudo nvidia-docker rm -f $(sudo nvidia-docker ps -aq)
sudo nvidia-docker rmi -f $(sudo nvidia-docker images -aq)

# 23 Pull your image
sudo nvidia-docker pull docker.io/pauloabelha/my_tensorflow:1

WELL DONE! END OF TUTORIAL
