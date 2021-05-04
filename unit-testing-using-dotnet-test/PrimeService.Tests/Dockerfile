FROM mcr.microsoft.com/dotnet/runtime:3.1 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["unit-testing-using-dotnet-test/PrimeService.Tests/PrimeService.Tests.csproj", "unit-testing-using-dotnet-test/PrimeService.Tests/"]
RUN dotnet restore "unit-testing-using-dotnet-test\PrimeService.Tests\PrimeService.Tests.csproj"
COPY . .
WORKDIR "/src/unit-testing-using-dotnet-test/PrimeService.Tests"
RUN dotnet build "PrimeService.Tests.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PrimeService.Tests.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PrimeService.Tests.dll"]
