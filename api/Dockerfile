FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
# Adding 443 port
EXPOSE 443 
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src

# Copy API
COPY Basic3TierAPI/Basic3TierAPI.csproj Basic3TierAPI/
# Restore API
RUN dotnet restore "Basic3TierAPI/Basic3TierAPI.csproj"
#Copy Infra
COPY Basic3Tier.Infrastructure/Basic3Tier.Infrastructure.csproj Basic3Tier.Infrastructure/
# Restore Infra
RUN dotnet restore "Basic3Tier.Infrastructure/Basic3Tier.Infrastructure.csproj"
# Copy Core
COPY Basic3Tier.Core/Basic3Tier.Core.csproj Basic3Tier.Core/
RUN dotnet restore "Basic3Tier.Core/Basic3Tier.Core.csproj"

COPY . .
WORKDIR "/src/Basic3TierAPI"
RUN dotnet build -c Release -o /app/build

FROM build AS publish
RUN dotnet publish -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Basic3TierAPI.dll"]
