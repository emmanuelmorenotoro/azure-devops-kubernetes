#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY SeekQ.Geo.Api/SeekQ.Geo.Api.csproj SeekQ.Geo.Api/
COPY App.Common/App.Common.csproj App.Common/
RUN dotnet restore "SeekQ.Geo.Api/SeekQ.Geo.Api.csproj"
COPY . .
WORKDIR "/src/SeekQ.Geo.Api"
RUN dotnet build "SeekQ.Geo.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SeekQ.Geo.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SeekQ.Geo.Api.dll"]
