How to SSH into GCP VM from VSCode running on a Windows machine

You will need the Google Cloud SDK on your local machine, specifically the <code>gcloud</code> command.<br>
You can get it here: <a href="https://cloud.google.com/sdk/docs/quickstart-windows" rel="nofollow">https://cloud.google.com/sdk/docs/quickstart-windows</a><br>
You will also need Putty/PuttyGen<br>
<a href="https://www.puttygen.com/" rel="nofollow">https://www.puttygen.com/</a><br>
<a href="https://www.putty.org/" rel="nofollow">https://www.putty.org/</a><br>
You'll also need the Remote-SSH plugin on VSCode</p>
<p><a href="https://cloud.google.com/compute/docs/instances/connecting-to-instance#store-host-key" rel="nofollow">https://cloud.google.com/compute/docs/instances/connecting-to-instance#store-host-key</a></p>
<p>Run in Google Cloud Console:<br>
<code>gcloud components update</code><br>
<code>gcloud compute instances add-metadata [INSTANCE_NAME] --metadata enable-guest-attributes=TRUE</code></p>
<p>Run in Windows:<br>
<code>gcloud compute ssh --project [PROJECT_ID] --zone [ZONE] [INSTANCE_NAME]</code></p>
<p>This should generate a private key on your machine in the ~/.ssh/ directory.</p>
<p>Open up PuttyGen and click Load<br>
Find the PuTTY Private Key that the gcloud command generated. For me it was ~\.ssh\google_compute_engine.ppk.<br>
Go to Conversions -&gt; Export OpenSSH key. Name it whatever you want (no file extension).</p>
<p>In VSCode, use f1 -&gt; Remote-SSH: Connect to Host -&gt; Add New SSH Host...<br>
Type in <code>ssh -v -i [PATH_TO_OPENSSH_KEY] [USERNAME]@[HOST]</code></p>
<p>Host should be the external IP of the VM, and your username should be the user of your computer.</p>
<p>Use <code>sudo -i</code> to become root</p>
<p>Trying this tomorrow: <a href="https://cloud.google.com/compute/docs/instances/connecting-advanced#root" rel="nofollow">https://cloud.google.com/compute/docs/instances/connecting-advanced#root</a>
