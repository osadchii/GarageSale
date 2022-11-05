FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Sources/GarageSale.ManagementBot/GarageSale.ManagementBot.csproj", "GarageSale.ManagementBot/"]
RUN dotnet restore "Sources/GarageSale.ManagementBot/GarageSale.ManagementBot.csproj"
COPY . .
WORKDIR "/src/GarageSale.ManagementBot"
RUN dotnet build "GarageSale.ManagementBot.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "GarageSale.ManagementBot.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "GarageSale.ManagementBot.dll"]
