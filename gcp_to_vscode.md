# How to connect gcp project to vscode

In this page I keep track of every steps should be taken in order to connect gcp(Google Cloud Platform) to vscode(Visual Studio Code).

[This page is the last page I have found](https://medium.com/@alex.burdenko/vs-code-happens-to-be-my-favorite-code-editor-and-ive-been-lucky-to-participate-so-many-diverse-952102856a7a#:~:text=Use%20CMD%2BSHIFT%2BP%20again,the%20remote%20Cloud%20Shell%20machine.) and is so useful but it did not followed it.

First of all the following page helped me to get some idea but it did not work completely:

[Unleash the power of Visual Studio Code (VSCode) on Google Cloud Platform Virtual Machine](https://towardsdatascience.com/unleash-the-power-of-visual-studio-code-vscode-on-google-cloud-platform-virtual-machine-f75f78f49aee).

However, I am going to customize it for myself. I have vscode installed on my Windows machine and want my VM machine on gcp be Linux.


## Pre-requisites
- Create a virtual machine by following steps explained [here](https://cloud.google.com/compute/docs/quickstart-linux). Do not forget to enable API by doing `API/API library/Compute Engine API`
- We need to [install](https://cloud.google.com/sdk/install) Google Cloud SDK(Software Development Key).
- From your start menu, run Windows Powershell as an admin.
- In order to connect to gcp from vscode, type in the following(None of the stuff I commented out in the text of this file did not work, I followed help of [this page](https://github.com/jonathanmiller2/picturepost-1/wiki/How-to-SSH-into-GCP-VM-from-VSCode-running-on-a-Windows-machine)):
```
`gcloud compute ssh --project [PROJECT_ID] --zone [ZONE] [INSTANCE_NAME]` in Powershell.
```
- The above will create private and public keys in `.ssh` folder and set the a public key for `metadata`. I am not able to use a key for instance instead of the project which I will add here if I was.  
- To configure your vscode go to `config` file in `.ssh` and set the following:
```python
Host gcp
    HostName EX IP
    IdentitiesOnly yes
    IdentityFile C:/Users/saeed/.ssh/google_compute_engine
```

## Delete a project of gcp
`gcp/IAM & Admin/manage resources` find the project and delete it.

## Connect vscode to GitHub
- Go to [Create an SSH key for GitHub](https://help.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#generating-a-new-ssh-key) and follow the steps in your vscode when your are SSHing to your VM on gcp. We just need do the followings in our terminal:
```
- ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
- eval $(ssh-agent -s)
- ssh-add ~/.ssh/id_rsa
```
- Go to [Add the SSH key to your GitHub account](https://help.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account) by going to ~/.ssh and copy the content of id_rsa.pub(vim) file or use the following method.

- You also can use clip < ~/.ssh/id_rsa.pub. You may need to install **geomview** package (first, sudo apt-get update -y, then sudo apt-get install -y geomview) and again try clip < ~/.ssh/id_rsa.pub.

<!---
- Create a new [SSH key](https://cloud.google.com/compute/docs/instances/adding-removing-ssh-keys#createsshkeys).
- Run PuTTYgen and generate a key and save them wherever you want 

I saved them but I am not seeing the public key with extension of `.pub` instead I opend the Powershell and used 

`ssh-keygen -t rsa -f [KEY_FILENAME] -C [USERNAME]` where I chose the name of the key and user name was `admin` which I had used for PuTTYgen so `ssh-keygen -t rsa -f trade -C admin`. Then keys were generated in the address where Powershell was in it. However, I relocate them to `c:\users\saeed\.ssh`. **Make sure you restart your laptop, because key is not working if you do not restart your windows machine**

- Add SSH key just to an instance not entire project following [this link](https://cloud.google.com/compute/docs/instances/adding-removing-ssh-keys#instance-only). Follow the instruction and then open the public key with Notepad and paste it where your instructed to do so.

None of the above worked so I used the following.

Run in Windows:
gcloud compute ssh --project [PROJECT_ID] --zone [ZONE] [INSTANCE_NAME]

This should generate a private key on your machine in the ~/.ssh/ directory.

- Open vscode. Since I have already installed remote-ssh I do not need to install this extension. Press 'Ctrl+Shift+p' and type in `add a new SSH`, in the prompted window type in `ssh -i C:\\Users\\saeed\\trade admin@[External IP]` where `External IP` can be found from virtual machine instance on gcp. **However**, this will just add a new SSH key, if go to `c:\users\saeed\conig` you should change it as follows.

Then it will added but  

 --->
