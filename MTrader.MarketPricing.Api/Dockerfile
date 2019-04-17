FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["MTrader.MarketPricing.Api/MTrader.MarketPricing.Api.csproj", "MTrader.MarketPricing.Api/"]
RUN dotnet restore "MTrader.MarketPricing.Api/MTrader.MarketPricing.Api.csproj"
COPY . .
WORKDIR "/src/MTrader.MarketPricing.Api"
RUN dotnet build "MTrader.MarketPricing.Api.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MTrader.MarketPricing.Api.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MTrader.MarketPricing.Api.dll"]