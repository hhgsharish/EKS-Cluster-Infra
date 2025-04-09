#**Terraform installation steps -Windows:**

#Launch windows powershell in administrator mode

#nstall chocolaty if it does not exists.

1.
Set-ExecutionPolicy Bypass -Scope Process -Force; `
[System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; `
iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

2.
choco install terraform -y

Open Visual Studio and install terraform official plugin:

![image](https://github.com/user-attachments/assets/a55b485b-c86d-4e64-8bab-6d0491fdaf35)


create a directory for Terraform and create main.tf file there:

Terraform Commands:

terraform init - Initializes the Terraform working directory by downloading required provider plugins.

terraform plan - Shows the changes Terraform will make before applying them.

terraform apply - Creates or updates infrastructure based on the Terraform configuration.

terraform destroy - Deletes all resources defined in the Terraform configuration.
