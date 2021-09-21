#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["Jenkins_.Net/Jenkins_.Net.csproj", "Jenkins_.Net/"]
RUN dotnet restore "Jenkins_.Net/Jenkins_.Net.csproj"
COPY . .
WORKDIR "/src/Jenkins_.Net"
RUN dotnet build "Jenkins_.Net.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Jenkins_.Net.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Jenkins_.Net.dll"]