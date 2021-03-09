# Azure Container registry

Azure container registry is a place to keep your containers, we will use this as part of our pipeline later.
For now we need to create it and push a placeholder image.

## Create the registry

You can either create the registry in the Azure Portal or use the following command:
`New-AzContainerRegistry -ResourceGroupName dotjs-leaderboard -Name <your-initials>containers -Location 'North Europe' -Sku Basic -EnableAdmin`

## Pushing the placeholder image

You will need to have docker installed on your computer to push the image. If you don't have docker, you can use `https://labs.play-with-docker.com/` at your own risk - change password or delete resource after workshop

Now run the following commands:
- `docker login <oddfcontainers>.azurecr.io`
    signs you into your newly created registry, username and password is show under `Access keys`
- `docker run -it hello-world`
    Pulls down the hello-world image and verifies your environment
- `docker tag hello-world <oddfcontainers>.azurecr.io/workshop/dotjs-leaderboard`
    Applies a tag to the image
- `docker push <oddfcontainers>.azurecr.io/workshop/dotjs-leaderboard`
    Pushes the hello-world image to a new repository within your registry