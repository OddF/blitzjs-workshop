# Configuring the AppService

Before we can run our blitz app on the app service we need to configure the database connection and a client secret.

Navigate to the configuration pane for the app service.

We will add the DATABASE_URL first.
the format of the url is `postgres://<Username>:<Password from section 12>@<hostname>:<port>/<database>`
It should look something like this: `postgres://oddf@dotjsleaderboard-sql:**********@dotjsleaderboard-sql.postgres.database.azure.com:5432/postgre`

When running blitz in production a SESSION_SECRET_KEY is required.
Use a guid like this: 0f37f091-3ed1-4e4c-85bb-546876ab43d8

Finally we need to allow our app some more time to start up than the default value, since we will be doing database migration as part of startup.
Set WEBSITES_CONTAINER_START_TIME_LIMIT to 600