<!DOCTYPE html>
<html>
<head>
	<h1>Setting Up Kubernetes on Minikube in Linux.</h1>
	
<h2>Install Docker</h2>
<p>Run the following command to install Docker:</p>
<code>• sudo apt update &amp;&amp; apt -y install docker.io</code>

<h2>Install kubectl</h2>
<p>Run the following commands to install kubectl:</p>
<code>• curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl &amp;&amp; chmod +x ./kubectl &amp;&amp; sudo mv ./kubectl /usr/local/bin/kubectl</code>

<h2>Install Minikube</h2>
<p>Run the following commands to install Minikube:</p>
<code>• curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 &amp;&amp; chmod +x minikube &amp;&amp; sudo mv minikube /usr/local/bin/</code>

<h2>Start Minikube</h2>
<p>Run the following commands to start Minikube:</p>
•	<code>sudo apt install conntrack</code><br>
•	<code>git clone https://github.com/Mirantis/cri-dockerd.git</code><br>
• <code>mkdir bin</code><br>
• <code>wget https://storage.googleapis.com/golang/getgo/installer_linux</code><br>
• <code>chmod +x ./installer_linux</code><br>
• <code>./installer_linux</code><br>
• <code>source ~/.bash_profile</code><br>
• <code>cd cri-dockerd</code><br>
• <code>mkdir bin</code><br>
• <code>go build -o bin/cri-dockerd</code><br>
• <code>mkdir -p /usr/local/bin</code><br>
• <code>install -o root -g root -m 0755 bin/cri-dockerd /usr/local/bin/cri-dockerd</code><br>
• <code>cp -a packaging/systemd/* /etc/systemd/system</code><br>
• <code>sed -i -e 's,/usr/bin/cri-dockerd,/usr/local/bin/cri-dockerd,' /etc/systemd/system/cri-docker.service</code><br>
• <code>systemctl daemon-reload</code><br>
• <code>systemctl enable cri-docker.service</code><br>
• <code>systemctl enable --now cri-docker.socket</code><br>
• <code>minikube start --vm-driver=none
  
  
  
<h2>//If getting Cri-tool error</h2>
• <code>wget https://github.com/kubernetes-sigs/cri-tools/releases/download/v1.25.0/crictl-v1.25.0-linux-amd64.tar.gz</code><br>
• <code>sudo tar zxvf crictl-v1.25.0-linux-amd64.tar.gz -C /usr/local/bin</code><br>
• <code>minikube status</code><br>

<h2>Here is link of my profile if you face any problem DM here!!</h2>
https://www.linkedin.com/in/muhammad-qasim-sultani/
