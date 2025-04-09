**Install Kubernetes with AWS Cloud Provider**

Terrafrom code to create infrastructure from the below link

https://github.com/yasapurnama/Install-Kubernetes-with-AWS-Cloud-Provider

**This will create Master and Worker Nodes:**
-Setup Kubernetes:
To Run on Master and Worker Nodes:
1.    TOKEN=`curl -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600"`

2.    hostnamectl set-hostname $(curl -s http://169.254.169.254/latest/meta-data/local-hostname -H "X-aws-ec2-metadata-token: $TOKEN")

3.     Save the below files and run

        bash ./container.sh

5.      bash ./kube.sh

6.  Save the file aws.yml in /etc/kubernetes/aws.yml

    vi /etc/kubernetes/aws.yml 

**init cluster**
6.  kubeadm init --config /etc/kubernetes/aws.yml

**Join Command from the above command and keep it**

7.
    mkdir -p $HOME/.kube
    sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
    sudo chown $(id -u):$(id -g) $HOME/.kube/config
    export KUBECONFIG=/etc/kubernetes/admin.conf
    kubectl apply -k 'github.com/kubernetes/cloud-provider-aws/examples/existing-cluster/base/?ref=master'
    kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml

**Only on Worker**

**Do not run this: just take IP, token, and hash value for the next command**
    kubeadm join 10.0.0.18:6443 --token a7bnl2.jubi0wib4slhx0cg \
        --discovery-token-ca-cert-hash sha256:902124cebdcf5d44bfc8891df0eb92033fa3ff93554a1788d9eb4423bbd
**Get IP from Worker node**
    hostnme -f 

**Add the token, hash, IP, host name to command and Run**

cat << EOF > /etc/kubernetes/node.yml
---
apiVersion: kubeadm.k8s.io/v1beta3
kind: JoinConfiguration
discovery:
  bootstrapToken:
    token: "0b54mt.2994qtdu36bxdxxe" #token value from kubeadm join command
    apiServerEndpoint: "10.0.0.18:6443" #IP EP value from kubeadm join command
    caCertHashes:
      - "sha256:ca25d924f8e55b447b1431ce45e66cf592cf384fae5ab810c1aa9b3ed064e569" #hash value from kubeadm join command
nodeRegistration:
  name: ip-10-0-0-76.ec2.internal  #worker node IP
  kubeletExtraArgs:
    cloud-provider: external
EOF

**Run this**
  kubeadm join --config /etc/kubernetes/node.yml

#Kubernetes cluster setup ends here
