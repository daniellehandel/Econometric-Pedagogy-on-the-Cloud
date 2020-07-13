# Econometric-Pedagogy
 Econometric Pedagogy and Cloud Computing: Training the Next Generation of Economists and Data Scientists
 
 Authors: Danielle V. Handel, Anson T. Y. Ho, Kim P. Huynh, David T. Jacho-Chávez, Carson H. Rea

<br>

_________________________________________________________________________________________________________

<img align="right"
     src="https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/workflow_3.png" 
     width="600" height="460" />

## Table of Contents
1. [Overview](#overview)
2. [Prerequisites](#prerequisites)
3. [Launching an Instance via AWS](#lauching-an-instance-via-aws)
   1. [Customizing an Instance](#seven-steps)
   2. [Navigating Bitvise](#navigating-bitvise)
4. [Anaconda](#anaconda)
   1. [Loading Anaconda](#loading-anaconda)
   2. [JupyterHub](#jupyterhub)
5. [R](#r)
   1. [Adding R](#adding-r)
   2. [Update and Install R Kernel](#update-and-install-r-kernel)
6. [Stata](#stata)
   1. [Adding Stata](#adding-stata)
7. [Disclaimer](#disclaimer)

## Overview 

<br>

The following instructions document a step-by-step guide to setting up a virtual “Econometrics Lab” hosted in the cloud. Ultimately, students will be able to connect to the lab via a web browser with a username and password and have access to JupyterLab and Jupyter Notebooks with Python, R, and Stata kernels. A group video chat service provider such as MS teams or Google hangout can be used alongside for synchronous instruction.

The guide below corresponds to workflow 3 outlined in “Econometric Pedagogy and Cloud Computing: Training the Next Generation of Economists and Data Scientists,” though the instructions may be modified to suit different teaching styles and classroom needs.


## Prerequisites

<br>
 
This guide assumes the following:

* An up-to-date personal computer is available for use.
* A classroom was created in AWS Educate.
* Stata or the department’s IT services were contacted for the proper Stata licensing.  

[Back to Top](#econometric-pedagogy)
 

## Launching an Instance via AWS <a name="lauching-an-instance-via-aws"></a>

  <br>
  
  This section details a method of launching an instance on AWS Educate's EC2 server. Demonstrational gifs are provided alongside the instructions, which feature the interfaces being used for this purpose. 
  
  #### Customizing an Instance <a name="seven-steps"></a>

|<img src="https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/1_nav_to_console_.gif" width="800" height="370" />|
|---|

  Log into your AWS Educate account. The "My Classrooms" tab on the top banner in the interface directs to the complete list of classrooms supported on the account. From there, select the desired classroom by clicking the blue "Go to classroom" button. The third-party application, Vocareum, will launch, showing an overview of the classroom. To manage, select "AWS console." To launch the proper instance, select EC2 from the dropdown menu labeled "All services". 
  
  :bulb: Your browser may block pop-ups from Vocarem. 

  <br>
  
|<img src="https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/2_start_instance.gif" width="800" height="370" />|
|---|

  Select an Ubuntu server as the desired Amazon Machine Image (AMI). This demonstration utilizes Ubuntu 20.4, though other Ubuntu servers will also be suitable. 

  The next tab requests an instance type to be selected. The "general purpose" option will be preselected and is available with AWS's free tier. Click "Next: Configure Image" to continue.
 
  Immediately continue to "Next: Add Storage."

  <br>
  
|<img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/3_security_group.gif"  width="800" height="370" />|
|---|
  
  Change the storage from the default to the maximum the free tier provides, 30 GiB. Continue to “Next: Add Tags”.

Tags are an optional feature to allow for categorization and organization. Continue to "Next: Configure Security Groups".

The default SSH rule will have the standard Port Range of 22 and a “Custom” source. Change the source to “Anywhere” to allow students to access the instance. Add a second custom TCP security rule by clicking the “Add Rule” button. Modify the rule to have a port range of 8000. Add a description of “JupyterHub.” Continue to the final stage by clicking the blue “Review and Launch” button. 

Given that all steps have been followed by this point, select “Launch”.

  <br>
  
|<img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/5_launch_and_key.gif"  width="800" height="370" />|
|---|
  
  Selecting “Launch” will prompt the user to select an existing key pair or create a new one. A key pair serves as a password to connect the instance to a SSH server or client. Name and download your key pair. 

:warning: Do not lose the key or all progress will be lost. Keep track of where the key is stored, as it will need to be accessed later. :warning:

  <br>
  
#### Navigating Bitvise <a name="navigating-bitvise"></a>
  
|<img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/4_IP_into_bitvise.gif"  width="800" height="370" />|
|---|

Download [Bitvise SSH Client](https://www.bitvise.com/ssh-client-download) or any other appropriate SSH software. 

The instance should now be visible in the EC2 homepage. Located towards the bottom of the screen, the description of the instance should be visible. Open Bitvise as an SSH client. Copy the IPv4 Public IP address and paste it into “Host” on Bitvise. Insert 22 as the port. 

:bulb: MacOS users may choose to use the Terminus App in lieu of Bitvise.

  <br>
  
|<img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/6_put in key.gif"  width="800" height="370" />|
|---|
  
  The proper username to connect Bitvise to the instance is “ubuntu." Change the following line “Initial method” to publickey. Select the proper key in from the newly created “client key” line. Click "Log In" to selct the key downloaded earlier. An optional comment can be left for organization purposes if desired.

The instance is now launched and hosted on a client. 
Continue reading the “Anaconda” section to download the distribution onto the newly created instance. 

[Back to Top](#econometric-pedagogy)
  

## Anaconda
  
  #### Loading Anaconda <a name="loading-anaconda"></a>
  
  The following directions are for use in the Bitvise (or other choise SSH software) terminal console. Unless otherwise specified, type and run each line individually. 
  
  To request root access:
  ```console
  ubuntu@ip-xx-xxx:~$ sudo -i
  ```
  
  After launching an instance with your selected cloud service provider, update the Ubuntu repository and upgrade packages with:
  ```console
  ubuntu@ip-xx-xxx:~$ apt-get update
  ubuntu@ip-xx-xxx:~$ apt-get upgrade
  ```
  
  To install Anaconda:
  ```console
  ubuntu@ip-xx-xxx:~$ wget https://repo.anaconda.com/archive/Anaconda3-2020.02-Linux-x86_64.sh
  ubuntu@ip-xx-xxx:~$ bash Anaconda3-2020.02-Linux-x86_64.sh
  ```
  When prompted with `[/root/anaconda3] >>>` enter:
  
  ```console
  /usr/anaconda3
  ```
 
  In order for Anaconda to operate, the following command needs to be entered:
  ```console
  ubuntu@ip-xx-xxx:~$ source .bashrc
  ```
 
  Open the profile in nano with the following command.
  ```console
  ubuntu@ip-xx-xxx:~$ nano /etc/profile
  ```
  
  Enter `export PATH="/usr/anaconda3/bin:$PATH"` into the bottom of the document as shown below.
  
  |<img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/enter%20anaconda%20path.png" width = "400" height = "400" />|
  |---|
  
  Use <kbd>CTRL</kbd>+<kbd>O</kbd> then <kbd>enter</kbd> to overwrite the document and <kbd>CTRL</kbd>+<kbd>X</kbd> to exit.
  <br>
  
  #### JupyterHub: 
  
  Install [JupyterHub](https://jupyterhub.readthedocs.io/en/stable/quickstart.html).
 
  First, make sure conda is up to date by entering: 
  ```console
  ubuntu@ip-xx-xxx:~$ conda update -n root conda
  ```

  Update all packages in the current environment to the latest version :
  ```console
  ubuntu@ip-xx-xxx:~$ conda update --all
  ubuntu@ip-xx-xxx:~$ conda install -c conda-forge jupyterhub
  ```
  
  A configuration file needs to be created for JupyterHub:
  ```console
  ubuntu@ip-xx-xxx:~$ mkdir /etc/jupyterhub/
  ubuntu@ip-xx-xxx:~$ cd /etc/jupyterhub/
  ubuntu@ip-xx-xxx:~$ jupyterhub --generate-config
  ```
  
  Using nano, access the newly created configuration file:
  ```console
  ubuntu@ip-xx-xxx:~$ nano jupyterhub_config.py
  ```
  
  The configuration file will be modified to:
  * Allow JupyterHub to be accessed by typing "lab" into the command line.
  * Allow admin to access other users' accounts.
  * Specify system user as administrator.
  * Shutdown user servers on logout.
  * Prevent the user-owned configuration files from being loaded.
  
  ```console
  c.Spawner.default_url = '/lab'
  c.JupyterHub.admin_access = True
  c.Authenticator.admin_users = {'admin'}
  c.JupyterHub.shutdown_on_logout = True
  c.Spawner.disable_user_config = True
  ```
  
  In nano, create and open a file with the following command.
  ```console
  ubuntu@ip-xx-xxx:~$ nano /etc/jupyterhub/jupyterhub.service
  ```
  
  Copy and paste the following:
  ```console
  [Unit]
  Description=JupyterHub
  After=syslog.target network.target

  [Service]
  User=root
  Environment="PATH=/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/usr/anaconda3/bin"
  ExecStart=/usr/anaconda3/bin/jupyterhub --no-ssl -f /etc/jupyterhub/jupyterhub_config.py

  [Install]
  WantedBy=multi-user.target
  ```
  
  The following commands will enable the new file.
  ```console
  ubuntu@ip-xx-xxx:~$ ln -s /etc/jupyterhub/jupyterhub.service /etc/systemd/system/jupyterhub.service

  ubuntu@ip-xx-xxx:~$ systemctl daemon-reload
  ubuntu@ip-xx-xxx:~$ systemctl enable jupyterhub.service
  ubuntu@ip-xx-xxx:~$ systemctl start jupyterhub.service
  ```
  JupyterHub is now set up on the server.
  Check its status with the following command (optional).
  ```console
  ubuntu@ip-xx-xxx:~$ systemctl status jupyterhub.service
  ```
  
  [Back to Top](#econometric-pedagogy)
  

## R

  
  #### Adding R <a name="adding-r"></a>
  Install R:
  ```console
  ubuntu@ip-xx-xxx:~$ apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
  ubuntu@ip-xx-xxx:~$ add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/'
  ubuntu@ip-xx-xxx:~$ apt update
  ubuntu@ip-xx-xxx:~$ apt install r-base r-base-dev
  
  #Start R
  ubuntu@ip-xx-xxx:~$ R
  ```
  
  <br>
  
  #### Update and Install R Kernel <a name="update-and-install-r-kernel"></a>
  ```r
  
  # update, without prompts for permission/clarification
  update.packages(ask = FALSE)
  install.packages('IRkernel', lib = '/usr/local/lib/R/site-library')
  
  #Make Jupyter see the newly installed R kernel by installing a kernel spec.
  #For system-wide installation, set user to False in the installspec command:

  IRkernel::installspec(user = FALSE)

  # Additional Ubuntu linux packages are needed for 'tidyverse' in R
  apt install libcurl4-openssl-dev libssl-dev libxml2-dev

  # Install tidyverse for all users
  install.packages("tidyverse", dependencies = TRUE, INSTALL_opts = '--no-lock')

  # Examples of other packages
  install.packages("openxlsx", lib = '/usr/local/lib/R/site-library', dependencies = TRUE, INSTALL_opts = '--no-lock')
  install.packages("knitr", lib = '/usr/local/lib/R/site-library', dependencies = TRUE, INSTALL_opts = '--no-lock')
  
  #When ready, quit
  q()
  ```
  
  [Back to Top](#econometric-pedagogy)


## Stata

 
 :bulb: Instructors should contact Stata to discuss the best licencing options. A Stata Labs licences may be best for this workflow, with the lab size corresponding to the number of students in the lab.
  
  #### Adding Stata <a name="adding-stata"></a>
  Download [Stata](https://www.stata.com/support/faqs/unix/install-download-on-linux/) for Linux    
  Download [Stata kernel](https://kylebarron.dev/stata_kernel/) for Jupyter Notebook  
 
 Uploading Stata:
  ```console
  # create a folder for your Stata installation file
  ubuntu@ip-xx-xxx:~$ mkdir /home/ubuntu/stata_source
  ```
 Place your Stata for Linux installation file into this folder:
 
 ```console
 # Create directory where Stata should be installed
 cd /usr/local
 ubuntu@ip-xx-xxx:~$ mkdir stata16
 ubuntu@ip-xx-xxx:~$ cd stata16
 
 #install Stata- you will be prompted to enter license information
 ubuntu@ip-xx-xxx:~$ /home/ubuntu/stata_source/install
 
 #During installation, you will be prompted to run the following:
 ubuntu@ip-xx-xxx:~$ ./stinit
 
 #This is specific to Ubuntu
 ubuntu@ip-xx-xxx:~$ apt install libtinfo5
  ```
 
 To add a path to Stata:
 
 ```console
 # open your nano document
 ubuntu@ip-xx-xxx:~$ nano /etc/profile
 ```
 Type `export PATH="/usr/local/stata16:$PATH"` into the bottom of the document as depicted below.
 
 |<img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/enter%20stata%20path.png" width = "400" height = "400" />|
 |---|
 
 Use <kbd>CTRL</kbd>+<kbd>O</kbd> then <kbd>enter</kbd> to overwrite the document and <kbd>CTRL</kbd>+<kbd>X</kbd> to exit.
 
 #### Stata Kernel for Jupyter
 ```console
 python -m stata_kernel.install
 
 # Copy configuration file to system configuration for all users
 cp .stata_kernel.conf /etc/stata_kernel.conf 
```
  
  
  [Back to Top](#econometric-pedagogy)
  

## Disclaimer 

 
This instructional guide is part of a demonstration used for “Econometric Pedagogy and Cloud Computing: Training the Next Generation of Economists and Data Scientists”. There is no guarantee this methodology works for others. For specific needs or troubleshooting, independent research may be necessary. 

AWS Educate and corresponding services are trademark of Amazon Web Services.

Stata is trademark of Stata Corporation.

Python is developed on an open source license distributed by the [Python Software Foundation](https://www.python.org/psf/).

R is offered on an open source license distributed by the [R Foundation](https://www.r-project.org/foundation/).

JupyterHub is an open source platform developed and maintained by [Project Jupyter](https://jupyter.org/).


[Back to Top](#econometric-pedagogy)
  

