# Use the official ASP.NET Core runtime image as base
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

# Use the .NET SDK image to build the app
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy csproj and restore dependencies
COPY ["OrderInvoiceSystem.csproj", "./"]
RUN dotnet restore "./OrderInvoiceSystem.csproj"

# Copy the rest of the source code
COPY . .

# Build and publish the app to the /app/publish folder
RUN dotnet publish "OrderInvoiceSystem.csproj" -c Release -o /app/publish --no-restore

# Final stage: build runtime image
FROM base AS final
WORKDIR /app
COPY --from=build /app/publish .
