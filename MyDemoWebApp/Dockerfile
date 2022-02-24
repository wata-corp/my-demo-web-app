FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["MyDemoWebApp/MyDemoWebApp.csproj", "MyDemoWebApp/"]
RUN dotnet restore "MyDemoWebApp/MyDemoWebApp.csproj"
COPY . .
WORKDIR "/src/MyDemoWebApp"
RUN dotnet build "MyDemoWebApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MyDemoWebApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MyDemoWebApp.dll"]
