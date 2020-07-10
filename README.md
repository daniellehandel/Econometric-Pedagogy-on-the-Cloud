# Econometric-Pedagogy
 Econometric Pedagogy and Cloud Computing: Training the Next Generation of Economists and Data Scientists
 
 Authors: Danielle V. Handel, Anson T. Y. Ho, Kim P. Huynh, David T. Jacho-Chávez, Carson H. Rea

## Launching an instance
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
    
    Change the storage from the default to the maximum the free tier provides, 30 GiB. Continue to “Next: Add Tags”.

    Tags are an optional feature to allow for categorization and organization. Continue to "Next: Configure Security Groups".

    The SSH rule there by default will have the standard Port Range of 22 and a “Custom” source. Change the source to “Anywhere” Add a second custom TCP security rule by clicking the “Add Rule” button. Modify the rule to have a port range of 8000; notice the source change to “Custom” from “Anywhere”. Add a description of “JupyterHub”. Continue to the final stage by clicking the blue “Review and Launch” button. 

    Given all steps have been followed by this point, select “Launch”.


  <img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/5_launch_and_key.gif"  width="800" height="370" />
    
    Selecting “Launch” will prompt the user to select an existing key pair or create a new one. A key pair serves as a sort of password to connect the instance to a SSH server or client. Name and download your key pair. 

:warning: Do not lose the key, or all progress will be lost. Keep track of where the key is stored, as it will need to be accessed later.


  <img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/4_IP_into_bitvise.gif"  width="800" height="370" />
    
    The instance should now be visible in the EC2 homepage. Located towards the bottom of the screen, the description of the instance should be visible. Download and open Bitvise as an SSH client. Copy the IPv4 Public IP address and paste it into “Host” on Bitvise. Insert 22 as the port. 

:bulb: MacOS users may choose to use the Terminus App off of the AppStore in lieu of Bitvise.


  <img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/6_put in key.gif"  width="800" height="370" />
    
    The proper username to connect Bitvise to the instance is “ubuntu”. Change the following line “Initial method” to Publickey. Select the proper key in from the newly created “client key” line. Click log in to selct the key downloaded earlier. An optional comment can be left for organization purposes if desired.

The instance is now launched and hosted on a client. 
Continue reading the “Anaconda” section to download the distribution onto the newly created instance. 

  master
  
</details>

## Ananconda
<details>
  <summary>Click to expand</summary>
  
  ###### Loading Anaconda
  
  The following directions are for use in the Bitvise (or other choise SSH software) terminal:
  
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
  enter `/usr/anaconda3`
  
  Refresh:
  ```console
  ubuntu@ip-xx-xxx:~$ source .bashrc
  ```
  Open a text editor (nano is used here):
  
  ```console
  ubuntu@ip-xx-xxx:~$ nano /etc/profile
  ```
 
</details>

## R
<details>
  <summary>Click to expand</summary>
  
  ###### Adding R 
  
 
</details>

## Stata
<details>
  <summary>Click to expand</summary>
  
  ###### Adding Stata

</details>

