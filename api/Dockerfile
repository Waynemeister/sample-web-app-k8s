FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["Basic3Tier.Core.csproj", "./"]
RUN dotnet restore "Basic3Tier.Core.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "Basic3Tier.Core.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Basic3Tier.Core.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Basic3Tier.Core.csproj.dll"]
