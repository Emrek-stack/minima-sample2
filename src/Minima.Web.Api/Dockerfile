FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["src/Minima.Web.Api/Minima.Web.Api.csproj", "src/Minima.Web.Api/"]
RUN dotnet restore "src/Minima.Web.Api/Minima.Web.Api.csproj"
COPY . .
WORKDIR "/src/src/Minima.Web.Api"
RUN dotnet build "Minima.Web.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Minima.Web.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Minima.Web.Api.dll"]
