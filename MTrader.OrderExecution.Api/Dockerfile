FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["MTrader.OrderExecution.Api/MTrader.OrderExecution.Api.csproj", "MTrader.OrderExecution.Api/"]
RUN dotnet restore "MTrader.OrderExecution.Api/MTrader.OrderExecution.Api.csproj"
COPY . .
WORKDIR "/src/MTrader.OrderExecution.Api"
RUN dotnet build "MTrader.OrderExecution.Api.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MTrader.OrderExecution.Api.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MTrader.OrderExecution.Api.dll"]