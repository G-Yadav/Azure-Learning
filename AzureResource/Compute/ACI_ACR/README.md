Create azure container with image

az container create -g 1-3a80efea-playground-sandbox -n simpleazcontainer --image mcr.microsoft.com/azuredocs/aci-helloworld:latest --ports 80 443 --dns-name-label az-land

simpleazregistry.azurecr.io

Create Azrue container registry

az acr create -g 1-3a80efea-playground-sandbox -n simpleazregistry --sku Basic

Login into acr using admin credential from azure registry access keys section

az acr login -n simpleazregistry

Pull image or create from dockerfile

sudo docker pull mcr.microsoft.com/azuredocs/aci-helloworld

Create a tag for image 

docker tag mcr.microsoft.com/azuredocs/aci-helloworld:latest simpleazregistry.azurecr.io/aci-helloworld:v1 -- didn't work

sudo docker tag mcr.microsoft.com/azuredocs/aci-helloworld simpleazregistry.azurecr.io/hello-world:v1

Push image to registry 

sudo docker push simpleazregistry.azurecr.io/hello-world:v1

