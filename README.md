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
2. [Functionality](#functionality)
3. [Prerequisites](#prerequisites)
4. [Launching an Instance via AWS](#lauching-an-instance-via-aws)
   1. [Customizing an Instance](#seven-steps)
   2. [Navigating Bitvise](#navigating-bitvise)
5. [Anaconda](#anaconda)
   1. [Loading Anaconda](#loading-anaconda)
   2. [JupyterHub](#jupyterhub)
6. [R](#r)
   1. [Adding R](#adding-r)
   2. [Update and Install R Kernel](#update-and-install-r-kernel)
7. [Stata](#stata)
   1. [Adding Stata](#adding-stata)
   2. [Stata Kernel for Jupyter](#stata-kernel)
8. [Optional GitHub Intergration](#github-intergration)
9. [Disclaimer](#disclaimer)

## Overview 

<br>

The following instructions document a step-by-step guide to setting up a virtual “Econometrics Lab” hosted in the cloud. Ultimately, students will be able to connect to the lab via a web browser with a username and password and have access to JupyterLab and Jupyter Notebooks with Python, R, and Stata kernels. A group video chat service provider such as MS teams or Google hangout can be used alongside for synchronous instruction.

The guide below corresponds to workflow 3 outlined in “Econometric Pedagogy and Cloud Computing: Training the Next Generation of Economists and Data Scientists,” though the instructions may be modified to suit different teaching styles and classroom needs.

## Functionality

This section will outline the functionality of the server after the below steps are completed. For more detail, including other possible workflows for cloud-based learning in Economentrics, view Econometric Pedagogy and Cloud Computing: Training the Next Generation of Economists and Data Scientists.

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
  
  The following directions are for use in the Bitvise (or other choice SSH software) terminal console. Unless otherwise specified, type and run each line individually. 
  
  To request root access:
  ```console
  ubuntu@ip-xx-xxx:~$ sudo -i
  ```
  
  After launching an instance with your selected cloud service provider, update the Ubuntu repository and upgrade packages with:
  ```console
  ubuntu@ip-xx-xxx:~$ apt-get update
  ubuntu@ip-xx-xxx:~$ apt-get upgrade
  ```
  
  To create a new administrator or student, respectively:
  ```console
  ubuntu@ip-xx-xxx:~$ adduser admin
  ubuntu@ip-xx-xxx:~$ adduser student
  ```

The instance is now launched and hosted on a client. 
Continue reading the “Anaconda” section to download the distribution onto the newly created instance. 

[Back to Top](#econometric-pedagogy)


## Anaconda

  The following directions are for use in the Bitvise (or other choise SSH software) terminal console. Unless otherwise specified, type and run each line individually. 
  
  #### Loading Anaconda <a name="loading-anaconda"></a>
  
  To install Anaconda:
  ```console
  ubuntu@ip-xx-xxx:~$ wget https://repo.anaconda.com/archive/Anaconda3-2020.02-Linux-x86_64.sh
  ubuntu@ip-xx-xxx:~$ bash Anaconda3-2020.02-Linux-x86_64.sh
  ```
  When prompted with `[/root/anaconda3] >>>` enter:
  
  ```console
  ubuntu@ip-xx-xxx:~$ /usr/anaconda3
  ```
 
  In order for Anaconda to operate, the following command needs to be entered:
  ```console
  ubuntu@ip-xx-xxx:~$ source .bashrc
  ```
 
  Open the profile in nano with the following command.
  ```console
  ubuntu@ip-xx-xxx:~$ nano /etc/profile
  ```
  
  Enter the follwoing into the bottom of the document as shown below.
  ```
  export PATH="/usr/anaconda3/bin:$PATH
  ```
  
  <p align="center">
    <img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/enter%20anaconda%20path.png" width = "400" height = "400" />
  </p>
  
  Use <kbd>CTRL</kbd>+<kbd>O</kbd> then <kbd>enter</kbd> to overwrite the document and <kbd>CTRL</kbd>+<kbd>X</kbd> to exit.
  <br>
  
  #### JupyterHub: 
  
  Install [JupyterHub](https://jupyterhub.readthedocs.io/en/stable/quickstart.html).
 
  First, make sure conda is up to date by entering: 
  ```console
  ubuntu@ip-xx-xxx:~$ conda update -n root conda
  ```

  Update all packages in the current environment to the latest version:
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
  ubuntu@ip-xx-xxx:~$ c.Spawner.default_url = '/lab'
  ubuntu@ip-xx-xxx:~$ c.JupyterHub.admin_access = True
  ubuntu@ip-xx-xxx:~$ c.Authenticator.admin_users = {'admin'}
  ubuntu@ip-xx-xxx:~$ c.JupyterHub.shutdown_on_logout = True
  ubuntu@ip-xx-xxx:~$ c.Spawner.disable_user_config = True
  ```
  
  In nano, create and open a file with the following command.
  ```console
  ubuntu@ip-xx-xxx:~$ nano /etc/jupyterhub/jupyterhub.service
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
  
  The following directions are for use in the Bitvise (or other choise SSH software) terminal console. Unless otherwise specified, type and run each line individually. 
  
  #### Adding R <a name="adding-r"></a>
  To install R through Bitvise:
  ```console
  ubuntu@ip-xx-xxx:~$ apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
  ubuntu@ip-xx-xxx:~$ add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/'
  ubuntu@ip-xx-xxx:~$ apt update
  ubuntu@ip-xx-xxx:~$ apt install r-base r-base-dev
  ```
  
  Start R by typing:
  ```console
  ubuntu@ip-xx-xxx:~$ R
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
  
  :bulb: Instructors should contact Stata to discuss the best licencing options. A Stata Labs licences may be best for this workflow, with the lab size corresponding to the number of students in the lab.
  
  #### Adding Stata <a name="adding-stata"></a>
  Download [Stata](https://www.stata.com/support/faqs/unix/install-download-on-linux/) for Linux    
  Download [Stata kernel](https://kylebarron.dev/stata_kernel/) for Jupyter Notebook  
 
 To upload Stata, create a folder for your Stata installation file:
  ```console
  ubuntu@ip-xx-xxx:~$ mkdir /home/ubuntu/stata_source
  ```
  
 Place your Stata for Linux installation file into this folder:
 ```console
 cd /usr/local
 ubuntu@ip-xx-xxx:~$ mkdir stata16
 ubuntu@ip-xx-xxx:~$ cd stata16
 ```
 
 Install Stata. Enter licensing information when prompted.
 ```console
 ubuntu@ip-xx-xxx:~$ /home/ubuntu/stata_source/install
 ```
 
 During installation, you will be prompted to run the following. 
 ```console
 ubuntu@ip-xx-xxx:~$ ./stinit
 ```
 
 Ubuntu users will be need to enter the following.
 ```console
 ubuntu@ip-xx-xxx:~$ apt install libtinfo5
  ```
 
 To add a path to Stata, open profile with nano:
 ```console
 ubuntu@ip-xx-xxx:~$ nano /etc/profile
 ```
 
 Type the follwing into the bottom of the document as depicted below.
 ```console
 export PATH="/usr/local/stata16:$PATH"
 ```
 
 <p align="center">
   <img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/enter%20stata%20path.png" width = "400" height = "400" />
 </p>
 
 Use <kbd>CTRL</kbd>+<kbd>O</kbd> then <kbd>enter</kbd> to overwrite the document and <kbd>CTRL</kbd>+<kbd>X</kbd> to exit.
 
 #### Stata Kernel for Jupyter <a name="stata-kernel"></a>
 
 The follwoing line will allow Jupyter users to create and run documents with a Stata kernel.
 ```console
 ubuntu@ip-xx-xxx:~$ pip install stata_kernel
 ubuntu@ip-xx-xxx:~$ python -m stata_kernel.install
 ```
 Ensure that the stata_kernel is installed correctly:
 ```console
 ubuntu@ip-xx-xxx:~$ nano .stata_kernel.conf
 ```
 You should see:
 
  <p align="center">
   <img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/stata_kernel.PNG" width = "400" height = "400" />
 </p>
 
  Copy configuration file to system configuration for all users:
 ```console
 ubuntu@ip-xx-xxx:~$ cp .stata_kernel.conf /etc/stata_kernel.conf 
 ```
 
  
  [Back to Top](#econometric-pedagogy)
  
## Optional GitHub Intergration <a name="github-intergration"></a>

  This section provides an advanced guide to intergrating GitHub with the server. While much of GitHub's functioanlity is sacraficed in this method, an instructor is saved from having to add each student and admin individually; instead, students can log in using their GitHub accounts. As a reminder, a student can set up a GitHub account for free if she or he does not already have on set up. 

  The following directions are for use in the Bitvise (or other choise SSH software) terminal console. Unless otherwise specified, type and run each line individually. 
  
  <details>
    <summary>:bulb: Function under test</summary>
 
  ```console
  # GitHub OAuth 
conda create -n jupyerhubenv python=3.6
$ conda activate jupyterhubenv
conda install -c conda-forge oauthenticator

# Create dhparam.pem
openssl dhparam -out /etc/jupyterhub/dhparam.pem 2048
chmod 600 /etc/jupyterhub/dhparam.pem

ln -s /etc/jupyterhub/dhparam.pem /etc/ssl/certs/dhparam.pem

# Obtain SSL Certificates
    sudo apt-get update
    sudo apt-get install software-properties-common
    sudo add-apt-repository universe
    sudo apt-get update

Install Certbot

Run this command on the command line on the machine to install Certbot.

sudo apt-get install certbot
sudo certbot certonly --webroot
sudo certbot renew --dry-run

 - Congratulations! Your certificate and chain have been sav
   /etc/letsencrypt/live/test.atyho.info/fullchain.pem
   Your key file has been saved at:
   /etc/letsencrypt/live/test.atyho.info/privkey.pem

apt install nginx

nano /etc/nginx/sites-available/jupyterhub.conf

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
    server_name test.atyho.info;

    # Tell all requests to port 80 to be 302 redirected to HTTPS
    return 302 https://$host$request_uri;
}

# HTTPS server to handle JupyterHub
server {
    listen 443 ssl http2;
    #listen [::]:443 ssl http2;
    server_name test.atyho.info;

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

unlink /etc/nginx/sites-enabled/default
ln -s /etc/nginx/sites-available/jupyterhub.conf /etc/nginx/sites-enabled/jupyterhub.conf

systemctl restart nginx.service

# Force the proxy to only listen to connections to 127.0.0.1
nano /etc/jupyterhub/jupyterhub_config.py
c.JupyterHub.bind_url = 'http://127.0.0.1:8000'
c.LocalGitHubOAuthenticator.oauth_callback_url = 'https://test.atyho.info/hub/oauth_callback'

# Don't forget to update GitHub OAuth settings!

systemctl restart jupyterhub.service
  ```
 
  </details>
  
  <details>
  <summary>:bulb: Generate cookie secret</summary>
 
  ```console
  mkdir /srv/jupyterhub
openssl rand -hex 32 > /srv/jupyterhub/jupyterhub_cookie_secret

nano /etc/jupyterhub/jupyterhub_config.py
c.JupyterHub.cookie_secret_file = '/srv/jupyterhub/jupyterhub_cookie_secret'

chmod 600 /srv/jupyterhub/jupyterhub_cookie_secret

  ```
 
  </details>
  
  <details>
  <summary>:bulb: Optional packages</summary>
 
  nbgitpuller:
  ```console
  conda install -c conda-forge nbgitpuller

  Use https://jupyterhub.github.io/nbgitpuller/link to generate link to git

  http://18.215.104.126:8000/hub/user-redirect/git-pull?repo=https%3A%2F%2Fgithub.com%2Fdjachoc%2FEmpirical-Methods-ML&app=lab
  ```
  
  nbgrader:
  ```console
  conda install -c conda-forge nbgrader
  ```
 
  </details>
  
  <details>
  <summary>:bulb: Setting up a reverse proxy</summary>
 
  ```console
  sudo nano /opt/jupyterhub/etc/jupyterhub/jupyterhub_config.py
c.JupyterHub.bind_url = 'http://127.0.0.1:8000'

sudo apt install nginx
sudo nano /etc/nginx/nginx.conf

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

sudo systemctl restart nginx.service
  ```
 
  </details>
  
  
  [Back to Top](#econometric-pedagogy)
  

## Disclaimer 

 
This instructional guide is part of a demonstration used for “Econometric Pedagogy and Cloud Computing: Training the Next Generation of Economists and Data Scientists”. There is no guarantee this methodology works for others. For specific needs or troubleshooting, independent research may be necessary. 

AWS Educate and corresponding services are trademark of Amazon Web Services.

Stata is trademark of Stata Corporation.

Python is developed on an open source license distributed by the [Python Software Foundation](https://www.python.org/psf/).

R is offered on an open source license distributed by the [R Foundation](https://www.r-project.org/foundation/).

JupyterHub is an open source platform developed and maintained by [Project Jupyter](https://jupyter.org/).


[Back to Top](#econometric-pedagogy)
  

