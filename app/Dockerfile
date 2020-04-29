FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build-env
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY src/ /app
RUN ls -la
RUN dotnet restore

# Copy everything else and build
RUN dotnet publish -c Release -o /publish

# Build runtime image
FROM mcr.microsoft.com/dotnet/core/sdk:3.1
WORKDIR /app
COPY --from=build-env /publish .
RUN ls -la
EXPOSE 80
ENV ASPNETCORE_URLS=http://+:5000


ENTRYPOINT ["dotnet", "/app/app.dll"]
