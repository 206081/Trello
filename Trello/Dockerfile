FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["Trello/Trello.csproj", "Trello/"]
RUN dotnet restore "Trello/Trello.csproj"
COPY . .
WORKDIR "/src/Trello"
RUN dotnet build "Trello.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Trello.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Trello.dll"]