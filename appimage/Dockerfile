FROM ghcr.io/chrismellard/baseimage:164c1657a876127fdeecea7f8f3a100d144c7bc3 AS base

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
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "appimage.dll"]
