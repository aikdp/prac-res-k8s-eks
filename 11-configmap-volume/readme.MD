# ConfigMap: Updating file with configmap
* For example in our expense project, we have environment variable DB_HOST value might changed or nginx.conf file need to update.
* We should rebuild the dockerfile again. and It is not good practice to do such things.
* We can make use of ConfigMap with volume mounts. See the example for manifest yaml file. Change the conf file with upadtes info or configs and delete the pods. 
* You will get updated configs without going for rebuild.
