# All-About-K8s-Practice-learning
ConfigMaps and Secrets
ConfigMaps and Secrets are essential tools in Kubernetes for managing configuration data and sensitive information, respectively. Let's explore how they work and how to use them.

ConfigMaps
ConfigMaps are used to store configuration data for your application.
They are useful when you need to provide multiple files or single files at different stages of your pods' execution.
For example, during development, you may require specific files to run the application, while during testing, different files are needed.
ConfigMaps create a virtual memory that holds the required files, which can be accessed and utilized by your application.
To create a ConfigMap as a volume:
Create a sample configuration file, e.g., sample.conf.
Run the command: kubectl create configmap mymap --from-file=sample.conf.
Verify the ConfigMap: kubectl get configmap.
Check the details of the ConfigMap: kubectl describe configmap mymap.
You can then mount the ConfigMap in your pods:
Create a YAML file, e.g., deployconfig.yml, with the necessary specifications.
Apply the YAML file: kubectl apply -f deployconfig.yml.
Check the created pods: kubectl get pods.
Access the container within the pod: kubectl exec myvolconfig -it -- /bin/bash.
Navigate to the mounted path: cd /tmp/config/.
List the files: ls.
To delete the deployment: kubectl delete -f deployconfig.yml.
ConfigMaps as Environment Variables
ConfigMaps can also be used to set environment variables.
To do this:
Create a YAML file, e.g., env.yml, specifying the necessary configurations.
Apply the YAML file: kubectl apply -f env.yml.
Check the created pods: kubectl get pods.
Access the container within the pod: kubectl exec myenvconfig -it -- /bin/bash.
View the environment variables: env.
Check the value of a specific environment variable: echo $MYENV.
To delete the deployment: kubectl delete -f env.yml.
Secrets
Secrets are used to store sensitive information such as passwords, API keys, or certificates.
They provide a secure way to handle and access sensitive data within Kubernetes.
To create a Secret:
Create the necessary files containing the sensitive information.
Run the command: kubectl create secret generic mysecret --from-file=username.txt --from-file=password.
Check the created secrets: kubectl get secrets.
View the details of a specific secret: kubectl describe secret mysecret.
To use the Secret in a pod:
Create a YAML file, e.g., depsecrets.yml, specifying the required configurations.
Apply the YAML file: kubectl apply -f depsecrets.yml.
Check the created pods: kubectl get pods.
Access the container within the pod: kubectl exec myvolsecret -it -- /bin/bash.
Navigate to the mounted path: cd tmp/mysecrets/.
List the files: ls.
View the contents of a specific file, e.g., password: cat password.
To delete the deployment: kubectl delete -f depsecrets.yml.
These examples demonstrate the practical usage of ConfigMaps and Secrets in Kubernetes. Harness the power of these tools to streamline your configuration management and protect your sensitive information effectively.
