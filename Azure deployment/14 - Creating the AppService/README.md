# Creating the WebApp

Now we need to create the Azure App service to host the container. 
We will use the UI to create the service as it's a bit easier to follow what is happening.

1. From the left menu in the Azure Portal press `Create a resource`
2. WebApp should be under the popular pane, if not just search functionality
3. Select desired resource group and name. As for the rest use:
    - Publish - Docker Container
    - Operating system - Linux
    - Region - 'North Europe' = only one I've verified that the rest of this workshop works on.
    - App Service Plan - Create a new one, change size to B1 to reduce billing.
4. We don't need to change anything else for this workshop. Press `Review + create` and confirm.