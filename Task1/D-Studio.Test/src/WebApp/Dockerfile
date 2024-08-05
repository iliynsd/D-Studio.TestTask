FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["D-Studio.Test/D-Studio.Test.csproj", "D-Studio.Test/"]
RUN dotnet restore "D-Studio.Test/D-Studio.Test.csproj"
COPY . .
WORKDIR "/src/D-Studio.Test"
RUN dotnet build "D-Studio.Test.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "D-Studio.Test.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "D-Studio.Test.dll"]
