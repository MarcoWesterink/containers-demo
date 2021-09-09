# syntax=docker/dockerfile:1
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /source

# Copy source, restore and build
COPY . .
RUN dotnet restore
RUN dotnet publish -c release -o /app --no-restore

# Run image from aspnet container
FROM mcr.microsoft.com/dotnet/aspnet:5.0
RUN apt-get update; apt-get install -y curl
WORKDIR /app
COPY --from=build /app ./
EXPOSE 8080/tcp
ENV ASPNETCORE_URLS=http://+:8080
ENV ASPNETCORE_ENVIRONMENT=Production
# RUN chmod +x ./entrypoint.sh
# CMD /bin/bash ./entrypoint.sh
ENTRYPOINT ["dotnet", "app.dll"]