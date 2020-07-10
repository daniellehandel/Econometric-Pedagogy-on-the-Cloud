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

  <img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/5_launch_and_key.gif"  width="800" height="370" />

  <img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/4_IP_into_bitvise.gif"  width="800" height="370" />

  <img src= "https://github.com/daniellehandel/Econometric-Pedagogy/blob/master/img/6_put in key.gif"  width="800" height="370" />
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

