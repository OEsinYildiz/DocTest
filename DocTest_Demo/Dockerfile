FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["DocTest_Demo/DocTest_Demo.csproj", "DocTest_Demo/"]
RUN dotnet restore "DocTest_Demo/DocTest_Demo.csproj"
COPY . .
WORKDIR "/src/DocTest_Demo"
RUN dotnet build "DocTest_Demo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DocTest_Demo.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DocTest_Demo.dll"]
