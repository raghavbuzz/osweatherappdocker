# Get Base Image (Full .NET Core SDK)
#FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build-env
FROM microsoft/aspnetcore-build:2.0.0 AS build-env
WORKDIR /app

# Copy csproj and restore
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# Generate runtime image
FROM microsoft/aspnetcore-build:2.0.0
WORKDIR /app
EXPOSE 80
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "weather-app.dll"]
