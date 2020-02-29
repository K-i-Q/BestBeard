#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["BestBeard.Web.Api/BestBeard.Web.Api.csproj", "BestBeard.Web.Api/"]
RUN dotnet restore "BestBeard.Web.Api/BestBeard.Web.Api.csproj"
COPY . .
WORKDIR "/src/BestBeard.Web.Api"
RUN dotnet build "BestBeard.Web.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BestBeard.Web.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BestBeard.Web.Api.dll"]