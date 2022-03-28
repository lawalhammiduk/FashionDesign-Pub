#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["FashionDesign.csproj", "."]
RUN dotnet restore "./FashionDesign.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "FashionDesign.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "FashionDesign.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "FashionDesign.dll"]