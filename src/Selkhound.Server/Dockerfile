﻿FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Selkhound.Server/Selkhound.Server.csproj", "Selkhound.Server/"]
RUN dotnet restore "Selkhound.Server/Selkhound.Server.csproj"
COPY . .
WORKDIR "/src/Selkhound.Server"
RUN dotnet build "Selkhound.Server.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Selkhound.Server.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Selkhound.Server.dll"]
