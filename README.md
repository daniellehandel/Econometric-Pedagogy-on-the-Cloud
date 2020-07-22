
# Econometric Pedagogy and Cloud Computing: Training the Next Generation of Economists and Data Scientists <a name="econometric-pedagogy"></a>
 
[Danielle V. Handel](https://www.linkedin.com/in/danielle-handel-134b53173/), [Anson T. Y. Ho](http://www.atyho.info), [Kim P. Huynh](https://www.bankofcanada.ca/profile/kim-huynh/), [David T. Jacho-Chávez](https://www.davidjachochavez.org/), [Carson H. Rea](https://www.linkedin.com/in/carson-rea-979062198/)

<br>

_________________________________________________________________________________________________________

<img align="right"
     src="https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/workflow_3.png" 
     width="600" height="460" />

## Table of Contents
1. [Overview](#overview)
2. [Functionality](#functionality)
   1. [Standard Functionality](#std-func)
   2. [(Optional) GitHub Integrated Functionality](#github-func)
3. [Pre-requisites](#pre-requisites)
4. [AWS: Instance Launching](#lauching-instance)
   1. [Customizing an Instance](#seven-steps)
   2. [Assigning an Elastic IP Address](#elastic-ip)
   3. [Connecting to Your Cloud](#navigating-bitvise)
5. [Updating Your Server and Adding New Users](#server-basics)
6. [Anaconda](#anaconda)
   1. [Anaconda Installation](#loading-anaconda)
   2. [JupyterHub Installation and Configuration](#jupyterhub)
7. [R](#r)
   1. [R Installation](#adding-r)
   2. [Update and Install R Kernel](#update-and-install-r-kernel)
8. [Stata](#stata)
   1. [Stata Installation](#adding-stata)
   2. [Stata Kernel for Jupyter](#stata-kernel)
9. [(Optional) GitHub Extensions and Packages](#packages)
10. [(Optional) GitHub Authentication](#github-authentication)
11. [Disclaimer](#disclaimer)

## Overview 

The following demonstration documents a step-by-step guide to setting up a virtual “Econometrics Lab” hosted by [Amazon Web Service (AWS)](https://aws.amazon.com/), one of the many cloud providers. Ultimately, students will be able to connect to an environment to preform live coding on [Jupyter Notebooks](https://jupyter.org/) with [Python](https://www.python.org/psf/), [R](https://www.r-project.org/foundation/), and [Stata](https://www.stata.com/) kernels.

<!---
The demonstration concludes with a method of integrating GitHub so that students may sign in with their GitHub accounts. This method is optional, and is recommended for those with an advanced uderstanding of the command line. 
--->

This demonstration corresponds to workflow 3 outlined in “*_Econometric Pedagogy and Cloud Computing: Training the Next Generation of Economists and Data Scientists_*,” though the instructions may be modified to suit different teaching styles and classroom needs.

## Functionality

This section showcases a fully operational server and the optional GitHub integration.

#### Standard Functionality <a name="std-func"></a>

|<img src="https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/base_functionality.gif" width="800" height="400" />|
|---|

After entering the lab with a pre-assigned username and password, students may generate new Jupyter Notebooks using R, Python, or Stata. They also may upload notebooks from their local machine or clone repositories from [GitHub](https://github.com) and work on those. None of this requires installation of any software on the local machine.

#### (Optional) GitHub Integrated Functionality <a name="github-func"></a>

Demonstrated below is the additional functionality granted by following the optional sections, [GitHub Extensions and Packages](#packages) and [GitHub Authentication](#github-authentication).

|<img src="https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/loginGitHubDemo.gif" width="800" height="400" />|
|---|

A student with their free GitHub account setup can select the "Sign in with GitHub" to be prompted to authorize the server to use GitHub when logging in. After selecting the button to authorize, the student will be directed to the JupyterHub interface and may begin working.

|<img src="https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/djachocGitHubDemo.gif" width="800" height="400" />|
|---|

The GitHub extension allows the student to access repositories as demonstrated above. By typing in a username, the student will be granted access to all of the *public* repositories that person has. A students can gain access to assignments directly from their instructor's GitHub.

[Back to Top](#econometric-pedagogy)

## Pre-requisites
 
To begin launching an instance, the following pre-requisites are required:

1. Hardware: Personal computer with internet connection.
2. Software:
   1. SSH Client.
   2. Stata license (contact your department's IT service).
3. Cloud Service:
   1. AWS account.
   2. GitHub account (optional).

[Back to Top](#econometric-pedagogy)
 

## AWS: Instance Launching <a name="lauching-instance"></a>
  
  This section details a method of launching an instance on AWS EC2 (Elastic Compute Cloud). Written instruction can be found below the corresponding demonstrational gif.

  <details>
    <summary>:bulb: What is an instance?</summary>
    <br>
     
  An instance in AWS is a type of virtual envirnoment. There are several types that AWS provides depending on the intended purpose; this demonstration walks through the launching of a free-tier EC2 instance. More information can be found in the [EC2 documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Instances.html) on the AWS website.
     
  </details>

  #### Customizing an Instance <a name="seven-steps"></a>
<!--- 
|<img src="https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/1_nav_to_console_.gif" width="800" height="370" />|
|---|
--->

<!---
  Log into your AWS Educate account. The "My Classrooms" tab on the top banner in the interface directs to the complete list of classrooms created on the account. From there, select the desired classroom by clicking the blue "Go to classroom" button. The third-party application, Vocareum, will launch, showing an overview of the classroom. To manage, select "AWS console." To launch the proper instance, select EC2 from the dropdown menu labeled "All services". 
--->

<!---
   :warning: Your browser may block pop-ups from Vocareum. :warning:
--->  
  
|<img src="https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/2_start_instance.gif" width="800" height="370" />|
|---|

  Log into your AWS account. To launch the proper instance, select EC2 from the dropdown menu labeled "All services".
  
  Select a Linux server as the desired Amazon Machine Image (AMI). This demonstration selects Ubuntu 20.4 LTS, though other Linux servers will also be suitable. 

  Select an instance type. *_This should be chosen based on class size and computational needs_*. For AWS's free tier, choose "General purpose" family and "t2.micro" type. Click "Next: Configure Image" to continue.
 
  Immediately continue to "Next: Add Storage."

  <br>
  
|<img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/3_security_group.gif"  width="800" height="370" />|
|---|
  
Change the storage from the default to 30 GB. *_This should be chosen based on class size and computational needs_*. Continue to “Next: Add Tags”.

Tags are optional metadata that describe the instance for categorization and organization purposes. To add a tag, the "Add a tag" button is located on the bottom left. Otherwise, continue to "Next: Configure Security Groups".

The default SSH rule will use the standard port 22. Change the source to “Anywhere” to allow the Ubuntu system adminstrator with any IP address to access the instance. For improved security, one can change the source to only allow specific IP. 

Since JupyterHub uses port 8000 as default for connecting to the internet, it has to be included in the security group. Add a second custom TCP security rule by clicking the “Add Rule” button. Modify the rule to include port 8000. Add an optional description of “JupyterHub.” Continue to the final stage by clicking the blue “Review and Launch” button. 

   <details>
    <summary>:bulb: What is port range?</summary>
    <br>
 
   A port is a designated number that specifies a network service for operating systems. E.g. Port 80 is assigned to HTTP (Hypertext Transfer Protocol). These are tied to the IP address and communicate the purpose of the network. The TCP (Transmission Control Protocol) port 22 is the default for SSH (Secure Shell). TCP Port 8000 is the default for JupyterHub. 
   
   </details>

Now, “Launch”.
  
  <br>

|<img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/5_launch_and_key.gif"  width="800" height="370" />|
|---|
  
  Selecting “Launch” will prompt the user to select an existing SSH key pair or create a new one. Name and download your key pair.

   :warning: Important to keep the key private and safe. Losing the key will render your instance inaccessible. Sharing the key could leave your instance vulnerable to unauthorized access.

   <details>
    <summary>:bulb: What is an SSH key?</summary>
    <br>
 
   An SSH key pair serves as the "password" which connects a SSH client to the server. This demonstration suggests the use of Bitvise, although other clients, such as PuTTY for Windows/Unix users or the Terminus App for Mac users, can serve as substitutions. 
   
   </details>

#### Assigning an Elastic IP Address <a name="elastic-ip"></a>

  In case your instance is stopped or failed, restarting or relaunching your instance will end up with a different public IP address. This becomes inconvenient if users have to change the address for accessing JupyterHub. This section will demonstrate the proper set-up for allocating a static IP address to your AWS instance. For this purpose, an [Elastic IP address](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/elastic-ip-addresses-eip.html) can be allocated to your account and asociated with an instance, so that users can always access your JupyterHub with the same IP.
  
|<img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/allocate_elastic.gif"  width="800" height="370" />|
|---|

Navigate to the Elastic IP configuration on the AWS EC2 Console. Opt to allocate an elastic IP address from Amazon's pool of IPv4 addresses. Then, choose to associate this new address and select your instance. Th Elastic IP is now your instance's public IP. 
  
#### Connecting to Your Cloud <a name="navigating-bitvise"></a>
  
|<img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/4_IP_into_bitvise.gif"  width="800" height="370" />|
|---|

The instance will now be visible in the EC2 homepage. The description of the instance and the IP address can be found at the bottom of the instance page. Open [Bitvise](https://www.bitvise.com/ssh-client-download) as an SSH client. Copy the IPv4 Public IP address from the instance page in EC2 and paste it into “Host” on Bitvise. Insert 22 as the port. 

   <details>
    <summary>:bulb: What is an SSH Client?</summary>
    <br>
 
   An SSH client allows establishing a secure and authenticated SSH connections to SSH server. Download [Bitvise SSH Client](https://www.bitvise.com/ssh-client-download) or [PuTTY](https://www.putty.org/) for Windows or [Terminus App](https://termius.com/) for MacOS.
   
   </details>

  <br>
  
|<img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/6_put in key.gif"  width="800" height="370" />|
|---|
  
  Enter "ubuntu" as the default username. Change the following line “Initial method” to publickey. For first-time log in, select "Client key manager" and import the SSH key downloaded earlier (named as Global 1 in this example). An optional comment can be left for organization purposes if desired. Select the key just imported in the “client key” line. Click "Log In" to connect. 
  
[Back to Top](#econometric-pedagogy)
  
## Updating Your Server and Adding New Users <a name="server-basics"></a>

:bulb: The following directions are for use on Ubuntu servers.

  :warning: Obtain administrative rights by requesting root access:
  ```console
  $ sudo -i
  ```
  
  Update the Ubuntu repository and upgrade packages with:
  ```console
  $ apt update
  $ apt upgrade
  ```
  
  Create new Ubuntu system users, say, designated JupyterHub administrator "admin1" and JupyterHub user "student", write:
  ```console
  $ adduser admin1
  $ adduser student
  ```
  
  You will be prompted to enter a password and information for each new user. Note: when typing the password, the cursor will not appear to move. 
  
  <details>
    <summary>:bulb: Why do I need to add new users? Is there other ways? </summary>
    <br>
 
   By default, JupyterHub uses PAM (Pluggable Authentication Module) to authenticate system users with their username and password, i.e. any user with an account and password on the Ubuntu system will be allowed to login. Alternatively, GitHub Authentication provides a guide to giving students the ability to login to the server with their GitHub credentials. View the section [GitHub Authentication](#github-authentication) to determine whether it is right for your server.
   
   :warning: JupyterHub administrator (we will assign [below](#jupyterhub)) does not need to have Ubuntu system administrative rights
   
  </details>

Continue reading the “[Anaconda](#anaconda)” section to set up Anaconda on the instance. 

[Back to Top](#econometric-pedagogy)

## Anaconda

  [Anaconda](https://www.anaconda.com/) is a popular python distribution which comes with many packages needed for data science along with the open-source package management system, conda. 
  
  <details>
    <summary>:bulb: Why is conda important?</summary>
    <br>
 
  The installation of Conda will allow the downloading and managment of packages through use of the command `conda`. This command will appear throughout the guide and facilitate the remainder of the set-up. 
   
  </details>
  
  #### Anaconda Installation <a name="loading-anaconda"></a>
  
  :warning: Obtain administrative rights by requesting root access:
  ```console
  $ sudo -i
  ```  
  
  To download and install [Anaconda](https://www.anaconda.com/):
  ```console
  $ wget https://repo.anaconda.com/archive/Anaconda3-2020.02-Linux-x86_64.sh
  $ bash Anaconda3-2020.02-Linux-x86_64.sh
  ```
  
  Specify the location where Anaconda should be installed. When prompted with `[/root/anaconda3] >>>`, enter path:
  ```console
  $ /usr/anaconda3
  ```
 
  Anaconda is now installed. Edit the Ubuntu system paths to include Anaconda for all users. Open the profile in [nano](https://www.nano-editor.org/):
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
    <img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/enter%20anaconda%20path.png" width = "350" height = "370" />
  </p>
  
  Use <kbd>CTRL</kbd>+<kbd>O</kbd> then <kbd>enter</kbd> to overwrite the document and <kbd>CTRL</kbd>+<kbd>X</kbd> to exit.
  <br>
  
  Refresh the paths to include Anaconda by typing:
  ```console
  $ source /etc/profile
  ```
  
  Make sure conda is up to date and update all packages to the latest version:: 
  ```console
  $ conda update -n root conda
  $ conda update --all
  ```
  
  #### JupyterHub Installation and Configuration <a name="jupyterhub"></a>
  
  Obtain administrative rights by requesting root access:
  ```console
  $ sudo -i
  ```  
  
  Install the package for [JupyterHub](https://jupyterhub.readthedocs.io/en/stable/quickstart.html)
  ```console
  $ conda install -c conda-forge jupyterhub
  ```
  
  Generate a JupyterHub configuration file in `/etc` by:
  ```console
  $ mkdir /etc/jupyterhub/
  $ cd /etc/jupyterhub/
  $ jupyterhub --generate-config
  ```
  
  Use nano to edit the newly created configuration file:
  ```console
  $ nano /etc/jupyterhub/jupyterhub_config.py
  ```
  
  Copy and paste the following into the configuration file:
  ```
  # Allow Jupyter Lab as the default interface
  c.Spawner.default_url = '/lab'
  
  # Allow admin to access other users' accounts
  c.JupyterHub.admin_access = True
  
  # Specify JupyterHub administrators
  c.Authenticator.admin_users = {'admin1'}
  
  # Shutdown user servers on logout
  c.JupyterHub.shutdown_on_logout = True
  
  # Prevent the user-owned configuration files from being loaded
  c.Spawner.disable_user_config = True
  ```
  Use <kbd>CTRL</kbd>+<kbd>O</kbd> then <kbd>enter</kbd> to overwrite the document and <kbd>CTRL</kbd>+<kbd>X</kbd> to exit.
  
  :bulb: For having access to the JupyterHub admin interface, at least _one_ JupyterHub administrator has to be specified in the configuration file. Additional JupyterHub administrators can be assigned/removed from the JupyterHub admin interface by existing administrator, e.g. `admin1`.
  
  Make JupyterHub as a system service, so that JupyterHub will run at system startup and continue to run after the system administrator logs out. To do so, create a service file:
  ```console
  $ nano /etc/jupyterhub/jupyterhub.service
  ```
  
  Copy and paste the following into the document as depicted below:
  ```
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
  
  Link the newly created service file to the `/etc/systemd/system` directory:
  ```console
  $ ln -s /etc/jupyterhub/jupyterhub.service /etc/systemd/system/jupyterhub.service
  ```

  Reload the system daemon and run JupyterHub as a system service:
  ```console
  $ systemctl daemon-reload
  $ systemctl enable jupyterhub.service
  $ systemctl start jupyterhub.service
  ```

  Check JupyterHub status (optional):
  ```console
  $ systemctl status jupyterhub.service
  ```
  
  :bulb: <b>Your JupyterHub server should be up and running at <code>http://&lt;your instance IP address&gt;:8000</code>.</b> Make sure that `:8000` is included in your address.
  
  :warning: You are running an unsecured instance of JupyterHub. For network setup and security, see [below](#github-authentication).
  
  [Back to Top](#econometric-pedagogy)
  
## R
  
  :warning: The following directions are for use on Ubuntu servers. Administrative rights are required. :warning: 
  
  #### R Installation <a name="adding-r"></a>
  
  Obtain administrative rights by requesting root access:
  ```bash
  $ sudo -i
  ```
  
  To install R version 4.0 or later on Ubuntu, add the CRAN (Comprehensive R Archive Network) repository to Ubuntu and install the R packages:
  ```console
  $ apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
  $ add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/'
  $ apt update
  $ apt install r-base r-base-dev
  ```
  
  Start R:
  ```bash
  $ R
  ```
  
  #### Update and Install IR Kernel <a name="update-and-install-r-kernel"></a>
  
  Update all packages in the current environment to the latest version, without prompts for permission:
  ```r
  update.packages(ask = FALSE)
  ```
  
  Install IRkernel for all users:
  ```r
  install.packages('IRkernel', lib = '/usr/local/lib/R/site-library')
  ```
  
  Make the IRkernel available to Jupyter. For system-wide installation, set user to False in the installspec command:
  ```r
  IRkernel::installspec(user = FALSE)
  ```

  When ready, quit:
  ```r
  q()
  ```

 <details>
  <summary>:bulb: Install tidyverse and other packages </summary>
  <br>

Additional Ubuntu linux packages are needed for 'tidyverse' in R. In Ubuntu terminal:
  ```bash
  apt install libcurl4-openssl-dev libssl-dev libxml2-dev
  ```
  
In R, install tidyverse for all users:
  ```r
  install.packages("tidyverse", dependencies = TRUE, INSTALL_opts = '--no-lock')
  ```

There are other useful R packages that one can install, for example:
  ```r
  install.packages("openxlsx", lib = '/usr/local/lib/R/site-library', dependencies = TRUE, INSTALL_opts = '--no-lock')
  install.packages("knitr", lib = '/usr/local/lib/R/site-library', dependencies = TRUE, INSTALL_opts = '--no-lock')
  ```
  
  </details>  
    
  [Back to Top](#econometric-pedagogy)

## Stata

  :bulb: Stata license is required. Instructors should contact Stata to discuss licensing options. 
  
  #### Stata Installation <a name="adding-stata"></a>
 
 Create a folder for your Stata installation file:
 ```console
 $ mkdir /home/ubuntu/stata_source
 ```
 Download the [Stata](https://www.stata.com/support/faqs/unix/install-download-on-linux/) tar file for Linux.

 Upload the tar file to the `/home/ubuntu/stata_source` folder just created (using BitVise's SFTP interface for example).

 :warning: Obtain administrative rights by requesting root access:
  ```console
  $ sudo -i
  ```

 Unzip the tar file in the `/tmp/statafiles` folder:
 ```bash
 $ cd /tmp/
 $ mkdir statafiles
 $ cd statafiles
 $ tar -zxf /home/ubuntu/stata_source/Stata16Linux64.tar.gz
 ````

 Create `/usr/local/stata16` directory for installing Stata for all users:
 ```console
 $ cd /usr/local
 $ mkdir stata16
 ```

 Install Stata. Enter licensing information when prompted:
 ```console
 $ cd /usr/local/stata16
 $ /tmp/statafiles/install
 ```
 
 After installation, you will be prompted to initialize Stata: 
 ```console
 $ ./stinit
 ```
 
 Ubuntu users will need an additional package for Stata to work:
 ```console
 $ apt install libtinfo5
  ```
 
 Edit the Ubuntu system paths to include Anaconda for all users. Open the profile in [nano](https://www.nano-editor.org/):
 ```console
 $ nano /etc/profile
 ```
 
 Type the following into the bottom of the document as depicted below.
 ```
 export PATH="/usr/local/stata16:$PATH"
 ```
 
 <p align="center">
   <img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/enter%20stata%20path.png" width = "400" height = "400" />
 </p>
 
 Use <kbd>CTRL</kbd>+<kbd>O</kbd> then <kbd>enter</kbd> to overwrite the document and <kbd>CTRL</kbd>+<kbd>X</kbd> to exit.
 
  Refresh the paths to include Anaconda by typing:
  ```console
  $ source /etc/profile
  ```
 
 #### Stata Kernel for Jupyter <a name="stata-kernel"></a>
 
 Install Stata kernel to allow Jupyter users to create and run Stata files in Jupyter Notebooks:
 ```console
 $ pip install stata_kernel
 $ python -m stata_kernel.install
 ```
 
 Ensure that the stata_kernel is installed correctly:
 ```console
 $ nano .stata_kernel.conf
 ```
 
 :warning: Make sure that `stata_path` is pointing to the correct executable. *It can be different depending on your Stata version*.
 
  <p align="center">
   <img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/stata_kernel.PNG" width = "400" height = "400" />
 </p>
 
  Copy configuration file to system configuration for all users:
 ```console
 $ cp .stata_kernel.conf /etc/stata_kernel.conf 
 ```
  
  [Back to Top](#econometric-pedagogy)

## (Optional) GitHub Extensions and Packages <a name="packages"></a>

The optional packages showcased below personalize your server to streamline online instruction. 

 <details>
    <summary>Expand</summary>
    <br>
  Contents
 
  1. [GitHub Extension](#extension)
  2. [nbgrader](#nbgrader)

  ###### GitHub Extension <a name="extension"></a>
  
  This [GitHub Extension](https://github.com/jupyterlab/jupyterlab-github) allows a GitHub icon to appear on the side bar of students' interface. When clicked, students can gain access to public repositories, such as notebook-based assignments.
  
  Install the extension for JupyterLab:
  ```console
  $ jupyter labextension install @jupyterlab/github
  ```
  
  Restart to ensure recognition of the new extension:
  ```bash
  $ systemctl restart jupyterhub.service
  ```
  
  ###### nbgrader
  
  The package [nbgrader](https://nbgrader.readthedocs.io/en/stable/) helps streamline the grading process for instructors using Jupyter notebooks. 
  
  Install the extension for JupyterLab:
  ```console
  $ conda install -c conda-forge nbgrader
  ```
  
  Restart to ensure recognition of the new extension:
  ```bash
  $ systemctl restart jupyterhub.service
  ```
  
  [Back to Top](#econometric-pedagogy)
  
 </details>
  
## (Optional) GitHub Integration <a name="github-authentication"></a>

  This section provides a guide to allowing the server to use GitHub authentication (OAuth) in the log-in process. By entering in their GitHub log-in information, students can access and use the server without the instructor having to manually enter each user and admin. As a reminder, a student can set up a GitHub account for free. An advanced understanding of the command line is recommended before attempting.

:warning: Before proceeding, setting up the site to run on HTTPS with SSL security is strongly recommended.

 <details>
    <summary>Expand</summary>
    <br>
Contents
 
1. [Generate Cookie Secret](#cookie-secret)
2. [Add a Custom Domain](#custom-url)
3. [Secure Your Lab](#secure-lab)
4. [Add GitHub Authentication](#authentication-final)

The following directions are for use in the Bitvise (or other SSH software) terminal console. Unless otherwise specified, type and run each line individually. 

 #### Generate Cookie Secret <a name="cookie-secret"></a>
Encrypt the your lab's [cookie](https://en.wikipedia.org/wiki/HTTP_cookie) for security purposes:
```console
# Create a new directory
$ mkdir /srv/jupyterhub

# Generate a random number and save it as the cookie secret
$ openssl rand -hex 32 > /srv/jupyterhub/jupyterhub_cookie_secret

$ Open JupyterHub's configuration file
$ nano /etc/jupyterhub/jupyterhub_config.py
```

Copy the following and add it to the file:
```
c.JupyterHub.cookie_secret_file = '/srv/jupyterhub/jupyterhub_cookie_secret'
```

Ensure that only the administrator can read and write the cookie secret:
```console
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

```console

# Create a key 
$ openssl dhparam -out /etc/jupyterhub/dhparam.pem 2048

# Make it so that only the administrator can edit
$ chmod 600 /etc/jupyterhub/dhparam.pem

# Link this file to the system folder
$ ln -s /etc/jupyterhub/dhparam.pem /etc/ssl/certs/dhparam.pem

```
Generate an SSL Certificate using Certbot:
```console

# Update Ubuntu and install the necessary software
$ apt-get update
$ apt-get install software-properties-common
$ add-apt-repository universe
$ apt-get update
```
Install [Certbot](https://certbot.eff.org/lets-encrypt/ubuntufocal-nginx):

```console
$ apt-get install certbot python3-certbot-nginx
```

Navigate to the AWS Console. Go to the Security Groups settings and select your instance. Edit the inbound rules. Add "HTTP" and save. 

|<img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/http_security.gif"  width="800" height="370" />|
|---|

```console
# Add this line so you do not need to shut down the server before proceeding
$ certbot certonly --nginx
```
You will be prompted to enter an email and a domain (the newly added custom domain, for example: "YOUR-DOMAIN")

You should see:
 - Congratulations! Your certificate and chain have been sav
   /etc/letsencrypt/live/YOUR-DOMAIN/fullchain.pem
   Your key file has been saved at:
   /etc/letsencrypt/live/YOUR-DOMAIN/privkey.pem

Install nginx so you do not have to type ":8000" at the end of the URL: 
```console
$ apt install nginx
```
Create a new configuration file to create the certificate on the nginx server:
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

    ssl_certificate YOUR-DOMAIN;
    ssl_certificate_key YOUR-DOMAIN;
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

Link this new configuration file:
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
$ conda install -c conda-forge oauthenticator

# Open the JupyterHub configuration file
$ nano /etc/jupyterhub/jupyterhub_config.py
```
Copy and paste the following into the file, being careful to replace the URL, Client ID, and Client Secret with your own. The Client ID and Client Secret can be found on the page of the GitHub "app" created above.

```
from oauthenticator.github import LocalGitHubOAuthenticator
c.JupyterHub.authenticator_class = LocalGitHubOAuthenticator
c.LocalGitHubOAuthenticator.oauth_callback_url = 'YOUR-URL/hub/oauth_callback'
c.LocalGitHubOAuthenticator.client_id = 'YOUR CLIENT ID'
c.LocalGitHubOAuthenticator.client_secret = 'YOUR CLIENT SECRET'

# This line means that it will no longer be necessary to manually add new users.
c.LocalGitHubOAuthenticator.create_system_users = True

c.JupyterHub.bind_url = 'http://127.0.0.1:8000'
```
It should look like this:

<p align="center">
    <img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/oath_editor.png" width = "500" height = "500" />
</p>

:warning: Notice that you may also change the admin username to your GitHub username to allow administrative access. :warning:

Reboot the server:
```console
$ systemctl restart jupyterhub.service
```
  
  [Back to Top](#econometric-pedagogy)
  
  </details>
  

## Disclaimer 

This instructional guide is part of a demonstration used for “*Econometric Pedagogy and Cloud Computing: Training the Next Generation of Economists and Data Scientists.*” There is no guarantee this methodology works for others or using a different cloud service vender. For specific needs or troubleshooting, independent research may be necessary. 

**AWS** and corresponding services are trademark of **[Amazon Web Services](https://aws.amazon.com/).**

**Stata** is trademark of **[Stata Corporation](https://www.stata.com/).**

**Google Domain** is trademark of **[Google](https://www.google.com/).**

**Python** is developed on an open source license distributed by the **[Python Software Foundation](https://www.python.org/psf/).**

**R** is offered on an open source license distributed by the **[R Foundation](https://www.r-project.org/foundation/).**

**[JupyterHub](https://jupyterhub.readthedocs.io/en/stable/)** is an open source platform developed and maintained by **[Project Jupyter](https://jupyter.org/).**


[Back to Top](#econometric-pedagogy)
  

