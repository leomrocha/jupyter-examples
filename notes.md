Things to install:

python(2,3)-pyqt5
$ sudo [apt-get|aptitude] install pyqt5-dev python-pyqt5 python3-pyqt5 

All python, pip, ipython>=4.0, jupyter
after with jupyter installed install with pip we can install many packages that can help us later:


$ sudo pip install nbconvert nbformat  console qtconsole


jupyter qtconsole --style monokai

to have a parrticular kernel:

jupyter console --kernel=julia-0.4
##########################################################################################################
#Installing BASH kernel  (useful for some sysadmin and file manipulation things)
##########################################################################################################

The kernel is here:
https://github.com/takluyver/bash_kernel

pip install bash_kernel
python -m bash_kernel.install

To use it, run one of:
$jupyter notebook
From the NEW menu choose BASH and a new page will open with a bash kernel there.

# In the notebook interface, select Bash from the 'New' menu
jupyter qtconsole --kernel bash --style monokai
jupyter console --kernel bash

##########################################################################################################
#Installing an R kernel for using with jupyter
##########################################################################################################
https://irkernel.github.io/
https://github.com/IRkernel/IRkernel

Instructions here:
http://irkernel.github.io/installation/

: install R
sudo aptitude install r-base

Install ZeroMQ development libraries (needed for IRkernel)

sudo aptitude install libzmq3-dev

Start an R session and install the packages:

install.packages(c('rzmq','repr','IRkernel','IRdisplay'),
                 repos = c('http://irkernel.github.io/', getOption('repos')),
                 type = 'source')
                 
And now the kernel needs to be made available for jupyter:
From the same R console do:

IRkernel::installspec()

Now to launch jupyter with R kernel

in a web based environment

$jupyter notebook
go to the new opened web page and on NEW select R as kernel
A new window will open with R as kernel (you'll also see the R symbol up to the right)

To launch R in a qtconsole (or console):

jupyter qtconsole --kernel=ir --style monokai
jupyter console --kernel=ir



##########################################################################################################
#Installing Scala Kernels
##########################################################################################################

There are several kernels, so let's install those and check that everything is working correctly:


################################
#Installing Jupyter-Scala kernel 
################################
Link here:
https://github.com/alexarchambault/jupyter-scala

1 - update all ipython packages:
$ pip install --upgrade ipython[all]

2 - Download the sources for the corresponding scala version

Read from the in progress README file here:

And execute (for my scala version: 2.11):

$ curl -L -o jupyter-scala https://git.io/vzhRi && chmod +x jupyter-scala && ./jupyter-scala && rm -f jupyter-scala


##########################################################################################################
#Installing APACHE-TOREE (SPARK + Scala) kernel 
##########################################################################################################

This kernel is quite tricky to make it work correctly. I haven't managed to have a stable version.


(this is more tricky one as needs to compile and do things without much automation)


#Install dependencies:


#Install Scala
sudo apt-get install scala scala-doc

#Install sbt
http://www.scala-sbt.org/release/docs/Installing-sbt-on-Linux.html

echo "deb https://dl.bintray.com/sbt/debian /" | sudo tee -a /etc/apt/sources.list.d/sbt.list
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 642AC823
sudo apt-get update
sudo apt-get install sbt

#Install Spark
Install Hadoop
Install Spark
Install Spark library dependencies (cassandra, SparkSQL, MLLib ... etc etc etc

#If this is just failing so we will have to build it from source
pip install toree --pre  #is still under development so needs to be done this way)
jupyter toree install #this command did not work so had to do it the hard way:

$ .local/bin/jupyter-toree install --user #here also should pass the SPARK path and options like:

For a local install with the correct path to spark (in my case):
.local/bin/jupyter-toree install --spark_home=/home/leo/installers/spark-1.6.0-bin-hadoop2.6 --spark_opts='--master=local[*]' --user


    jupyter toree install
    jupyter toree install --spark_home=/spark/home/dir
    jupyter toree install --spark_opts='--master=local[4]'
    jupyter toree install --kernel_name=toree_special

Verify that the kernel.json file created is correct (there might be the need to modify some parameters in the configuration file as it is not yet really good in the dev version, but is not hard to modify it!!)

So if this is installed in a cluster, can be run as multi-user (see jupyter multi user plugins) and set to use the spark cluster, this way all the development is done via the web interface and all the processing is in the cluster


##

