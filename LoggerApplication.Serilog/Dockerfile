FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["LoggerApplication.Serilog/LoggerApplication.Serilog.csproj", "LoggerApplication.Serilog/"]
RUN dotnet restore "LoggerApplication.Serilog/LoggerApplication.Serilog.csproj"
COPY . .
WORKDIR "/src/LoggerApplication.Serilog"
RUN dotnet build "LoggerApplication.Serilog.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "LoggerApplication.Serilog.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "LoggerApplication.Serilog.dll"]
