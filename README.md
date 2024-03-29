# slurm-cresset-v2

This demo terraform scipt will setup and configure an HPC Slurm + Cresset Flare environment for testing and evaluation. It is intended to be deployed to a sandbox environment.    

From Cloud Shell:

```git clone https://github.com/vjb-collab/slurm-cresset-v2.git```

```cd slurm-cresset-v2/tf/examples/basic/```

```terraform init```

Before deploying the cluster, you can modify the deloyment configuration by modifying values in the *basic.tfvars* file. 

Then deploy the cluster

 ```make apply```
 
 While the cluster is deploying, you will see this message on the controller node when you ssh into it:
 
 *** *Slurm & Flare are currently being configured in the background* ***
 
 If you stay logged into the controller during the deployment, you will see a broadcast message when's it's completed like this: 
 
 *** *Slurm controller & Flare setup complete* ***
 
 _Note: If you ssh into the controller and you do not see the message (i.e., you just see the Slurm and Flare logos), then the installation has completed._
 
 After the cluster has been setup and configured, put the license in place:  
 
 ```gcloud compute scp  <LICENSEFILE>  cresset-flare-controller:~/. --zone=<zone>```
 
 The rest of the configuration takes place on the _controller_ node. On the controller node:
 
 ```sudo mv <LICENSEFILE> /apps/cresset/licenses/.```
 
 ``` cd /apps/ ```
 
 ```sudo chown -R $USER cresset/```
 
 ```sudo chgrp -R $USER cresset/```
 
 ```cd cresset```
 
 ```./start-CEBroker.sh```
 
 ```tail -f cebroker2.log```
 
