FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Nettoyer le cache NuGet avant restore
RUN dotnet nuget locals all --clear

COPY *.csproj ./
RUN dotnet restore --no-cache

COPY . ./
RUN dotnet publish -c Release -o out

FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /app/out .
EXPOSE 8080
ENV ASPNETCORE_URLS=http://+:8080
ENTRYPOINT ["dotnet", "BrasilBurgerWeb.dll"]
