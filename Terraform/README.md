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


#### Get list of publishers for a specific location (eastus2):

az vm image list-publishers --location eastus2 --output table

#### Get list of offers for required publishers (Canonical):

az vm image list-offers --location eastus2 --publisher Canonical --output table

#### Get list of skus for required publisher and offer:

az vm image list-skus --location eastus2 --publisher Canonical --offer 0001-com-ubuntu-server-focal --output table

#### Get image details for required publisher, offer and sku:

az vm image list --location eastus2 --publisher Canonical --offer 0001-com-ubuntu-server-focal --sku 20_04-lts-arm64 --all --output table