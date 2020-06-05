FROM mcr.microsoft.com/dotnet/core/sdk:3.1-alpine AS base

WORKDIR /app

COPY SampleApi.sln .
COPY SampleApi/SampleApi.csproj ./SampleApi/

RUN dotnet restore
EXPOSE 5000
ENTRYPOINT ["dotnet", "watch", "-p", "SampleApi.sln", "run", "-p", "SampleApi", "--urls", "http://0.0.0.0:5000"]

#--------------------------------------#
FROM base AS builder

COPY . .

RUN dotnet publish -c Release -o /publish

#--------------------------------------#
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-alpine

WORKDIR /app

COPY --from=builder /publish .

EXPOSE 80
ENTRYPOINT ["dotnet", "SampleApi.dll"]