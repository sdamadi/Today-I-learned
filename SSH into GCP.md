# How to SSH into GCP VM from VSCode running on a Windows machine

Create a virtual machine by following steps explained [here](https://cloud.google.com/compute/docs/quickstart-linux). Do not forget to enable API by doing `API/API library/Compute Engine API`

You will need the Google Cloud SDK on your local machine, specifically the <code>gcloud</code> command.<br>

You can get it here: <a href="https://cloud.google.com/sdk/docs/quickstart-windows" rel="nofollow">https://cloud.google.com/sdk/docs/quickstart-windows</a><br>

You will also need Putty/PuttyGen<br>

<a href="https://www.puttygen.com/" rel="nofollow">https://www.puttygen.com/</a><br>

<a href="https://www.putty.org/" rel="nofollow">https://www.putty.org/</a><br>

You'll also need the Remote-SSH plugin on VSCode
<a href="https://cloud.google.com/compute/docs/instances/connecting-to-instance#store-host-key" rel="nofollow">https://cloud.google.com/compute/docs/instances/connecting-to-instance#store-host-key</a>

Run in Google Cloud Console:<br>

<code>gcloud components update</code><br>

<code>gcloud compute instances add-metadata [INSTANCE_NAME] --metadata enable-guest-attributes=TRUE</code>(I did not use this line.)

From your start menu, run Windows Powershell as an admin.

Run in Windows:<br>

<code>gcloud compute ssh --project [PROJECT_ID] --zone [ZONE] [INSTANCE_NAME]</code>

This should generate a private key on your machine in the ~/.ssh/ directory.

Open up **PuttyGen** and click Load to load the private key. To find the PuTTY Private Key that the gcloud command generated you should go to `~\.ssh\google_compute_engine.ppk`.

Once you load your private key, go to Conversions -&gt; Export OpenSSH key and ame it whatever you want (no file extension).

In VSCode, use f1 -&gt; Remote-SSH: Connect to Host -&gt; Add New SSH Host....

Type in <code>ssh -v -i [PATH_TO_OPENSSH_KEY] [USERNAME]@[HOST]</code>

Host should be the external IP of the VM, and your username should be the user of your computer.

After doing the above you can change the name of host from IP to a name you would like.

I do not know what are the following two lines of explanations.

Use <code>sudo -i</code> to become root

Trying this tomorrow: <a href="https://cloud.google.com/compute/docs/instances/connecting-advanced#root" 


The above will create private and public keys in `.ssh` folder and set the a public key for `metadata`. I am not able to use a key for instance instead of the project which I will add here if I was.  
- To configure your vscode go to `config` file in `.ssh` and set the following:
```python
Host gcp
    HostName EX IP
    IdentitiesOnly yes
    IdentityFile C:/Users/saeed/.ssh/google_compute_engine
```
