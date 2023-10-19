#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["TestAPI1/TestAPI1.csproj", "TestAPI1/"]
RUN dotnet restore "TestAPI1/TestAPI1.csproj"
COPY . .
WORKDIR "/src/TestAPI1"
RUN dotnet build "TestAPI1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TestAPI1.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TestAPI1.dll"]