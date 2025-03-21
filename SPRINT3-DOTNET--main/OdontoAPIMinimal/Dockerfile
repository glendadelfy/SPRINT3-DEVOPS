FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 8080


FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["OdontoAPIMinimal.csproj", "."]
RUN dotnet restore "./OdontoAPIMinimal.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "OdontoAPIMinimal.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "OdontoAPIMinimal.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "OdontoAPIMinimal.dll"]