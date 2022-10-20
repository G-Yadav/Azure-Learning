Get List of runtimes

az functionapp list-runtimes

App service plan should be atleast B1, free tier doesn't work with azure function

az appservice plan create -g 1-68c7e18e-playground-sandbox -n simpleazlinuxappserviceplan --sku B1 --is-linux

Create a function 

az functionapp create -g 1-68c7e18e-playground-sandbox -n simpleazfunctionapp -s simpleazstorageaccount20 -p simpleazlinuxappserviceplan --runtime dotnet --https-only