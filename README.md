**Install Kubernetes with AWS Cloud Provider**

Terrafrom code to create infrastructure from the below link

https://github.com/yasapurnama/Install-Kubernetes-with-AWS-Cloud-Provider

**This will create Master and Worker Nodes:**
-Setup Kubernetes:
To Run on Master and Worker Nodes:
TOKEN=`curl -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600"`

hostnamectl set-hostname $(curl -s http://169.254.169.254/latest/meta-data/local-hostname -H "X-aws-ec2-metadata-token: $TOKEN")

bash ./container.sh
bash ./kube.sh
