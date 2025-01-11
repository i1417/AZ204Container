FROM mcr.microsoft.com/dotnet/aspnet:7.0 as base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
COPY . /src
WORKDIR /src
#RUN CMD ls
RUN dotnet build "MyApiProject.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MyApiProject.csproj" -c Release -o /app/publish

#Build runtime image
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MyApiProject.dll"]