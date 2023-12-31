FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src

COPY ["./Desafio.API/Desafio.API.csproj", "Desafio.API/"]
COPY ["./Desafio.API.Application/Desafio.API.Application.csproj", "Desafio.API.Application/"]
COPY ["./Desafio.API.Domain/Desafio.API.Domain.csproj", "Desafio.API.Domain/"]

RUN dotnet restore "Desafio.API/Desafio.API.csproj"

COPY . .
WORKDIR "/src/Desafio.API"
RUN dotnet build "Desafio.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Desafio.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Desafio.API.dll"]