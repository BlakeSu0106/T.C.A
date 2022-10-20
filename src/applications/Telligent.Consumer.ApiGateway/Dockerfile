#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["src/applications/Telligent.Consumer.ApiGateway/Telligent.Consumer.ApiGateway.csproj", "src/applications/Telligent.Consumer.ApiGateway/"]
RUN dotnet restore "src/applications/Telligent.Consumer.ApiGateway/Telligent.Consumer.ApiGateway.csproj"
COPY . .
WORKDIR "/src/src/applications/Telligent.Consumer.ApiGateway"
RUN dotnet build "Telligent.Consumer.ApiGateway.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Telligent.Consumer.ApiGateway.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Telligent.Consumer.ApiGateway.dll"]