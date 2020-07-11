# Econometric-Pedagogy
 Econometric Pedagogy and Cloud Computing: Training the Next Generation of Economists and Data Scientists
 
 Authors: Danielle V. Handel, Anson T. Y. Ho, Kim P. Huynh, David T. Jacho-Chávez, Carson H. Rea

<br>

_________________________________________________________________________________________________________

<br>

The following are instructions for setting up a lab as used in Workflow 3.



## Launching an instance via AWS
<details>
  <summary>Click to expand</summary>

  <img src="https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/1_nav_to_console_.gif" width="800" height="370" />

  Log into your AWS Educate account. The "My Classrooms" tab on the top banner in the interface directs to the complete list of classrooms supported on the account. From there,   select the desired classroom by clicking the blue "Go to classroom" button. The third party, Vocareum, will launch, allowing the management of the classroom. To launch an      instance, select "AWS console". TO launch the instance, select EC2 from the list of services AWS provides. 

  <img src="https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/2_start_instance.gif" width="800" height="370" />

  Instruction
  Launching an instance supported by EC2 is a seven step process. Follow the following instructions to ensure the instance has the maximum security and memory for the free teir   offered by AWS. 

  First, select an Ubunto server as the desired Amazon Machine Image (AMI). 20.4 was selected in this demonstration, although any can be selcted, given Ubunto is the AMI. 

  The next tab requests an instance type to be selected. The "general purpose" option will be preselected and be elgible for AWS's free tier. Click "Next: Configure Image" to   continue.
 
  Immediately continue to "Next: Add Storage".


  <img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/3_security_group.gif"  width="800" height="370" />

  <img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/5_launch_and_key.gif"  width="800" height="370" />

  <img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/4_IP_into_bitvise.gif"  width="800" height="370" />

  <img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/6_put in key.gif"  width="800" height="370" />
  master
  
</details>

## Ananconda
<details>
  <summary>Click to expand</summary>
  
  ###### Loading Anaconda
  
  The following directions are for use in the Bitvise (or other choise SSH software) terminal console. Unless otherwise specified, type and run each line individually. 
  
  To request root access:
  
  ```console
  ubuntu@ip-xx-xxx:~$ sudo -i
  ```
  After launching an instance with your selected cloud service provider, update the Ubuntu repository and upgrade packages by:
  
  ```console
  ubuntu@ip-xx-xxx:~$ apt-get update
  ubuntu@ip-xx-xxx:~$ apt-get upgrade
  ```
  To install Anaconda:
  ```console
  ubuntu@ip-xx-xxx:~$ wget https://repo.anaconda.com/archive/Anaconda3-2020.02-Linux-x86_64.sh
  ubuntu@ip-xx-xxx:~$ bash Anaconda3-2020.02-Linux-x86_64.sh
  ```
  When prompted with
  ```console
  [/root/anaconda3] >>>
  ```
  enter `/usr/anaconda3`.
 
  ```console
  ubuntu@ip-xx-xxx:~$ source .bashrc
 
  #Open a text editor (nano is used here):
  ubuntu@ip-xx-xxx:~$ nano /etc/profile
  
  #enter the following:
  export PATH="/usr/anaconda3/bin:$PATH"
  ```
  Jupyter Hub:
  
  ```console
  # Install jupyter hub 
  # https://jupyterhub.readthedocs.io/en/stable/quickstart.html

  # Update to the latest conda version
  ubuntu@ip-xx-xxx:~$ conda update -n root conda

  # Update all packages in the current environment to the latest version 
  ubuntu@ip-xx-xxx:~$ conda update --all
  ubuntu@ip-xx-xxx:~$ conda install -c conda-forge jupyterhub
  ```
  ```console
  # Create jupyter hub configuration file
  ubuntu@ip-xx-xxx:~$ mkdir /etc/jupyterhub/
  ubuntu@ip-xx-xxx:~$ cd /etc/jupyterhub/
  ubuntu@ip-xx-xxx:~$ jupyterhub --generate-config
  ubuntu@ip-xx-xxx:~$ nano jupyterhub_config.py
  
  # enter the following in the file:
  # open jupyter lab by default
  c.Spawner.default_url = '/lab'
  # allow admin to access other users' accounts 
  c.JupyterHub.admin_access = True
  # specify system user as administrator
  c.Authenticator.admin_users = {'admin'}
  # shutdown user servers on logout
  c.JupyterHub.shutdown_on_logout = True
  # prevent the user-owned configuration files from being loaded
  c.Spawner.disable_user_config = True
  
  ```
  ```console
  #
  ubuntu@ip-xx-xxx:~$ nano /etc/jupyterhub/jupyterhub.service
  
  #enter the following:
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
  Now, enable this:
  ```console
  ubuntu@ip-xx-xxx:~$ ln -s /etc/jupyterhub/jupyterhub.service /etc/systemd/system/jupyterhub.service

  ubuntu@ip-xx-xxx:~$ systemctl daemon-reload
  ubuntu@ip-xx-xxx:~$ systemctl enable jupyterhub.service
  ubuntu@ip-xx-xxx:~$ systemctl start jupyterhub.service
  ubuntu@ip-xx-xxx:~$ systemctl status jupyterhub.service
  ```
</details>

## R
<details>
  <summary>Click to expand</summary>
 
  ###### Adding R 
  Install R:
  ```console
  ubuntu@ip-xx-xxx:~$ apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
  ubuntu@ip-xx-xxx:~$ add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/'
  ubuntu@ip-xx-xxx:~$ apt update
  ubuntu@ip-xx-xxx:~$ apt install r-base r-base-dev
  
  #Start R
  ubuntu@ip-xx-xxx:~$ R
  ```
  
  Update and add install R kernel to be used in Jupyter:
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

</details>

## Stata
<details>
  <summary>Click to expand</summary>
  
  ###### Adding Stata
  Download Stata for Linux from https://www.stata.com/support/faqs/unix/install-download-on-linux/
  Download Stata kernel for Jupyter Notebook from https://kylebarron.dev/stata_kernel/
  
  
</details>

