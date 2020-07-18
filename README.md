
# Econometric Pedagogy and Cloud Computing: Training the Next Generation of Economists and Data Scientists <a name="econometric-pedagogy"></a>
 
[Danielle V. Handel](https://www.linkedin.com/in/danielle-handel-134b53173/), [Anson T. Y. Ho](http://www.atyho.info), [Kim P. Huynh](https://www.bankofcanada.ca/profile/kim-huynh/), [David T. Jacho-Chávez](https://www.davidjachochavez.org/), [Carson H. Rea](https://www.linkedin.com/in/carson-rea-979062198/)

<br>

_________________________________________________________________________________________________________

<img align="right"
     src="https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/workflow_3.png" 
     width="600" height="460" />

## Table of Contents
1. [Overview](#overview)
2. [Pre-requisites](#pre-requisites)
3. [AWS: Instance Launching](#lauching-instance)
   1. [Customizing an Instance](#seven-steps)
   2. [Creating an Elastic IP Adress](#elastic-ip)
   3. [Navigating Bitvise](#navigating-bitvise)
4. [Anaconda](#anaconda)
   1. [Anaconda Installation](#loading-anaconda)
   2. [JupyterHub Installation and Configuration](#jupyterhub)
5. [R](#r)
   1. [R Installation](#adding-r)
   2. [Update and Install R Kernel](#update-and-install-r-kernel)
6. [Stata](#stata)
   1. [Stata Installation](#adding-stata)
   2. [Stata Kernel for Jupyter](#stata-kernel)
7. [(Optional) GitHub Extensions and Packages](#packages)
8. [(Optional) GitHub Authentication](#github-authentication)
9. [Disclaimer](#disclaimer)

## Overview 

<br>

The following instructions document a step-by-step guide to setting up a virtual “Econometrics Lab” hosted in the cloud. Ultimately, students will be able to connect to an environment to preform live coding on [Jupyter notebooks](https://jupyter.org/) with [Python](https://www.python.org/psf/)), [R](https://www.r-project.org/foundation/), and [Stata](https://www.stata.com/) kernels.

Optionally, this guide concludes with a method of integrating GitHub as to expidite the process of adding users for instructors. This method is for those with an advanced uderstanding of the command line. 

The guide below corresponds to workflow 3 outlined in “Econometric Pedagogy and Cloud Computing: Training the Next Generation of Economists and Data Scientists,” though the instructions may be modified to suit different teaching styles and classroom needs.


## Pre-requisites

<br>
 
To begin launching an instance, the following pre-requisites are required:

1. Hardware: Personal computer with internet connection.
2. Software:
   1. SSH Client (BitVise recommended).
   2. Stata license (contact your department's IT service).
3. Cloud Service:
   1. A classroom in AWS Educate.
   2. GitHub account (optional).

[Back to Top](#econometric-pedagogy)
 

## AWS: Instance Launching <a name="lauching-instance"></a>

  <br>
  
  This section details a method of launching an instance on AWS Educate's EC2 server. Demonstrational gifs are provided alongside the instructions to aid in navigating the complex interfaces.
  
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
  
#### Creating an Elastic IP Address <a name="elastic-ip"></a>

  An instructor may choose to turn off the server periodically to avoid billing when little to no traffic is expected. An [elastic IP address](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/elastic-ip-addresses-eip.html) ensures the original SSH key will function.
  
  <details>
    <summary>:bulb: What is an SSH key?</summary>
    <br>
 
   An SSH key serves as the "password" which connects the server to the SSH client. This demonstration suggests the use of Bitvise, although other clients, such as the Terminus App for Mac users, can serve as substitutions. 
   
   :warning: It is important to keep the key private and safe on your local computer. Loosing the key will prevent the server from functioning. Sharing the key could leave the server vulnerable :warning:
   
  </details>

|<img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/allocate_elastic.gif"  width="800" height="370" />|
|---|

Navigate to the Elastic IP configuration on the Amazon EC2 Console. Opt to allocate an elastic IP address from Amazon's pool of IPv4 addresses. Then, choose to associate this new address and select your instance. You will now have a different IP address for your lab. 

:warning: Typing this new IP address appended with ":8000" into your browser will bring you to your lab. It may be useful to do this to check the functionality of your lab after each step. :warning:

  <br>
  
#### Navigating Bitvise <a name="navigating-bitvise"></a>
  
|<img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/4_IP_into_bitvise.gif"  width="800" height="370" />|
|---|

Download [Bitvise SSH Client](https://www.bitvise.com/ssh-client-download) (Windows) or [Terminus App](https://termius.com/). 

The instance should now be visible in the EC2 homepage. Located towards the bottom of the screen, the description of the instance should be visible. Open Bitvise as an SSH client. Copy the IPv4 Public IP address and paste it into “Host” on Bitvise. Insert 22 as the port. 

  <br>
  
|<img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/6_put in key.gif"  width="800" height="370" />|
|---|
  
  The proper username to connect Bitvise to the instance is “ubuntu." Change the following line “Initial method” to publickey. Select the proper key in from the newly created “client key” line. Click "Log In" to selct the key downloaded earlier. An optional comment can be left for organization purposes if desired.
  
  The following directions are for use in the Bitvise (or other choice SSH software) terminal console. Unless otherwise specified, type and run each line individually. 
  
  To request root access:
  ```console
  $ sudo -i
  ```
  
  After launching an instance with your selected cloud service provider, update the Ubuntu repository and upgrade packages with:
  ```console
  $ apt-get update
  $ apt-get upgrade
  ```
  
  To create a new administrator or student, respectively:
  ```console
  $ adduser admin
  $ adduser student
  ```
  
  :bulb: To avoid having to add users and admin individually, view the section [GitHub Authentication](#github-authentication) to determine whether it is right for your server.

The instance is now launched and hosted on a client. 
Continue reading the “Anaconda” section to download the distribution onto the newly created instance. 

[Back to Top](#econometric-pedagogy)


## Anaconda

  The following directions are for use in the Bitvise (or other choise SSH software) terminal console. Unless otherwise specified, type and run each line individually. 
  
  #### Anaconda Installation <a name="loading-anaconda"></a>
  
  To install Anaconda:
  ```console
  $ wget https://repo.anaconda.com/archive/Anaconda3-2020.02-Linux-x86_64.sh
  $ bash Anaconda3-2020.02-Linux-x86_64.sh
  ```
  When prompted with `[/root/anaconda3] >>>`, enter:
  
  ```console
  $ /usr/anaconda3
  ```
 
  In order for Anaconda to operate, refresh:
  ```console
  $ source .bashrc
  ```
 
  Open the profile in [nano](https://www.nano-editor.org/).
  ```console
  $ nano /etc/profile
  ```
  <details>
    <summary>:bulb: What is nano?</summary>
    <br>
 
   Nano is the default text editor for Ubuntu. This program will be used throughout the tutorial to edit the configuration files of the needed software, enabling full integration into the lab interface. 
   
   Although there are many shortcuts included in this text editor, the most important for use in this project are the commands <kbd>CTRL</kbd>+<kbd>O</kbd> then <kbd>enter</kbd> which will overwrite a document and <kbd>CTRL</kbd>+<kbd>X</kbd> which will exit the editor.
   
   If you are using MacOS or Linux, nano may already be installed on your machine. To check, type the following line of code in the command line:
   
   ```console
   nano --version
   ```
   
   If the output shows a version number, nano is already installed.
   
  </details>
  
  Enter the following into the bottom of the document as shown below.
  ```
  export PATH="/usr/anaconda3/bin:$PATH
  ```
  
  <p align="center">
    <img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/enter%20anaconda%20path.png" width = "350" height = "400" />
  </p>
  
  Use <kbd>CTRL</kbd>+<kbd>O</kbd> then <kbd>enter</kbd> to overwrite the document and <kbd>CTRL</kbd>+<kbd>X</kbd> to exit.
  <br>
  
  Anaconda is now installed. Anaconda is a popular python distribution which comes with many packages needed for data science along with the open-source package managemnet system, conda. 
  
  <details>
    <summary>:bulb: Why is conda important?</summary>
    <br>
 
  Conda will allows the downloading and managment of packages through use of the command `conda`. This command will appear throughout the guide and facilitate the remainder of the set-up. 
   
  </details>
  
  
  #### JupyterHub Installation and Configuration <a name="jupyterhub"></a>
  
  Install [JupyterHub](https://jupyterhub.readthedocs.io/en/stable/quickstart.html).
 
  First, make sure conda is up to date by entering: 
  ```console
  $ conda update -n root conda
  ```

  Update all packages in the current environment to the latest version:
  ```console
  $ conda update --all
  $ conda install -c conda-forge jupyterhub
  ```
  
  Create the JupyterHub configuration file:
  ```console
  $ mkdir /etc/jupyterhub/
  $ cd /etc/jupyterhub/
  $ jupyterhub --generate-config
  ```
  
  Using nano, access the newly created configuration file:
  ```console
  $ nano jupyterhub_config.py
  ```
  
  Copy and paste the following into the configuration file:
  
  ```console
  #Allow JupyterHub to be accessed by typing "lab" into the command line.
  c.Spawner.default_url = '/lab'
  
  #Allow admin to access other users' accounts
  c.JupyterHub.admin_access = True
  
  #Specify system user as administrator
  c.Authenticator.admin_users = {'admin'}
  
  #Shutdown user servers on logout
  c.JupyterHub.shutdown_on_logout = True
  
  #Prevent the user-owned configuration files from being loaded
  c.Spawner.disable_user_config = True
  ```
  Use <kbd>CTRL</kbd>+<kbd>O</kbd> then <kbd>enter</kbd> to overwrite the document and <kbd>CTRL</kbd>+<kbd>X</kbd> to exit.
  
  In nano, create and open a file to configure JupyterHub's functionality.
  ```console
  $ nano /etc/jupyterhub/jupyterhub.service
  ```
  
  Copy and paste the following into the document as depicted below:
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
  <p align="center">
   <img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/jupytergnu.PNG" width = "650" height = "400" />
 </p>
  
  Use <kbd>CTRL</kbd>+<kbd>O</kbd> then <kbd>enter</kbd> to overwrite the document and <kbd>CTRL</kbd>+<kbd>X</kbd> to exit.
  
  Enable the new file.
  ```console
  $ ln -s /etc/jupyterhub/jupyterhub.service /etc/systemd/system/jupyterhub.service

  $ systemctl daemon-reload
  $ systemctl enable jupyterhub.service
  $ systemctl start jupyterhub.service
  ```
  JupyterHub is now set up on the server.
  Check its status (optional).
  ```console
  $ systemctl status jupyterhub.service
  ```
  
  [Back to Top](#econometric-pedagogy)
  

## R
  
  The following directions are for use in the Bitvise (or other choise SSH software) terminal console. Unless otherwise specified, type and run each line individually. 
  
  #### R Installation <a name="adding-r"></a>
  To install R through Bitvise:
  ```console
  $ apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
  $ add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/'
  $ apt update
  $ apt install r-base r-base-dev
  ```
  
  Start R:
  ```console
  $ R
  ```
  
  <br>
  
  #### Update and Install R Kernel <a name="update-and-install-r-kernel"></a>
  
  Update all packages in the current environment to the latest version, without prompts for permission:
  ```r
  update.packages(ask = FALSE)
  install.packages('IRkernel', lib = '/usr/local/lib/R/site-library')
  ```
  
  Make Jupyter see the newly installed R kernel by installing a kernel spec. For system-wide installation, set user to False in the installspec command:
  ```r
  IRkernel::installspec(user = FALSE)
  ```

  Additional Ubuntu linux packages are needed for 'tidyverse' in R. Then install tidyverse for all users.
  ```r
  apt install libcurl4-openssl-dev libssl-dev libxml2-dev
  install.packages("tidyverse", dependencies = TRUE, INSTALL_opts = '--no-lock')
  ```
 
 <details>
  <summary>:bulb: Examples of other packages</summary>
 
  ```r
  install.packages("openxlsx", lib = '/usr/local/lib/R/site-library', dependencies = TRUE, INSTALL_opts = '--no-lock')
  install.packages("knitr", lib = '/usr/local/lib/R/site-library', dependencies = TRUE, INSTALL_opts = '--no-lock')
  ```
  
  </details>
  
  When ready, quit:
  ```r
  q()
  ```
  
  [Back to Top](#econometric-pedagogy)


## Stata

  The following directions are for use in the Bitvise (or other choise SSH software) terminal console. Unless otherwise specified, type and run each line individually. 
  
  :bulb: Instructors should contact Stata to discuss the best licensing options. A Stata Labs license may be best for this workflow, with the lab size corresponding to the number of students in the lab.
  
  #### Stata Installation <a name="adding-stata"></a>
  Download [Stata](https://www.stata.com/support/faqs/unix/install-download-on-linux/) for Linux  
 
 To upload Stata, create a folder for your Stata installation file:
  ```console
 $ mkdir /home/ubuntu/stata_source
  ```
  
 Place your Stata for Linux installation file into this folder:
 ```console
 cd /usr/local
 $ mkdir stata16
 $ cd stata16
 ```
 
 Install Stata. Enter licensing information when prompted.
 ```console
 $ /home/ubuntu/stata_source/install
 ```
 
 During installation, you will be prompted to run the following. 
 ```console
 $ ./stinit
 ```
 
 Ubuntu users will be need to enter the following.
 ```console
 $ apt install libtinfo5
  ```
 
 To add a path to Stata, open profile with nano:
 ```console
 ubuntu@ip-xx-xxx:~$ nano /etc/profile
 ```
 
 Type the following into the bottom of the document as depicted below.
 ```console
 export PATH="/usr/local/stata16:$PATH"
 ```
 
 <p align="center">
   <img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/enter%20stata%20path.png" width = "400" height = "400" />
 </p>
 
 Use <kbd>CTRL</kbd>+<kbd>O</kbd> then <kbd>enter</kbd> to overwrite the document and <kbd>CTRL</kbd>+<kbd>X</kbd> to exit.
 
 #### Stata Kernel for Jupyter <a name="stata-kernel"></a>
 
 The following line will allow Jupyter users to create and run documents with a Stata kernel.
 ```console
 $ pip install stata_kernel
 ubuntu@ip-xx-xxx:~$ python -m stata_kernel.install
 ```
 Ensure that the stata_kernel is installed correctly:
 ```console
 $ nano .stata_kernel.conf
 ```
 You should see:
 
  <p align="center">
   <img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/stata_kernel.PNG" width = "400" height = "400" />
 </p>
 
  Copy configuration file to system configuration for all users:
 ```console
 $ cp .stata_kernel.conf /etc/stata_kernel.conf 
 ```
 
  
  [Back to Top](#econometric-pedagogy)

## (Optional) GitHub Extensions and Packages <a name="packages"></a>

The optional packages showcased below personalize your server to expidite online instruction. 

 <details>
    <summary>Expand</summary>
    <br>
  Contents
 
  1. [GitHub Extension](#extension)
  2. [nbgrader](#nbgrader)

  ###### GitHub Extension <a name="extension"></a>
  
  This extension will show up on a side bar of the students interface. When clicked, students can gain access to public repositories, such as notebook based assignments. Through use of the server's terminal, a student can also access private repositories. 
  
  ```console
  # Install the extension for JupyterLab
  $ jupyter labextension install @jupyterlab/github
  
  # Restart to ensure recognition of the new extension
  $ systemctl restart jupyterhub.service
  
  #Fully enable the GitHub viewing extension
  $ conda install -c conda install -c conda-forge jupyter-github
  ```
  ###### nbgrader
  
  The package [nbgrader](https://nbgrader.readthedocs.io/en/stable/) helps streamline the grading process for instructors using jupyter notebooks. Notebook based assignments can be created, collected, and returned with little hassle. 
  
  ```console
  conda install -c conda-forge nbgrader
  ```
 </details>
  
## (Optional) GitHub Integration <a name="github-authentication"></a>

  This section provides a guide to allowing the server to use GitHub credidentials in the log-in process. By entering in their GitHub log-in information, students can access and use the server, without the instructor having to manually enter each user and admin. As a reminder, a student can set up a GitHub account for free. An advanced understanding of the command line is recommended before attempting.

 <details>
    <summary>Expand</summary>
    <br>
Contents
 
1. [Generate Cookie Secret](#cookie-secret)
2. [Add a Custom Domain](#custom-url)
3. [Secure Your Lab](#secure-lab)
4. [Add GitHub Authentication](#authentication-final)
5. [Setting Up a Reverse Proxy](#reverse-proxy)

The following directions are for use in the Bitvise (or other choise SSH software) terminal console. Unless otherwise specified, type and run each line individually. 

 #### Generate Cookie Secret <a name="cookie-secret"></a>
Encrypt the your lab's [cookie](https://en.wikipedia.org/wiki/HTTP_cookie) for security purposes.
```console
# Create a new directory
$ mkdir /srv/jupyterhub

# Generate a random number and save it as the cookie secret
$ openssl rand -hex 32 > /srv/jupyterhub/jupyterhub_cookie_secret

$ Open JupyterHub's configuration file
$ nano /etc/jupyterhub/jupyterhub_config.py

# Copy the following and add it to the file:
c.JupyterHub.cookie_secret_file = '/srv/jupyterhub/jupyterhub_cookie_secret'

# Ensure that only the administrator can read and write the cookie secret
$ chmod 600 /srv/jupyterhub/jupyterhub_cookie_secret
```

#### Add a Custom Domain <a name="custom-url"></a>

Instructors may use Amazon Web Services, a university domain, or any other domain service to add a custom domain, which is necessary for setting up GitHub authentication. This demonstration uses [Google Domains](https://domains.google/). With an existing custom domain, you may add the lab as a sub-domain as done below. This tutorial assumes an existing domain has been registered with Google Domains. Visit the [Google Domains Learning Center](https://domains.google/learning-center/) for more information on this. 

  <details>
    <summary>:bulb: What is a sub-domain?</summary>
    <br>
 
  A sub-domain is an additional section of a domain that can help organize, specify, or navigate to different websites under a single primary domain.
  
  For example, while navigating from a website `www.example.com` to its store, you may see the domain change to `store.example.com`. This shortens the domain and makes it easier for you and your students to remember. The following method requires a domain to aquire the proper safety features.
   
  </details>

|<img src="https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/domain_assign.gif" width="800" height="370" />|
|---|

Navigate to the "Domain Name Servers," then to "Custom resource records." Enter the desired name (jupyterlab, econlab, etc.). Then enter the IP4 address of your instance.

:warning: This will take up to 48 hours to update and begin serving as a functioning URL. :warning:

#### Secure Your Lab <a name="secure-lab"></a>
The following instructions will allow the inclusion of "https://" in your lab address, ensuring the security needed to utilize GitHub authorizations and sign-ins.

:warning: By allowing students to log in with their GitHub credientials, the server is much more vulnerable. It is highly recommended the following steps are followed so "https://" can be included in your lab address to protect against outside threats. :warning:

```console

# Create a key 
$ openssl dhparam -out /etc/jupyterhub/dhparam.pem 2048

#Make it so that only the administrator can edit
$ chmod 600 /etc/jupyterhub/dhparam.pem

#Link this file to the system folder
$ ln -s /etc/jupyterhub/dhparam.pem /etc/ssl/certs/dhparam.pem

```
Generate an SSL Certificate using Certbot.
```console

# Update Ubuntu and install the necessary software
    $ apt-get update
    $ apt-get install software-properties-common
    $ add-apt-repository universe
    $ apt-get update
```
Install [Certbot](https://certbot.eff.org/lets-encrypt/ubuntufocal-nginx).

```console
$ apt-get install certbot python3-certbot-nginx
```

Navigate to the AWS Console. Go to the Security Groups settings and select your instance. Edit the inbound rules. Add "HTTP" and save. 

|<img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/http_security.gif"  width="800" height="370" />|
|---|

```console
#Add this line so you do not need to shut down the server before proceeding
$ certbot certonly --nginx
```
You will be prompted to enter an email and a domain (the newly added custom domain, for example: "jupyterlab.professorx.com")
```console
$ certbot renew --dry-run
```

You should see:
 - Congratulations! Your certificate and chain have been sav
   /etc/letsencrypt/live/your-domain/fullchain.pem
   Your key file has been saved at:
   /etc/letsencrypt/live/your-domain/privkey.pem

Install nginx so you do not have to type ":8000" at the end of the URL. 
```console
$ apt install nginx
```
Create a new configuration file to create the certificate on the nginx server.
```console
$ nano /etc/nginx/sites-available/jupyterhub.conf
```
Copy and paste the following code into this file, being careful to modify the text to include your domain wherever "YOUR-DOMAIN" is present.
```
# top-level http config for websocket headers
# If Upgrade is defined, Connection = upgrade
# If Upgrade is empty, Connection = close
map $http_upgrade $connection_upgrade {
    default upgrade;
    ''      close;
}

# HTTP server to redirect all 80 traffic to SSL/HTTPS
server {
    listen 80;
    #listen [::]:80;
    server_name YOUR-DOMAIN;

    # Tell all requests to port 80 to be 302 redirected to HTTPS
    return 302 https://$host$request_uri;
}

# HTTPS server to handle JupyterHub
server {
    listen 443 ssl http2;
    #listen [::]:443 ssl http2;
    server_name YOUR-DOMAIN;

    ssl_certificate /etc/letsencrypt/live/test.atyho.info/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/test.atyho.info/privkey.pem;
    ssl_session_timeout 1d;
    ssl_session_cache shared:MozSSL:10m;  # about 40000 sessions
#    ssl_session_cache shared:SSL:50m;
    ssl_session_tickets off;

    ssl_dhparam /etc/ssl/certs/dhparam.pem;

    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384;
#    ssl_ciphers 'ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:AES:CAMELLIA:DES-CBC3-SHA:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!aECDH:!EDH-DSS-DES-CBC3-SHA:!EDH-RSA-DES-CBC3-SHA:!KRB5-DES-CBC3-SHA';
    ssl_prefer_server_ciphers on;

    # HSTS (ngx_http_headers_module is required) (63072000 seconds)
    add_header Strict-Transport-Security "max-age=63072000" always;
    #add_header Strict-Transport-Security max-age=1576800;

    # OCSP stapling
    ssl_stapling on;
    ssl_stapling_verify on;

    # Managing literal requests to the JupyterHub front end
    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

        # websocket headers
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection $connection_upgrade;
    }

    # Managing requests to verify letsencrypt host
    location ~ /.well-known {
        allow all;
    }
}
```

Link this new configuration file
```console
# Unlink the default file
$ unlink /etc/nginx/sites-enabled/default

# Link the new file
$ ln -s /etc/nginx/sites-available/jupyterhub.conf /etc/nginx/sites-enabled/jupyterhub.conf

# Restart nginx
$ systemctl restart nginx.service

```

#### Add GitHub Authentication <a name="authentication-final"></a>
Execute the following to set up a method for students to sign in using GitHub.

From your GitHub account, navigate to the Developer Settings. Choose OAth Apps and create a New OAth app. Enter the corresponding information. Enter [https://YOUR-URL/hub/oauth_callback]() as the Authorization callback URL, being careful to replace YOUR-URL with the link to your lab.

|<img src="https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/github_oath.gif" width="800" height="370" />|
|---|

```console
# Install GitHub OAuth 
conda install -c conda-forge oauthenticator

# Open the JupyterHub configuration file
$ nano /etc/jupyterhub/jupyterhub_config.py
```
Enter the following into the file, being careful to replace the URL, Client ID, and Client Secret with your own. The Client ID and Client Secret can be found on the page of the GitHub "app" created above.

```console
from oauthenticator.github import LocalGitHubOAuthenticator
c.JupyterHub.authenticator_class = LocalGitHubOAuthenticator
c.LocalGitHubOAuthenticator.oauth_callback_url = 'YOUR-URL/hub/oauth_callback'
c.LocalGitHubOAuthenticator.client_id = 'YOUR CLIENT ID'
c.LocalGitHubOAuthenticator.client_secret = 'YOUR CLIENT SECRET'

#This line means that it will no longer be necessary to manually add new users.
c.LocalGitHubOAuthenticator.create_system_users = True

c.JupyterHub.bind_url = 'http://127.0.0.1:8000'
```
It should look like this:

<p align="center">
    <img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/oath_editor.png" width = "500" height = "500" />
</p>

:warning: Notice that you may also change the admin username to your GitHub username to allow administrative access. :warning:

Reboot the server. 
```console
$ systemctl restart jupyterhub.service
```

#### Setting Up a Reverse Proxy <a name="reverse-proxy"></a>

A reverse proxy is an added level of security which connects externel servers to internel clinets while hiding ip addresses from being veiwed externally. This guide uses [nginx](https://www.nginx.com/) as its reverse proxy server.

Begin by opening jupyterhub's configuration file in nano.
```console
$ nano /opt/jupyterhub/etc/jupyterhub/jupyterhub_config.py
```

```
c.JupyterHub.bind_url = 'http://127.0.0.1:8000'
```

Install nginx and open its configuration file in nano.
```console
$ apt install nginx
$ nano /etc/nginx/nginx.conf
```

Copy and paste the follwoing text:
```
server{

  location /jupyter/ {    
    # NOTE important to also set base url of jupyterhub to /jupyter in its config
    proxy_pass http://127.0.0.1:8000;

    proxy_redirect   off;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header Host $host;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;

    # websocket headers
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection $connection_upgrade;

  }
}
```

To finish, restart the server.
```console
$ systemctl restart nginx.service
```
  
  </details>
  
  [Back to Top](#econometric-pedagogy)
  

## Disclaimer 

 
This instructional guide is part of a demonstration used for “*Econometric Pedagogy and Cloud Computing: Training the Next Generation of Economists and Data Scientists*”. There is no guarantee this methodology works for others. For specific needs or troubleshooting, independent research may be necessary. 

**AWS Educate and corresponding services are trademark of [Amazon Web Services](https://aws.amazon.com/).**

**Stata is trademark of [Stata Corporation](https://www.stata.com/).**

**Google Domain is trademark of [Google](https://www.google.com/).**

**Python is developed on an open source license distributed by the [Python Software Foundation](https://www.python.org/psf/).**

**R is offered on an open source license distributed by the [R Foundation](https://www.r-project.org/foundation/).**

**JupyterHub is an open source platform developed and maintained by [Project Jupyter](https://jupyter.org/).**


[Back to Top](#econometric-pedagogy)
  

