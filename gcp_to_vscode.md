# How to conncet gcp project to vscode
In this page I keep track of every steps should be taken in order to conncet gcp(Google Cloud Platform) to vscode(Visual Studio Code).

First of all the following page helped me to do so:
[Unleash the power of Visual Studio Code (VSCode) on Google Cloud Platform Virtual Machine](https://towardsdatascience.com/unleash-the-power-of-visual-studio-code-vscode-on-google-cloud-platform-virtual-machine-f75f78f49aee)
but I am going to customize it for myself. Since I found Linux better, I will use Linux.


## Delete a project of gcp
`gcp/IAM & Admin/manage resources` find the project and delete it.


## Pre-requisites
- Create a virtual machine by following steps explained [here](https://cloud.google.com/compute/docs/quickstart-linux).
- We need to [install](https://cloud.google.com/sdk/install) Google Cloud SDK(Software Developement Key).
- Since I am using vscode on Windows machine, from your start menu, run Windows Powershell as an admin.
- None of the stuff I commented out did not work. In order to connect to gcp from vscode, type in:
```
`gcloud compute ssh --project [PROJECT_ID] --zone [ZONE] [INSTANCE_NAME]` in Powershell.
```
- The above will create private and public keys in `.ssh` folder and set the a public key for `metadata`. I am not able to use a key for instance instead of the project.  
- To config your vscode go to `config` file in `.ssh` and set the following:
```python
Host gcp
    HostName EX IP
    IdentitiesOnly yes
    IdentityFile C:/Users/saeed/.ssh/google_compute_engine
```

<!---
- Create a new [SSH key](https://cloud.google.com/compute/docs/instances/adding-removing-ssh-keys#createsshkeys).
- Run PuTTYgen and generate a key and save them wherever you want 

I saved them but I am not seeing the public key with extension of `.pub` instead I opend the Powershell and used 

`ssh-keygen -t rsa -f [KEY_FILENAME] -C [USERNAME]` where I chose the name of the key and user name was `admin` which I had used for PuTTYgen so `ssh-keygen -t rsa -f trade -C admin`. Then keys were generated in the address where Powershell was in it. However, I relocate them to `c:\users\saeed\.ssh`. **Make sure you restart your laptop, because key is not working if you do not restart your windows machine**

- Add SSH key just to an instance not entire project following [this link](https://cloud.google.com/compute/docs/instances/adding-removing-ssh-keys#instance-only). Follow the instrunction and then open the public key with Notepad and paste it where your instructed to do so.

None of the above worked so I used the following.

Run in Windows:
gcloud compute ssh --project [PROJECT_ID] --zone [ZONE] [INSTANCE_NAME]

This should generate a private key on your machine in the ~/.ssh/ directory.

- Open vscode. Since I have already installed remote-ssh I do not need to install this extension. Press 'Ctrl+Shift+p' and type in `add a new SSH`, in the prompted window type in `ssh -i C:\\Users\\saeed\\trade admin@[External IP]` where `External IP` can be found from virtual machine instance on gcp. **However**, this will just add a new SSH key, if go to `c:\users\saeed\conig` you should change it as follows.

Then it will added but  

 --->

