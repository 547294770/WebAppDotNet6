#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["WebAppDotNet6/WebAppDotNet6.csproj", "WebAppDotNet6/"]
RUN dotnet restore "WebAppDotNet6/WebAppDotNet6.csproj"
COPY . .
WORKDIR "/src/WebAppDotNet6"
RUN dotnet build "WebAppDotNet6.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebAppDotNet6.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebAppDotNet6.dll"]