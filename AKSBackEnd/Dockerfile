FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 8411

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["AKSBackEnd/AKSBackEnd.csproj", "AKSBackEnd/"]

RUN dotnet restore "$PROJECT_DIR/AKSBackEnd.csproj"
COPY . .
WORKDIR "/src/AKSBackEnd"
RUN dotnet build "AKSBackEnd.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "AKSBackEnd.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AKSBackEnd.dll"]