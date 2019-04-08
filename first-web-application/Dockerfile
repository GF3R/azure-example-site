FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["first-web-application/first-web-application.csproj", "first-web-application/"]
RUN dotnet restore "first-web-application/first-web-application.csproj"
COPY . .
WORKDIR "/src/first-web-application"
RUN dotnet build "first-web-application.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "first-web-application.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "first-web-application.dll"]