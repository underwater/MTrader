FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["MTrader.TradeBook.Api/MTrader.TradeBook.Api.csproj", "MTrader.TradeBook.Api/"]
RUN dotnet restore "MTrader.TradeBook.Api/MTrader.TradeBook.Api.csproj"
COPY . .
WORKDIR "/src/MTrader.TradeBook.Api"
RUN dotnet build "MTrader.TradeBook.Api.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MTrader.TradeBook.Api.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MTrader.TradeBook.Api.dll"]