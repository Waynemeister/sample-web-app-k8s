FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src

# Copy core
COPY ["Basic3Tier.Core.csproj", "./"]
# Restore as distinct layers
RUN dotnet restore "Basic3Tier.Core.csproj"

# Copy infrastructure
COPY ["Basic3Tier.Infrastructure.csproj", "./"]
# Restore as distinct layers
RUN dotnet restore "Basic3Tier.Infrastructure.csproj"

# Copy API
COPY ["Basic3TierAPI.csproj", "./"]
# Restore as distinct layers
RUN dotnet restore "Basic3TierAPI.csproj"


COPY . .
WORKDIR "/src/."
RUN dotnet build -c Release -o /app/build

FROM build AS publish
RUN dotnet publish -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Basic3Tier.Core.csproj.dll"]
