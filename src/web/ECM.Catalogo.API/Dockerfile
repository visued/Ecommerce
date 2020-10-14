#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["src/web/ECM.Catalogo.API/ECM.Catalogo.API.csproj", "src/web/ECM.Catalogo.API/"]
RUN dotnet restore "src/web/ECM.Catalogo.API/ECM.Catalogo.API.csproj"
COPY . .
WORKDIR "/src/src/web/ECM.Catalogo.API"
RUN dotnet build "ECM.Catalogo.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ECM.Catalogo.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ECM.Catalogo.API.dll"]