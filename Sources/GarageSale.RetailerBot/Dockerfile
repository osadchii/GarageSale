FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Sources/GarageSale.RetailerBot/GarageSale.RetailerBot.csproj", "GarageSale.RetailerBot/"]
RUN dotnet restore "Sources/GarageSale.RetailerBot/GarageSale.RetailerBot.csproj"
COPY . .
WORKDIR "/src/GarageSale.RetailerBot"
RUN dotnet build "GarageSale.RetailerBot.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "GarageSale.RetailerBot.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "GarageSale.RetailerBot.dll"]
