Create Linux App service plan:

az appservice plan create -g <resource group> -n simpleazlinuxappserviceplan --sku free --is-linux

Create webapp with container image:

az webapp create -g <resource group> -n azsimplewebapp2 -p simpleazlinuxappserviceplan -i mcr.microsoft.com/azuredocs/aci-helloworld:latest

Delete webapp -- this also deleted the appservice plan why?

az webapp delete -n azsimplewebapp2 -g <resource group>
