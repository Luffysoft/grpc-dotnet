FROM mcr.microsoft.com/dotnet/core/sdk:3.1.201 AS build-env
WORKDIR /app

# Copy everything
COPY . ./
RUN dotnet restore testassets/InteropTestsWebsite
RUN dotnet publish testassets/InteropTestsWebsite -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "InteropTestsWebsite.dll", "--port_http1", "80"]