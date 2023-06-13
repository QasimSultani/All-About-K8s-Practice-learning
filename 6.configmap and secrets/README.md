<h2>ConfigMap and Secrets</h2>

<p>You can understand ConfigMap as a way to manage multiple files or a single file in different stages of your pods to run the application. For example, during development, you might need specific files, and during testing, you might require different files. ConfigMap creates a virtual memory to store and support the application files defined in your YAML file.</p>

<h3>Labs</h3>

<ol>
  <li>
    <p>Create ConfigMap as a volume:</p>
    
    <pre><code># First, create a sample config file to support
nano sample.conf

# Create the ConfigMap object and attach the sample files you want
kubectl create configmap mymap --from-file=sample.conf
kubectl get configmap

kubectl describe configmap mymap   # To check details in the file
</code></pre>

    <p>Now, in the cluster, there is a node, pod, and container. Whenever a container is created, the config file will be available there.</p>
    
    <pre><code># Create deployconfig.yml
apiVersion: v1
kind: Pod
metadata:
  name: myvolconfig
spec:
  containers:
  - name: c1
    image: centos
    command: ["/bin/bash", "-c", "while true; do echo HAPPY DAY; sleep 5 ; done"]
    volumeMounts:
      - name: testconfigmap
        mountPath: "/tmp/config"   # The config files will be mounted as ReadOnly by default here
  volumes:
  - name: testconfigmap
    configMap:
       name: mymap   # This should match the config map name created in the first step
       items:
       - key: sample.conf
         path: sample.conf

kubectl apply -f deployconfig.yml
kubectl get pods
kubectl exec myvolconfig -it -- /bin/bash
cd /tmp/config/
ls

kubectl delete -f deployconfig.yml
</code></pre>
  </li>
  
  <li>
    <p>Create ConfigMap as an environment variable:</p>
    
    <pre><code># Create env.yml
apiVersion: v1
kind: Pod
metadata:
  name: myenvconfig
spec:
  containers:
  - name: c1
    image: centos
    command: ["/bin/bash", "-c", "while true; do echo Good BY; sleep 5 ; done"]
    env:
    - name: MYENV         # Env name in which the value of the key is stored
      valueFrom:
        configMapKeyRef:
          name: mymap      # Name of the config created
          key: sample.conf

kubectl apply -f env.yml
kubectl get pods
kubectl exec myenvconfig -it -- /bin/bash
env      # Type this because this time we used an environment variable
echo $MYENV    # To check output

kubectl delete -f env.yml
</code></pre>
  </li>
  
  <li>
    <p>Secrets Labs:</p>
    
    <pre><code># Create 2 files & let them be created by the Secrets object
touch username.txt password
nano username.txt
Qasim
nano password
1234

kubectl create secret generic mysecret --from-file=username.txt  --from-file=password
kubectl get secrets
kubectl describe secret mysecret    # Here you can check the files in secret but won't find the content in these files (hidden)

# Now, if you want this information in pods & containers
nano depsecret.yml
apiVersion: v1
kind: Pod
metadata:
  name: myvolsecret
spec:
  containers:
  - name: c1
    image: centos
    command: ["/bin/bash", "-c", "while true; do echo IT'S RAINING; sleep 5 ; done"]
    volumeMounts:
      - name: testsecret
        mountPath: "/tmp/mysecrets"   # The secret files will be mounted as ReadOnly by default here
  volumes:
  - name: testsecret
    secret:
       secretName: mysecret

kubectl apply -f depsecrets.yml
kubectl get pods
kubectl exec myvolsecret -it -- /bin/bash
cd tmp/mysecrets/
ls
cat password

# You can see password credentials and secret files' details in the container

</code></pre>
  </li>
</ol>
