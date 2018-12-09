FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["AKSFrontEnd/AKSFrontEnd.csproj", "AKSFrontEnd/"]

RUN dotnet restore "$PROJECT_DIR/AKSFrontEnd.csproj"
COPY . .
WORKDIR "/src/AKSFrontEnd"
RUN dotnet build "AKSFrontEnd.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "AKSFrontEnd.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AKSFrontEnd.dll"]