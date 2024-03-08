
# Get Token for database

## Login to azure

```
az login
```

## Check endpoints for public cloud

```
az cloud show
```

## Get Token for Resourcetype Database
Resourcetype: oss-rdbms
```
az account get-access-token --resource https://ossrdbms-aad.database.windows.net
az account get-access-token --resource-type oss-rdbms
```
### Result

```
{
  "accessToken": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6IlhSdmtvOFA3QTNVYVdTblU3Yk05blQwTWpoQSIsImtpZCI6IlhSdmtvOFA3QTNVYVdTblU3Yk05blQwTWpoQSJ9.eyJhdWQiOiJodHRwczovL29zc3JkYm1zLWFhZC5kYXRhYmFzZS53aW5kb3dzLm5ldCIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0Lzk3MTU0MGMyLTI4MTctNDI3Zi1hOTM2LWY3YmE0NWIzNDQwNi8iLCJpYXQiOjE3MDk4ODUxMDMsIm5iZiI6MTcwOTg4NTEwMywiZXhwIjoxNzA5ODg5NDYzLCJhY3IiOiIxIiwiYWlvIjoiQVlRQWUvOFdBQUFBSUxEUEZ0SFJ6T0FOOWtzbEpUL2JzNXlQSjVXMTZuTDU5S0dJNzlXOUxHcTlRcFgrb0wxUnFiWGpxM3QyM2RYN0w2eGRML29qVDlLR2EycGo0TUd1R05jNXVEN1krb2JWa0tFQTR1ckMyaFdtZk9JL3lCTUJNWGpxclJpSW02eUpIWDQwUnNPZk85VFNKYjdTYmFRaUhjbFJyeWxsWVZJMlE5ZDNyY0c4R0lFPSIsImFsdHNlY2lkIjoiMTpsaXZlLmNvbTowMDAzQkZGRENCMkVGQ0NGIiwiYW1yIjpbInB3ZCIsIm1mYSJdLCJhcHBpZCI6IjA0YjA3Nzk1LThkZGItNDYxYS1iYmVlLTAyZjllMWJmN2I0NiIsImFwcGlkYWNyIjoiMCIsImVtYWlsIjoicmF5X2J1cmtzQG91dGxvb2suY29tIiwiZmFtaWx5X25hbWUiOiJCdXJrcyIsImdpdmVuX25hbWUiOiJSYXkiLCJpZHAiOiJsaXZlLmNvbSIsImlwYWRkciI6IjJhMDI6ODA3MToyMTgzOmQ3MjA6NzA0OTozNTgxOmZkYTk6YTU2NCIsIm5hbWUiOiJSYXkgQnVya3MiLCJvaWQiOiIwZDM1ZGVhOS01OTVhLTRjYmEtOWI5Mi1iMGVlMjZiNTIyNzEiLCJwdWlkIjoiMTAwMzIwMDM1ODM5NjFDRiIsInJoIjoiMC5BVXNBd2tBVmx4Y29mMEtwTnZlNlJiTkVCbERZUEJMZjJiMUFsTlhKOEh0X29nTVpBUkEuIiwic2NwIjoidXNlcl9pbXBlcnNvbmF0aW9uIiwic3ViIjoiQ3NlOXlfWmpUZHFRQktZX3FhMk1WSjF6Zy1xTTIzeHQ0V1NTenBiamVKSSIsInRpZCI6Ijk3MTU0MGMyLTI4MTctNDI3Zi1hOTM2LWY3YmE0NWIzNDQwNiIsInVuaXF1ZV9uYW1lIjoibGl2ZS5jb20jcmF5X2J1cmtzQG91dGxvb2suY29tIiwidXRpIjoiVmpBRUswMXdOa1d5NGE0VTdLRmNBQSIsInZlciI6IjEuMCJ9.Xsx5zDT4WyZ6I1yz1uzIbWVo1SwI-zJxXJ71X58n8yA4nv-enYMEbnm6XqvHvxrkauJA6ANsBnWlsQEv6JOnXb7LZfv5sWZ-6wL7_ZI4M9H4_FqlFHcztmJpzjgjmDRYtSbJKBrHwZ7WCG50FidbiE5v3VEY6eQ71BhSijxbnlD897TNJ0iWfDnOXn-sgEACUsuyMzj3CuX5n4KjhXaMUGHBMp9890zeMbBuREjezGaveAGvDJjGxU04Wc9qj2YFwMYkSpmWwB05DDbC1JxcqwoOjc6i-8DTtSznsUkpBo88Ep1K3TpZPT-8Yc6JuCZ1H_-d6.......",    
  "expiresOn": "2024-03-08 10:17:42.000000",
  "subscription": "<SubscriptionId>",
  "tenant": "<tenantId>",
  "tokenType": "Bearer"
}
```

### Bearer Payload

check with https://jwt.io

```json
{
  "aud": "https://ossrdbms-aad.database.windows.net",
  "iss": "https://sts.windows.net/<tenantid>/",
  "iat": 1709885103,
  "nbf": 1709885103,
  "exp": 1709889463,
  "acr": "1",
  "aio": "AYQAe/8WAAAAILDPFtHRzOAN9kslJT/bs5yPJ5W16nL59KGI79W9LGq9QpX+oL1RqbXjq3t23dX7L6xdL/ojT9KGa2pj4MGuGNc5uD7Y+obVkKEA4urC2hWmfOI/yBMBMXjqrRiIm6yJHX40RsOfO9TSJb7SbaQiHclRryllYVI2Q9d3rcG8GIE=",
  "altsecid": "1:live.com:0003BFFDCB2EFCCF",
  "amr": [
    "pwd",
    "mfa"
  ],
  "appid": "04b07795-8ddb-461a-bbee-02f9e1bf7b46",
  "appidacr": "0",
  "email": "ray_burks@outlook.com",
  "family_name": "Burks",
  "given_name": "Ray",
  "idp": "live.com",
  "ipaddr": "2a02:8071:2183:d720:7049:3581:fda9:a564",
  "name": "Ray Burks",
  "oid": "0d35dea9-595a-4cba-9b92-b0ee26b52271",
  "puid": "10032003583961CF",
  "rh": "0.AUsAwkAVlxcof0KpNve6RbNEBlDYPBLf2b1AlNXJ8Ht_ogMZARA.",
  "scp": "user_impersonation",
  "sub": "Cse9y_ZjTdqQBKY_qa2MVJ1zg-qM23xt4WSSzpbjeJI",
  "tid": "971540c2-2817-427f-a936-f7ba45b34406",
  "unique_name": "live.com#ray_burks@outlook.com",
  "uti": "VjAEK01wNkWy4a4U7KFcAA",
  "ver": "1.0"
}
```

# Access to psql

export PGPASSWORD=<copy/pasted TOKEN value from step 2>
psql "host=<mydbhost>.postgres.database.azure.com user=user@tenant.onmicrosoft.com@mydb dbname=postgres sslmode=require"

