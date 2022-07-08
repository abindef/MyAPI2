#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["MyAPI2/MyAPI2.csproj", "MyAPI2/"]
RUN dotnet restore "MyAPI2/MyAPI2.csproj"
COPY . .
WORKDIR "/src/MyAPI2"
RUN dotnet build "MyAPI2.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MyAPI2.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MyAPI2.dll"]