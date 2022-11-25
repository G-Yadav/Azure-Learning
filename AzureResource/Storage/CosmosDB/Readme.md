Connection String for Azure Cosmos DB

Can be found under keys




-------------to be placed laterr

$resourceGroup = az group list --query '[0].name' --output json
 
 $location = az resource list --query '[0].location'
 
 $namespace = az eventhubs namespace list --resource-group $resourceGroup --query '[0].name' --output json 
 
 $hubId = az eventhubs eventhub list --resource-group $resourceGroup --namespace-name $namespace --query '[0].id' --output json
#create event grid topic and subscription

$topicname = “topic-09152020”

az eventgrid topic create --name $topicname -l $location -g $resourceGroup

$topicId = az eventgrid topic list --query ‘[0].id’ --output json

$ehSubName = “es09152020”

az eventgrid event-subscription create --name $ehSubName --source-resource-id $topicId --endpoint $hubId --endpoint-type eventhub

$eventID = Get-Random 99999

$eventDate = Get-Date -Format s

$htbody = @{
 id= $eventID
 eventType="recordInserted"
 subject="myapp/guitars/gibson"
 eventTime= $eventDate
 data= @{
 make="Gibson"
 model="Les Paul"
 }
 dataVersion="1.0"
}

$body = "["+(ConvertTo-Json $htbody)+"]"

$endpoint = az eventgrid topic list --resource-group $resourceGroup --query '[0].endpoint' --output tsv

$key = az eventgrid topic key list --name $topicname -g $resourceGroup --query "key1" --output tsv

Invoke-WebRequest -Uri $endpoint -Method POST -Body $body -Headers @{"aeg-sas-key" = $key}

Invoke-WebRequest -Uri $endpoint -Method POST -Body $body -Headers @{"aeg-sas-key" = $key}
