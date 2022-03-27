#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["dotnet-codedeploy-demo/dotnet-codedeploy-demo.csproj", "dotnet-codedeploy-demo/"]
RUN dotnet restore "dotnet-codedeploy-demo/dotnet-codedeploy-demo.csproj"
COPY . .
WORKDIR "/src/dotnet-codedeploy-demo"
RUN dotnet build "dotnet-codedeploy-demo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "dotnet-codedeploy-demo.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "dotnet-codedeploy-demo.dll"]