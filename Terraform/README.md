### Download Terraform binary for Linux (64-bit):

curl -LO https://releases.hashicorp.com/terraform/1.0.8/terraform_1.0.8_linux_amd64.zip

### Unzip the downloaded Terraform binary:

unzip terraform_1.0.8_linux_amd64.zip

### Create the directory where you'll store the Terraform binary:

mkdir -p ~/.local/bin

### Move the Terraform binary to the newly created directory:

mv terraform ~/.local/bin/

### Add Terraform to your PATH by appending it to the .bashrc file:

echo 'export PATH=$HOME/.local/bin:$PATH' >> ~/.bashrc

### Source the .bashrc file to apply the changes immediately:

source ~/.bashrc

### Verify the Terraform installation by checking the version:

terraform --version
