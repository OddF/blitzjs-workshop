# Create a Postgre SQL resource

## Resource group

First we need a resource group to place the database in. Use an existing resource group or create a new one.
To create a new resource group use the UI in azure portal, or simply run this command `New-AzResourceGroup -name dotjs-leaderboard -Location 'North Europe'` from the CLI

## Database

Now that we got our resource group in place we can create our database. Use the UI to create an `Azure Database for PostgreSQL server`
Optionally you can use the following commands:
- `Install-Module -Name Az.PostgreSql`
- `Register-AzResourceProvider -ProviderNamespace Microsoft.DBforPostgreSQL`
- `$Password = Read-Host -Prompt 'Please enter your password' -AsSecureString`
- `New-AzPostgreSqlServer -Name <YourInitials>WorkshopSql -ResourceGroup dotjs-leaderboard -Sku B_Gen5_1 -Location 'North Europe' -AdministratorUsername <USERNAME> -AdministratorLoginPassword $Password`

PSA: Take note of the password provided, it will be used later.

When the database becomes available open it in the Azure portal, change `Allow access to Azure services` to `Yes` and press the `Add client IP` form the top before hitting `save`

## Updating the code

Now that we have changed to use PostgreSQL we need to update `db/schema.prisma` file.

The first lines should look like this.

```javascript
datasource db {
  provider = "postgres"
  url      = env("DATABASE_URL")
}

generator client {
  provider = "prisma-client-js"
}
```

To get this working on your local machine you will need to change the connection string in `.env.local` to point to the Azure PostgreSQL resource, or install PostgreSQL locally and use this.