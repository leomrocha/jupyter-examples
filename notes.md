# Jupyter Kernel Installation notes

A jupyter kernel is the piece of code that links the Jupyter API with the desired Language.

There are many kernels, the main and original one is the python kernel which usually comes provided in any linux installation.

A comprehensive list of kernels is listed in [github](https://github.com/ipython/ipython/wiki/IPython-kernels-for-other-languages)


_ *Note* _: these notes were taken during installation in a Ubuntu 15.10, steps or details might change from your local environment

## Make sure you have the dependencies

### Things to install:

- python(2,3)-pyqt5
    
    $ sudo [apt-get|aptitude] install pyqt5-dev python-pyqt5 python3-pyqt5 

- All python, pip, ipython>=4.0, jupyter

    after with jupyter installed install with pip we can install many packages that can help us later


    $ sudo pip install nbconvert nbformat  console qtconsole

    $ sudo pip install ipython[all]


##### check that jupyter is correctly installed

    jupyter qtconsole --style monokai


It could be that jupyter is not yet there, try with *ipython* instead

    jupyter qtconsole --style monokai

When a kernel is installed, to launch jupyter with a particular kernel is something like this:

    jupyter console --kernel=julia-0.4
    
# Installing Kernels    

## Installing BASH kernel

The kernel is in the [bash kernel project page](https://github.com/takluyver/bash_kernel)

Basically it should be uber-simple to install:

    pip install bash_kernel
    python -m bash_kernel.install

To use it, run one of:

    $jupyter notebook

And from the NEW menu choose BASH and a new page will open with a bash kernel there.

To launch a console with the BASH kernel use one of the following:

    jupyter qtconsole --kernel bash --style monokai
    jupyter console --kernel bash

Note that you can change styles for qtconsole, I like the monokai style

## Installing an R kernel

For complete details it's better to go to the [iR kernel project web page](https://irkernel.github.io/) or to the [github source](https://github.com/IRkernel/IRkernel)

The complete instructions are [here](http://irkernel.github.io/installation/)

But the basic steps are:

1. install R

    sudo aptitude install r-base

2. Install ZeroMQ development libraries (needed for IRkernel)

    sudo aptitude install libzmq3-dev

3. Start an R session and install the packages:

    install.packages(c('rzmq','repr','IRkernel','IRdisplay'),
                 repos = c('http://irkernel.github.io/', getOption('repos')),
                 type = 'source')
    
After the kernel has beein installed, it needs to be made available to jupyter, for this from the same R console do:

    IRkernel::installspec()

#### Verify it was installed:

    $ jupyter kernelspec list

should output the kernel and the path it was installed to. If the kernel is not listed there, then there was an installation error

#### Launching

Now you can launch jupyter with R kernel

Getting the notebook (a web based environment)

    $jupyter notebook

Then go to the new opened web page and on NEW select R as kernel
A new window will open with R as kernel (you'll also see the R symbol up to the right)

To launch R in a qtconsole (or console):

    jupyter qtconsole --kernel=ir --style monokai
    jupyter console --kernel=ir



## Installing Scala Kernels

There are several kernels, so let's install those and check that everything is working correctly:

First make sure you have scala installed


#### Install dependencies:

Check your dependencies, in my case aptitude takes care of everything.

You can use apt-get instead, it's just that I like aptitude

#### Install Scala
sudo apt-get install scala scala-doc

#### Install sbt

From [Sbt install documentation](http://www.scala-sbt.org/release/docs/Installing-sbt-on-Linux.html)

This should work:

    echo "deb https://dl.bintray.com/sbt/debian /" | sudo tee -a /etc/apt/sources.list.d/sbt.list
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 642AC823
    sudo apt-get update
    sudo apt-get install sbt

#### Install Spark

1. Install Hadoop
2. Install Spark (in my case I downloaded the pre-build spark binaries, it just works)
3. Install Spark library dependencies (cassandra, SparkSQL, MLLib ... etc etc etc


### Installing Jupyter-Scala kernel 


This is the kernel I've been using successfully and without any incidents. Take a note that scala kernels are usually slower to start than other kernels. But after the first 

This kernel allows for autocompletion and has been quite stable for my experiments.

The [project page](https://github.com/alexarchambault/jupyter-scala) contains a lot of information. But is recommended to check the newest (in progress) [readme file](https://github.com/alexarchambault/jupyter-scala/tree/e1e3db4b9f013a2d8b785001ae6a390897bd20fa#classpathadd) that actually contains the good information to install the kernel

##### Steps:

1 - Make sure to update all ipython packages:

    $ pip install --upgrade ipython[all]

Search for the one line bash in the README.md file (linked above), choose the one that corresponds to the correct scala version and execute it

for my setup, the scala version is 2.11:

    $ curl -L -o jupyter-scala https://git.io/vzhRi && chmod +x jupyter-scala && ./jupyter-scala && rm -f jupyter-scala


#### Verify it was installed:

    $ jupyter kernelspec list

should output the kernel and the path it was installed to. If the kernel is not listed there, then there was an installation error

#### Launching

Is the same as before, either launch

    $ jupyter notebook
    
and from the NEW menu button choose *Spark 2.11* (my case, yours might be *Scala 2.10*)

### Installing APACHE-TOREE (SPARK + Scala) kernel []


This kernel is quite tricky to make it work correctly. I haven't managed to have a stable version.

I leave this here in case it might be useful for somebody that wants to give it a try but I won't do more than that as I had many issues with the stability of the kernel (kernels taht die suddenly, autocompletion not working, etc)


_If this is just failing so we will have to build it from source_

This should be the *easy way*: 

install with pip, you need the --pre as it is a pre-alpha version pip will refuse to install it unless you actually order it to do it with the *--pre* at the end

    pip install toree --pre  #is still under development so needs to be done this way)
    jupyter toree install #this command did not work so had to do it the hard way:

    $ .local/bin/jupyter-toree install --user #here also should pass the SPARK path and options like:

For a local install with the correct path to spark (in my case):

.local/bin/jupyter-toree install --spark_home=/home/leo/installers/spark-1.6.0-bin-hadoop2.6 --spark_opts='--master=local[*]' --user

Some options can be:

    jupyter toree install
    jupyter toree install --spark_home=/spark/home/dir
    jupyter toree install --spark_opts='--master=local[4]'
    jupyter toree install --kernel_name=toree_special

Verify that the kernel.json file created is correct (there might be the need to modify some parameters in the configuration file as it is not yet really good in the dev version, but is not hard to modify it!!)

So if this is installed in a cluster, can be run as multi-user (see jupyter multi user plugins) and set to use the spark cluster, this way all the development is done via the web interface and all the processing is in the cluster


