FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Example.WeatherForecast.API/Example.WeatherForecast.API.csproj", "Example.WeatherForecast.API/"]
RUN dotnet restore "Example.WeatherForecast.API/Example.WeatherForecast.API.csproj"
COPY . .
WORKDIR "/src/Example.WeatherForecast.API"
RUN dotnet build "Example.WeatherForecast.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Example.WeatherForecast.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Example.WeatherForecast.API.dll"]
