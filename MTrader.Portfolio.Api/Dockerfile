FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["MTrader.Portfolio.Api/MTrader.Portfolio.Api.csproj", "MTrader.Portfolio.Api/"]
RUN dotnet restore "MTrader.Portfolio.Api/MTrader.Portfolio.Api.csproj"
COPY . .
WORKDIR "/src/MTrader.Portfolio.Api"
RUN dotnet build "MTrader.Portfolio.Api.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MTrader.Portfolio.Api.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MTrader.Portfolio.Api.dll"]