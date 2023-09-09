FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["FoolCardGame.Api/FoolCardGame.Api.csproj", "FoolCardGame.Api/"]
RUN dotnet restore "FoolCardGame.Api/FoolCardGame.Api.csproj"
COPY . .
WORKDIR "/src/FoolCardGame.Api"
RUN dotnet build "FoolCardGame.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "FoolCardGame.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "FoolCardGame.Api.dll"]
