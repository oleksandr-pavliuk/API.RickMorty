FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["RickMortyAPI/RickMortyAPI.csproj", "RickMortyAPI/"]
RUN dotnet restore "RickMortyAPI/RickMortyAPI.csproj"
COPY . .
WORKDIR "/src/RickMortyAPI"
RUN dotnet build "RickMortyAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "RickMortyAPI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "RickMortyAPI.dll"]
