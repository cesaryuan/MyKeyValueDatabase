#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["MyKeyValueDatabase/MyKeyValueDatabase.csproj", "MyKeyValueDatabase/"]
RUN dotnet restore "MyKeyValueDatabase/MyKeyValueDatabase.csproj"
COPY . .
WORKDIR "/src/MyKeyValueDatabase"
RUN dotnet build "MyKeyValueDatabase.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MyKeyValueDatabase.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MyKeyValueDatabase.dll"]