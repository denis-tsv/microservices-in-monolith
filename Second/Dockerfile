﻿FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Second/Second.csproj", "Second/"]
RUN dotnet restore "Second/Second.csproj"
COPY . .
WORKDIR "/src/Second"
RUN dotnet build "Second.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Second.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Second.dll"]
