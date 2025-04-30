# Use the official ASP.NET Core runtime as a base image
FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS base
WORKDIR /app
EXPOSE 80

# Use the .NET SDK image for building the application
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src
COPY ["AZ2003.csproj", "./"]
RUN dotnet restore "AZ2003.csproj"
COPY . .
WORKDIR "/src/"
RUN dotnet build "AZ2003.csproj" -c Release -o /app/build

# Publish the application
FROM build AS publish
RUN dotnet publish "AZ2003.csproj" -c Release -o /app/publish

# Use the runtime image to run the application
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AZ2003.dll"]