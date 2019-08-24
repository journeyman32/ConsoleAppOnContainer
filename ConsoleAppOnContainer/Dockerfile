FROM mcr.microsoft.com/dotnet/core/runtime:2.1-stretch-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["ConsoleAppOnContainer/ConsoleAppOnContainer.csproj", "ConsoleAppOnContainer/"]
RUN dotnet restore "ConsoleAppOnContainer/ConsoleAppOnContainer.csproj"
COPY . .
WORKDIR "/src/ConsoleAppOnContainer"
RUN dotnet build "ConsoleAppOnContainer.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ConsoleAppOnContainer.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ConsoleAppOnContainer.dll"]