I want to create an API and deploy it via Docker container. Let's do it:
  
## Publishing our app

Create your ASP.NET Core project, in my case I need to use an API and I created it using JetBranins IDE in my Ubuntu Linux desktop. Once created is necessary to publish the project in the project path:

> **Note:** Is important to be in the **project path** because that's what we want to deploy.

``` csharp
dotnet publish -o ./publish
```

## Prepare our project to work with Docker
Create the Dockerfile, a basic example:

```
FROM microsoft/dotnet:sdk AS build-env
WORKDIR /ElectricCities.Users-Api

COPY ./ElectricCities.Users-Api/publish .

ENTRYPOINT ["dotnet", "ElectricCities.Users-Api.dll"]
```

Is important to create the Docker Ignore file to avoid use unnecessary files:

``` csharp
bin\
obj\
```

## Creating the ASP.NET Core image
Then, we're going to create the docker image:

``` csharp
sudo docker build -t electriccities.users-api .
```

Let's see if the image has been created:

sudo docker images

## Running our app

And let's see if the image runs correctly

``` csharp
sudo docker run -d -p 5002:80 electriccities.users-api
```

We can verify if it's running:

``` csharp
sudo docker ps
```

And we can navigate with our browser