FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["SeleniumAutomationAPI/SeleniumAutomationAPI.csproj", "SeleniumAutomationAPI/"]
RUN dotnet restore "SeleniumAutomationAPI/SeleniumAutomationAPI.csproj"
COPY . .
WORKDIR "/src/SeleniumAutomationAPI"
RUN dotnet build "SeleniumAutomationAPI.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "SeleniumAutomationAPI.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "SeleniumAutomationAPI.dll"]