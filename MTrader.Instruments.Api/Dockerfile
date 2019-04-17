FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["MTrader.Instruments.Api/MTrader.Instruments.Api.csproj", "MTrader.Instruments.Api/"]
RUN dotnet restore "MTrader.Instruments.Api/MTrader.Instruments.Api.csproj"
COPY . .
WORKDIR "/src/MTrader.Instruments.Api"
RUN dotnet build "MTrader.Instruments.Api.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MTrader.Instruments.Api.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MTrader.Instruments.Api.dll"]