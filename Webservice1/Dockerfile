FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 5000
EXPOSE 443
ENV ASPNETCORE_URLS=http://+:5000
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Webservice1/Webservice1.csproj", "Webservice1/"]
RUN dotnet restore "Webservice1/Webservice1.csproj"
COPY . .
WORKDIR "/src/Webservice1"
RUN dotnet build "Webservice1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Webservice1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Webservice1.dll"]
