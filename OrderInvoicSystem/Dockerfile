# Base image with ASP.NET Core runtime
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

# SDK image for building the app
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy the .csproj file and restore dependencies
COPY OrderInvoicSystem/OrderInvoicSystem.csproj ./
RUN dotnet restore "OrderInvoicSystem.csproj"

# Copy the rest of the source code
COPY OrderInvoicSystem/. ./
RUN dotnet publish "OrderInvoicSystem.csproj" -c Release -o /app/publish

# Final runtime image
FROM base AS final
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "OrderInvoicSystem.dll"]
