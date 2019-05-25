FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["FuckYou/FuckYou.csproj", "FuckYou/"]
RUN dotnet restore "FuckYou/FuckYou.csproj"
COPY . .
WORKDIR "/src/FuckYou"
RUN dotnet build "FuckYou.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "FuckYou.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "FuckYou.dll"]