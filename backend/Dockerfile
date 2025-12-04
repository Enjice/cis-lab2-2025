ARG SDK_VERSION=8.0
ARG ASPNET_VERSION=8.0

FROM mcr.microsoft.com/dotnet/sdk:${SDK_VERSION} AS build-stage

WORKDIR /src

COPY Backend.csproj ./

RUN dotnet restore

COPY . .

RUN dotnet build -c Release -o /app/build

RUN dotnet publish -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:${ASPNET_VERSION} AS production-stage

WORKDIR /app

COPY --from=build-stage /app/publish .

ENTRYPOINT ["dotnet", "Backend.dll"]