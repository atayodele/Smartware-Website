FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["SmartwareWebsite/SmartwareWebsite.csproj", "SmartwareWebsite/"]
RUN dotnet restore "SmartwareWebsite/SmartwareWebsite.csproj"
COPY . .
WORKDIR "/src/SmartwareWebsite"
RUN dotnet build "SmartwareWebsite.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "SmartwareWebsite.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "SmartwareWebsite.dll"]