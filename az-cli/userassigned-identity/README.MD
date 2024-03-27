
# User assigned managed identity

```
az identity create -g identitymanagement-rg -l westeurope -n appcreator-uaid 
```

Result:
```json
{
  "clientId": "bd85c927-3d7d-475f-b9c4-54ac3c7af448",
  "id": "/subscriptions/0f9ae2bf-d8f0-4c62-b655-d635a28fca2f/resourcegroups/identitymanagement-rg/providers/Microsoft.ManagedIdentity/userAssignedIdentities/appcreator-uaid",
  "location": "westeurope",
  "name": "appcreator-uaid",
  "principalId": "75997a04-c033-4564-a127-2cd7809bea12", ==> objectid
  "resourceGroup": "identitymanagement-rg",
  "systemData": null,
  "tags": {},
  "tenantId": "d3b2b3d8-d7bc-45ef-b755-f0459c1ccd2c",
  "type": "Microsoft.ManagedIdentity/userAssignedIdentities"
}
```

# Role assignment with RestApi

Application administrator’ role=9b895d92-2cd3-44c7-9d02-a6ac2d5ea5c3

scope is missing, command doesn't word
```
az rest --method POST --uri 'https://graph.microsoft.com/beta/roleManagement/directory/roleAssignments' --body '{"principalId": "75997a04-c033-4564-a127-2cd7809bea12", "roleDefinitionId": "9b895d92-2cd3-44c7-9d02-a6ac2d5ea5c3"}'
```

# Create UAid with bicep

The bicep script create-uaid.bicep creates the uaid with bicep.

