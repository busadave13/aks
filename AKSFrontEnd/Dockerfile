FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 8455

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["AKSFrontEnd.csproj", "AKSFrontEnd/"]

RUN dotnet restore "AKSFrontEnd/AKSFrontEnd.csproj"
WORKDIR "src/AKSFrontEnd"
COPY . .
RUN dotnet build "AKSFrontEnd.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "AKSFrontEnd.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AKSFrontEnd.dll"]