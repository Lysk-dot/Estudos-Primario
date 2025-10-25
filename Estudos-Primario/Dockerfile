FROM mcr.microsoft.com/dotnet/runtime:9.0 AS base
USER $APP_UID
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["Estudos-Primario/Estudos-Primario.csproj", "Estudos-Primario/"]
RUN dotnet restore "Estudos-Primario/Estudos-Primario.csproj"
COPY . .
WORKDIR "/src/Estudos-Primario"
RUN dotnet build "./Estudos-Primario.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "./Estudos-Primario.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Estudos-Primario.dll"]
