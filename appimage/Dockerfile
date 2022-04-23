FROM ghcr.io/chrismellard/baseimage:e6a44600cf5835d1d5ca9b0b32128fe5887c8115 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["appimage/appimage.csproj", "appimage/"]
RUN dotnet restore "appimage/appimage.csproj"
COPY . .
WORKDIR "/src/appimage"
RUN dotnet build "appimage.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "appimage.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "appimage.dll"]
