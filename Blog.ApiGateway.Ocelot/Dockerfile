#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["Blog.ApiGateway.Ocelot/Blog.ApiGateway.Ocelot.csproj", "Blog.ApiGateway.Ocelot/"]
RUN dotnet restore "Blog.ApiGateway.Ocelot/Blog.ApiGateway.Ocelot.csproj"
COPY . .
WORKDIR "/src/Blog.ApiGateway.Ocelot"
RUN dotnet build "Blog.ApiGateway.Ocelot.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Blog.ApiGateway.Ocelot.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Blog.ApiGateway.Ocelot.dll"]